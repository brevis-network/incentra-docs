---
description: Retrieve campaigns that incentivizes lending/borrowing from Euler vaults.
---

# Lend and Borrow Campaign (Euler)

This page specifies the API for retrieving details about Lend/Borrow campaigns for the Euler protocol.

### Endpoint

```
POST https://incentra-prd.brevis.network/sdk/v1/eulerCampaigns
```

### Request

<table><thead><tr><th width="171.02734375">Field</th><th width="199.8515625">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>[uint64]</code></td><td>Chain ID(s) where the targeted Euler vault is deployed.</td></tr><tr><td><code>vault_address</code></td><td><code>[string]</code></td><td>List of targeted Euler vault contract addresses.</td></tr><tr><td><code>action</code></td><td><code>[uint64]</code></td><td>Filter by campaign action type: <code>borrow: 2001</code>, <code>lend: 2002</code>.</td></tr><tr><td><code>campaign_id</code></td><td><code>[string]</code></td><td>List of specific campaign IDs to retrieve.</td></tr><tr><td><code>status</code></td><td><code>[CampaignStatus]</code></td><td>Filter by campaign status (enum will be specified later)</td></tr><tr><td><code>user_address</code></td><td><code>[string]</code></td><td>Retrieve campaigns where the specified user address(es) has participated.</td></tr></tbody></table>

If any filter is not specified, it means there is no constraint for this filter.

**`CampaignStatus` Enum**

The `CampaignStatus` enum has the following values:

* `DEPLOYING`
* `CREATING_FAILED`
* `INACTIVE`
* `ACTIVE`
* `ENDED`
* `DEACTIVATED`

### Response

<table><thead><tr><th width="225.3125">Field</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td><code>err</code></td><td><code>ErrMsg</code></td><td>Error message if request fails.</td></tr><tr><td><code>campaigns</code></td><td><code>[EulerCampaignInfo]</code></td><td>List of Euler campaign details.</td></tr></tbody></table>

`EulerCampaignInfo` **Fields**

<table><thead><tr><th width="281.55859375">Field</th><th width="163.11328125">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>chain_id</code></td><td><code>uint64</code></td><td>Chain ID where the targeted Euler vault is deployed.</td></tr><tr><td><code>vault_address</code></td><td><code>string</code></td><td>Euler vault address.</td></tr><tr><td><code>action</code></td><td><code>uint64</code></td><td>Campaign action type: <code>borrow: 2001</code>, <code>lend: 2002</code>.</td></tr><tr><td><code>campaign_id</code></td><td><code>string</code></td><td>Unique identifier for the campaign.</td></tr><tr><td><code>campaign_name</code></td><td><code>string</code></td><td>Campaign display name</td></tr><tr><td><code>start_time</code></td><td><code>uint64</code></td><td>Campaign start timestamp.</td></tr><tr><td><code>end_time</code></td><td><code>uint64</code></td><td>Campaign end timestamp.</td></tr><tr><td><code>reward_info</code></td><td><code>RewardInfo</code></td><td>Details about the reward token and amount. See <code>RewardInfo</code> below.</td></tr><tr><td><code>last_reward_attestation_time</code></td><td><code>uint64</code></td><td>Last campaign reward attestation timestamp.</td></tr><tr><td><code>status</code></td><td><code>CampaignStatus</code></td><td>Current status of the campaign. See <code>CampaignStatus</code> enum.</td></tr></tbody></table>

`RewardInfo` **Fields**

<table><thead><tr><th width="218.54296875">Field</th><th width="118.79296875">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>submission_chain_id</code></td><td><code>uint64</code></td><td>Campaign reward submission chain ID (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details).</td></tr><tr><td><code>submission_contract</code></td><td><code>string</code></td><td>Campaign reward submission contract address (see <a href="../read-and-claim-rewards.md">on-chain reward claim</a> for details)</td></tr><tr><td><code>claim_chain_id</code></td><td><code>uint64</code></td><td>Chain ID where rewards can be claimed.</td></tr><tr><td><code>claim_contract</code></td><td><code>string</code></td><td>Reward claim contract address.</td></tr><tr><td><code>token_address</code></td><td><code>string</code></td><td>Reward token address.</td></tr><tr><td><code>token_symbol</code></td><td><code>string</code></td><td>Reward token symbol.</td></tr><tr><td><code>reward_amt</code></td><td><code>string</code></td><td>Reward amount.</td></tr><tr><td><code>reward_usd_price</code></td><td><code>string</code></td><td>USD price for the reward token.</td></tr><tr><td><code>reward_per_hour</code></td><td><code>string</code></td><td>Reward amount distributed per hour.</td></tr><tr><td><code>apr</code></td><td><code>float</code></td><td>The APR of the campaign (for example, 0.03 means 3% APR)</td></tr><tr><td><code>tvl</code></td><td><code>float</code></td><td>The supply/borrow USD value of the vault</td></tr></tbody></table>

### Post Example (curl)

{% code title="data.json" %}
```json
{
    "chain_id": [
        1,
        42161
    ],
    "vault_address": [
        "0xF037eeEBA7729c39114B9711c75FbccCa4A343C8"
    ],
    "campaign_id": [

    ],
    "status": [
        4
    ],
    "user_address": [],
    "action": [
        2001,
        2002
    ]
}
```
{% endcode %}

post with `data.json`:

```sh
curl -X POST -H "Content-Type: application/json" -d @data.json POST https://incentra-prd.brevis.network/sdk/v1/eulerCampaigns
```
