
# Concentrated Liquidity Campaign

This page provides a detailed reference for the `GetLiquidityCampaigns` API, which allows you to retrieve information about concentrated liquidity campaigns for DEXes.

### Endpoint

```
POST https://incentra-prd.brevis.network/sdk/v1/liquidityCampaigns
```

### Request

<table data-header-hidden><thead><tr><th width="165.07421875">Field</th><th width="192.00390625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>[uint64]</code></td><td>Filter by the chain ID(s) where the targeted DEX pool is deployed.</td></tr><tr><td><code>campaign_type</code></td><td><code>[CampaignType]</code></td><td>Filter by the DEX protocols. Enum will be specified later.</td></tr><tr><td><code>pool_id</code></td><td><code>[string]</code></td><td>Filter by pool identifier (e.g., pool address or ID). </td></tr><tr><td><code>campaign_id</code></td><td><code>[string]</code></td><td>Filter by specific campaign ID(s).</td></tr><tr><td><code>status</code></td><td><code>[CampaignStatus]</code></td><td>Filter by campaign status(es).  Enum will be specified later.</td></tr><tr><td><code>user_address</code></td><td><code>[string]</code></td><td>Retrieve campaigns where the specified user address(es) has participated.</td></tr></tbody></table>

If any filter is not specified, it means there is no constraint for this filter.

The `CampaignType` enum has the following values:

* `UNISWAP_V3：1`
* `UNISWAP_V4：2`&#x20;
* `PANCAKE_V3：3`&#x20;
* ~~`PANCAKE_V4：4`~~&#x20;
* `QUICKSWAP_V3：5`
* `KOALASWAP：6`&#x20;
* `PANCAKE_V4_CL：8`
* `PANCAKE_V4_BIN：9`

\
`CampaignStatus` **Enum**

The `CampaignStatus` enum has the following values:

* `DEPLOYING`
* `CREATING_FAILED`
* `INACTIVE`
* `ACTIVE`
* `ENDED`
* `DEACTIVATED`

### Response

<table><thead><tr><th width="159.98046875">Field</th><th width="260.390625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>err</code></td><td><code>ErrMsg</code></td><td>Error details if the request failed.</td></tr><tr><td><code>campaigns</code></td><td><code>[LiquidityCampaignInfo]</code></td><td>List of matching liquidity campaigns.</td></tr></tbody></table>

**`LiquidityCampaignInfo` Fields**

Each campaign includes the following fields:

<table data-header-hidden><thead><tr><th width="277.73828125">Fileld</th><th width="168.19140625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>uint64</code></td><td>Chain ID where the liquidity pool is deployed.</td></tr><tr><td><code>campaign_type</code></td><td><code>CampaignType</code></td><td>The DEX protocol/version for the campaign. </td></tr><tr><td><code>pools</code></td><td><code>PoolInfo</code></td><td>Information about the specific liquidity pool targeted by the campaign.</td></tr><tr><td><code>campaign_id</code></td><td><code>string</code></td><td>Unique identifier for the campaign.</td></tr><tr><td><code>campaign_name</code></td><td><code>string</code></td><td>Campaign display name.</td></tr><tr><td><code>start_time</code></td><td><code>uint64</code></td><td>Campaign start timestamp.</td></tr><tr><td><code>end_time</code></td><td><code>uint64</code></td><td>Campaign end timestamp.</td></tr><tr><td><code>reward_info</code></td><td><code>RewardInfo</code></td><td>Details about the reward token and amount. See <code>RewardInfo</code> below.</td></tr><tr><td><code>last_reward_attestation_time</code></td><td><code>uint64</code></td><td>Last campaign reward attestation timestamp.</td></tr><tr><td><code>status</code></td><td><code>CampaignStatus</code></td><td>Current status of the campaign. See <code>CampaignStatus</code> enum.</td></tr></tbody></table>

**`PoolInfo` Fields**

<table data-header-hidden><thead><tr><th width="193.953125">Field</th><th width="159.921875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>pool_id</code></td><td><code>string</code></td><td>Pool identifier (e.g., pool address or pool ID).</td></tr><tr><td><code>pool_name</code></td><td><code>string</code></td><td>Pool display name.</td></tr></tbody></table>

**`RewardInfo` Fields**

<table data-header-hidden><thead><tr><th width="227.5546875">Field</th><th width="140.09375">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>submission_chain_id</code></td><td><code>uint64</code></td><td>Campaign reward submission chain ID (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details).</td></tr><tr><td><code>submission_contract</code></td><td><code>string</code></td><td>Campaign reward submission contract address (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details)</td></tr><tr><td><code>claim_chain_id</code></td><td><code>uint64</code></td><td>Chain ID where rewards can be claimed.</td></tr><tr><td><code>claim_contract</code></td><td><code>string</code></td><td>Smart contract address for claiming rewards.</td></tr><tr><td><code>token_address</code></td><td><code>string</code></td><td>Reward token address.</td></tr><tr><td><code>token_symbol</code></td><td><code>string</code></td><td>Reward token symbol.</td></tr><tr><td><code>reward_amt</code></td><td><code>string</code></td><td>Total reward amount for the campaign.</td></tr><tr><td><code>reward_usd_price</code></td><td><code>string</code></td><td>USD price per reward token.</td></tr><tr><td><code>reward_per_hour</code></td><td><code>string</code></td><td>Reward amount distributed per hour.</td></tr><tr><td><code>apr</code></td><td><code>float</code></td><td>The APR of the campaign (for example, 0.03 means 3% APR)</td></tr><tr><td><code>tvl</code></td><td><code>float</code></td><td>The TVL of the liquidity pool (in USD value)</td></tr></tbody></table>

### Example Request (curl)


```json
{
    "chain_id": [
        1,
        42161
    ],
    "campaign_type": [
        1,
        2,
        3,
        4,
        5
    ],
    "pool_id": [
        "0xD0A4c8A1a14530C7C9EfDaD0BA37E8cF4204d230"
    ],
    "campaign_id": [],
    "status": [
        4,
        5
    ],
    "user_address": [] // no constraint for this filter 
}
```


Post with `data.json`

```sh
curl -X POST -H "Content-Type: application/json" -d @data.json https://incentra-prd.brevis.network/sdk/v1/liquidityCampaigns
```

