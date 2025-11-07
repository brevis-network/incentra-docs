# Read and Claim Rewards

## Same-chain reward claim

If the ZK-attested rewards information is submitted to the same chain that hosts the campaign for users to claim rewards, the reward claim process is straightforward: call the following functions.

```solidity
// claim reward, send reward token to the earner
function claim(address earner) external;

// claim reward, send reward token to address specified by the earner (msg.sender)
function claimWithRecipient(address to) external;
```

One can obtain a user's _cumulative rewards and unclaimed rewards_ through the following view functions.

```solidity
struct AddrAmt {
    address token;
    uint256 amount;
}

// get cumulative rewards
function viewTotalRewards(address user) external view returns (AddrAmt[] memory) ;
// get unclaimed rewards
function viewUnclaimedRewards(address earner) external view returns (AddrAmt[] memory);
```

## Cross-chain reward claim

To reduce the gas cost of the campaign on an expensive chain (e.g., Ethereum), we can configure the system to submit ZK-attested rewards on a more affordable chain (e.g., Optimism, Arbitrum), then bridge the Merkle root of all rewards back to the campaign chain.

In this case, there are 2 contracts:

1. **Rewards Submission contract** where the ZK-proved rewards are submitted. The Rewards Submission contract builds and stores the entire reward Merkle tree.
2. **Rewards Claim contract** that synchronizes the Merkle root from the Rewards Submission contract. Users interact with this contract to claim their rewards by providing a Merkle proof. This contract also escrows the rewards and stores each user’s already-claimed reward amount.

**To claim rewards, the user needs to**&#x20;

1. Obtain the reward information along with the Merkle proof by calling the [Get Reward Merkle Proof API](read-and-claim-rewards.md#get-reward-merkle-proof-api).
2. Submit the reward information along with the Merkle proof to the **Reward Claim contract.**&#x20;

**NOTE:** There is also a "**ClaimAll**" contract which can help claim a user's rewards from multiple campaigns in a single transaction. See [here](read-and-claim-rewards.md#claim-all-rewards-in-a-single-transaction) for details.

```solidity
// claim reward, send reward token to the earner
function claim(
    address earner, 
    uint256[] calldata cumulativeAmounts, 
    uint64 epoch, 
    bytes32[] calldata proof) external;

// claim reward, send reward token to address specified by the earner (msg.sender)    
function claimWithRecipient(
    address to,
    uint256[] calldata cumulativeAmounts,
    uint64 _epoch,
    bytes32[] calldata proof
) external
```

**To get a user's claimable reward amount:**

A user's currently claimable reward amount and the cumulative reward amount can be obtained by calling the [Get Reward Merkle Proof API](read-and-claim-rewards.md#get-reward-merkle-proof-api) (enclosed together with the Merkle proof) or [Get Reward Balance API](read-and-claim-rewards.md#get-reward-balance-api) (an API dedicated to display a user's reward balances).

### Get Reward Merkle Proof API

This API returns the reward info and the corresponding Merkle proofs of a specific user in multiple campaigns that the user has participated in (i.e., has non-zero cumulative rewards in the campaign) and match the supplied filters in the request. The data included in the response can be used to call the `claim` or `claimWithRecipient` functions of the claim chain contract.

#### **Endpoint**

```
POST https://incentra-prd.brevis.network/v1/getMerkleProofsBatch
```

#### **Request Fields**

The request data should specify a user address and multiple filters for the campaign.&#x20;

**NOTE**: `user_addr` is a required field while other filters are optional. If any filter is not specified in the request, it means no constraint for the filter.

<table><thead><tr><th width="135.546875">Field</th><th width="177.828125">Type</th><th> Description</th></tr></thead><tbody><tr><td><code>user_addr</code></td><td><code>string</code></td><td>The user address.</td></tr><tr><td><code>types</code></td><td><code>[CampaignType]</code></td><td>The campaign types (the detailed enum will be specified later). </td></tr><tr><td><code>chain_id</code></td><td><code>[uint64]</code></td><td>The chain IDs where the DEX pools/Euler vaults/tokens are deployed.</td></tr><tr><td><code>status</code></td><td><code>[CampaignStatus]</code></td><td><p>The campaign statuses with enum:<br><code>INACTIVE = 3</code></p><p><code>ACTIVE = 4</code></p><p><code>ENDED = 5</code></p></td></tr><tr><td><code>campaign_id</code></td><td><code>[string]</code></td><td>The campaign IDs.</td></tr></tbody></table>

**`CampaignType`** enum:

* Liquidity campaign (Uniswap v3) = **1**
* Liquidity campaign (PancakeSwap v3) = **3**
* Liquidity campaign (QuickSwap v3) = **5**
* Token holding campaign = **1001**
* Euler borrow campaign = **2001**
* Euler lend campaign = **2002**

#### **Response Fields** <a href="#response-fields" id="response-fields"></a>

<table><thead><tr><th width="144.19140625">Field</th><th width="262.71875">Type</th><th> Description</th></tr></thead><tbody><tr><td><code>err</code></td><td><code>ErrMsg</code></td><td>Error details if the request failed.</td></tr><tr><td><code>rewardsBatch</code></td><td><code>[SingleCampaignMerkle]</code></td><td>An array that includes the details about rewards info and the corresponding Merkle proofs of the user in all the campaigns that user has participated in and match the filters.</td></tr></tbody></table>

**ErrMsg Fields**

<table><thead><tr><th width="198.71484375">Field</th><th width="238.9609375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>code</code></td><td><code>string</code></td><td>Error code</td></tr><tr><td><code>msg</code></td><td><code>string</code></td><td>Error reason</td></tr></tbody></table>

**SingleCampaignMerkle Fields**

<table><thead><tr><th width="205.2421875">Fileld</th><th width="151.48046875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>campaignId</code></td><td><code>string</code></td><td>The campaign ID.</td></tr><tr><td><code>epoch</code></td><td><code>string</code></td><td>The rewards in the Merkle tree is accumulated up to this epoch number.</td></tr><tr><td><code>claimChainId</code></td><td><code>string</code></td><td>The claim chain ID.</td></tr><tr><td><code>claimContractAddr</code></td><td><code>string</code></td><td>The claim contract address.</td></tr><tr><td><code>cumulativeRewards</code></td><td><code>[string]</code></td><td>The cumulative reward amount earned by the user in the campaign so far.</td></tr><tr><td><code>merkleProof</code></td><td><code>[string]</code></td><td>The Merkle path proof to be submitted to the claim contract.</td></tr><tr><td><code>claimableRewards</code></td><td><code>string</code></td><td>The claimable reward amount of this user in the campaign.</td></tr></tbody></table>

#### Example Request (curl)

```powershell
curl --location 'https://incentra-prd.brevis.network/v1/getMerkleProofsBatch' \
--header 'Content-Type: application/json' \
--data '{
    "user_addr": "0x0195b198088e464103e3840f52a1fa9ea81de84b",
    "types": [
        1001
    ],
    "chain_id": [
        1
    ],
    "status": [],
    "campaign_id": []
}'
```

### Get Reward Balance API

This API returns the cumulative and claimable reward balances of a specific user in all campaigns the user has participated in and match the specified filters.

#### **Endpoint**

```
POST https://incentra-prd.brevis.network/v1/getUserRewardsBatch
```

#### **Request Fields**

The request data should specify a user address and multiple filters for the campaign.&#x20;

**NOTE**: `user_addr` is a required field while other filters are optional. If any filter is not specified in the request, it means no constraint for the filter.

<table><thead><tr><th width="135.546875">Field</th><th width="177.828125">Type</th><th> Description</th></tr></thead><tbody><tr><td><code>user_addr</code></td><td><code>string</code></td><td>The user address.</td></tr><tr><td><code>types</code></td><td><code>[CampaignType]</code></td><td>The campaign types (the detailed enum will be specified later). </td></tr><tr><td><code>chain_id</code></td><td><code>[uint64]</code></td><td>The chain IDs where the DEX pools/Euler vaults/tokens are deployed.</td></tr><tr><td><code>status</code></td><td><code>[CampaignStatus]</code></td><td><p>The campaign statuses with enum:<br><code>INACTIVE = 3</code></p><p><code>ACTIVE = 4</code></p><p><code>ENDED = 5</code></p></td></tr><tr><td><code>campaign_id</code></td><td><code>[string]</code></td><td>The campaign IDs.</td></tr></tbody></table>

**`CampaignType`** enum:

* Liquidity campaign (Uniswap v3) = **1**
* Liquidity campaign (PancakeSwap v3) = **3**
* Liquidity campaign (QuickSwap v3) = **5**
* Token holding campaign = **1001**
* Euler borrow campaign = **2001**
* Euler lend campaign = **2002**

#### **Response Fields** <a href="#response-fields" id="response-fields"></a>

<table><thead><tr><th width="186.3046875">Field</th><th width="225.66796875">Type</th><th> Description</th></tr></thead><tbody><tr><td><code>err</code></td><td><code>ErrMsg</code></td><td>Error details if the request failed.</td></tr><tr><td><code>rewardsBatch</code></td><td><code>[SingleCampaignReward]</code></td><td>An array that contains the reward balances of the user in all the campaigns that user has participated in and match the filters.</td></tr></tbody></table>

**ErrMsg Fields**

<table><thead><tr><th width="185.33203125">Field</th><th width="187.03515625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>code</code></td><td><code>string</code></td><td>Error code.</td></tr><tr><td><code>msg</code></td><td><code>string</code></td><td>Error reason.</td></tr></tbody></table>

**SingleCampaignReward Fields**

<table><thead><tr><th width="189.17578125">Fileld</th><th width="186.65234375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>cumulative</code></td><td><code>string</code></td><td>The cumulative reward amount earned by the user in the campaign.</td></tr><tr><td><code>claimable</code></td><td><code>string</code></td><td>The claimable reward amount of the user in the campaign.</td></tr><tr><td><code>campaignId</code></td><td><code>string</code></td><td>The campaign ID.</td></tr><tr><td><code>claimChainId</code></td><td><code>string</code></td><td>The claim chain ID.</td></tr></tbody></table>

#### Example Request (curl)

```powershell
curl --location 'https://incentra-prd.brevis.network/v1/getUserRewardsBatch' \
--header 'Content-Type: application/json' \
--data '{
    "user_addr": "0x0195b198088e464103e3840f52a1fa9ea81de84b",
    "types": [
        1001
    ],
    "chain_id": [
        1
    ],
    "status": [],
    "campaign_id": []
}'
```

## Claim all rewards in a single transaction

A user can claim all rewards from all participated campaigns on a given chain in a single transaction by calling the following functions of the `ClaimAll` contract deployed on that chain:


```solidity
// claim all same-chain rewards
function claimAll(address earner, address[] calldata campaignAddrs) external;

// claim all cross-chain rewards 
// calldata can be fetched using the getMerkleProofsBatch API
struct CampaignReward {
    address campaignAddr; // the campaign claim contract address
    uint256[] cumulativeAmounts;
    uint64 epoch;
    bytes32[] proof;
}
function claimAll(address earner, CampaignReward[] calldata campaignRewards) external;

// claim all same-chain and cross-chain rewards
function claimAll(
    address earner, 
    address[] calldata sameChainCampaignAddrs, 
    CampaignReward[] calldata crossChainCampaignRewards) external;
```


The currently deployed `ClaimAll` contract addresses are:

<table><thead><tr><th width="254.89453125">Chain</th><th>ClaimAll contract address</th></tr></thead><tbody><tr><td>Ethereum</td><td><a href="https://etherscan.io/address/0x39ae8501186e8f4d7b120981ddad5db8915a6371">0x39ae8501186E8F4d7b120981DDaD5db8915A6371</a></td></tr><tr><td>BNB Chain</td><td><a href="https://bscscan.com/address/0x3704597fdE1f11E4C87423B9246b295c31bfbb8d">0x3704597fdE1f11E4C87423B9246b295c31bfbb8d</a></td></tr><tr><td>Arbitrum</td><td><a href="https://arbiscan.io/address/0x273d0d19eaC2861FCF6B21893AD6d71b018E25aB">0x273d0d19eaC2861FCF6B21893AD6d71b018E25aB</a></td></tr><tr><td>World Chain</td><td><a href="https://worldscan.org/address/0xc8c741C7C4844Cd3C4B60d8dc95DF1DC452C53c6">0xc8c741C7C4844Cd3C4B60d8dc95DF1DC452C53c6</a></td></tr><tr><td>Arbitrum Sepolia Testnet</td><td><a href="https://sepolia.arbiscan.io/address/0x8fa1Bd18F30e0b387E2f24279Eca033eb2a30327">0x8fa1Bd18F30e0b387E2f24279Eca033eb2a30327</a></td></tr><tr><td>Base Sepolia Testnet</td><td><a href="https://sepolia.basescan.org/address/0x39ae8501186E8F4d7b120981DDaD5db8915A6371">0x39ae8501186E8F4d7b120981DDaD5db8915A6371</a></td></tr></tbody></table>
