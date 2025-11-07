
# Token Holding Campaign

This page provides a detailed reference for the `GetTokenHoldingCampaigns` API, which allows you to retrieve information about token holding campaigns by different filters.

### Endpoint

```
POST https://incentra-prd.brevis.network/sdk/v1/tokenholdingCampaigns
```

### Request

<table><thead><tr><th width="181.296875">Field</th><th width="187.953125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>[uint64]</code></td><td>Chain ID(s) where the target token is deployed.</td></tr><tr><td><code>token_address</code></td><td><code>[string]</code></td><td>Filter by the address(es) of the token being held for the campaign.</td></tr><tr><td><code>campaign_id</code></td><td><code>[string]</code></td><td>Filter by specific campaign ID(s).</td></tr><tr><td><code>status</code></td><td><code>[CampaignStatus]</code></td><td>Filter by campaign status(es).  Enum will be specified later.</td></tr><tr><td><code>user_address</code></td><td><code>[string]</code></td><td>Retrieve campaigns where the specified user address(es) has participated.</td></tr></tbody></table>

If any filter is not specified, it means there is no constraint for this filter.

`CampaignStatus` **Enum**

The `CampaignStatus` enum has the following values:

* `DEPLOYING`
* `CREATING_FAILED`
* `INACTIVE`
* `ACTIVE`
* `ENDED`
* `DEACTIVATED`

### Response

<table><thead><tr><th width="148.0625">Field</th><th width="332.00390625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>err</code></td><td><code>ErrMsg</code></td><td>Error message.</td></tr><tr><td><code>campaigns</code></td><td><code>[TokenHoldingCampaignInfo]</code></td><td>List of matching token holding campaigns.</td></tr></tbody></table>

`TokenHoldingCampaignInfo` **Fields**

<table><thead><tr><th width="281.3828125">Field</th><th width="162.56640625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>uint64</code></td><td>Chain ID where the target token is deployed.</td></tr><tr><td><code>token_address</code></td><td><code>string</code></td><td>Address of the token being held.</td></tr><tr><td><code>token_symbol</code></td><td><code>string</code></td><td>Symbol of the token being held (e.g., "WETH", "USDC").</td></tr><tr><td><code>campaign_id</code></td><td><code>string</code></td><td>Campaign ID.</td></tr><tr><td><code>campaign_name</code></td><td><code>string</code></td><td>Campaign display name.</td></tr><tr><td><code>start_time</code></td><td><code>uint64</code></td><td>Campaign start timestamp.</td></tr><tr><td><code>end_time</code></td><td><code>uint64</code></td><td>Campaign end timestamp.</td></tr><tr><td><code>reward_info</code></td><td><code>RewardInfo</code></td><td>Details about the reward token and amount. See <code>RewardInfo</code> below.</td></tr><tr><td><code>last_reward_attestation_time</code></td><td><code>uint64</code></td><td>Timestamp of the last reward calculation/snapshot.</td></tr><tr><td><code>status</code></td><td><code>CampaignStatus</code></td><td>Current status of the campaign. See <code>CampaignStatus</code> enum.</td></tr></tbody></table>

`RewardInfo` **Fields**

<table><thead><tr><th width="203.0625">Field</th><th width="98.703125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>submission_chain_id</code></td><td><code>uint64</code></td><td>Campaign reward submission chain ID (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details)</td></tr><tr><td><code>submission_contract</code></td><td><code>string</code></td><td>Campaign reward submission contract address (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details)</td></tr><tr><td><code>claim_chain_id</code></td><td><code>uint64</code></td><td>Chain ID where rewards can be claimed.</td></tr><tr><td><code>claim_contract</code></td><td><code>string</code></td><td>Address of the smart contract used for claiming rewards.</td></tr><tr><td><code>token_address</code></td><td><code>string</code></td><td>Address of the reward token.</td></tr><tr><td><code>token_symbol</code></td><td><code>string</code></td><td>Symbol of the reward token (e.g., "WETH").</td></tr><tr><td><code>reward_amt</code></td><td><code>string</code></td><td>Total reward amount for this campaign.</td></tr><tr><td><code>reward_usd_price</code></td><td><code>string</code></td><td>USD price for the reward token.</td></tr><tr><td><code>reward_per_hour</code></td><td><code>string</code></td><td>Reward amount distributed per hour.</td></tr><tr><td><code>apr</code></td><td><code>float</code></td><td>The APR of the campaign (for example, 0.03 means 3% APR)</td></tr><tr><td><code>tvl</code></td><td><code>float</code></td><td>The total supply USD value of the token to be held</td></tr></tbody></table>

### Example Request (curl)


```json
{
    "chain_id": [
        1,
        42161
    ],
    "token_address": [
        "0x8D983cb9388EaC77af0474fA441C4815500Cb7BB"
    ],
    "campaign_id": [

    ],
    "status": [
        4,
        5
    ],
    "user_address": [

    ]
}
```


post with `data.json`

```sh
curl -X POST -H "Content-Type: application/json" -d @data.json https://incentra-prd.brevis.network/sdk/v1/tokenholdingCampaignsityCampaigns
```

