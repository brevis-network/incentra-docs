
# Get User Leaderboard

Retrieve a CSV file that displays all the users who have rewards in the campaign and their cumulative rewards by a given Campaign ID.

### &#x20;Endpoint

```
GET  https://incentra-prd.brevis.network/sdk/v1/userRewards
```

### Example (curl)

```sh
curl https://incentra-prd.brevis.network/sdk/v1/userRewards?campaign_id=1745558044
```

**Response:**

```json
{
    "err": null,
    "url": "https://incentra-user-reward-csv.s3.us-west-2.amazonaws.com/campaign-1745985401-rewards-20250506-061050.csv"
}
```

**CSV name rule:**

```css
campaign-{campaignID}-rewards-{dateTime}.csv
```

* `campaignID`: The unique ID for a campaign
* `dateTime`: In `"YYMMDD-HHmmss"` format, UTC. For example, `20250506-151050` represents `2025-05-06 15:10:50.`

### CSV Format

The CSV including the 2 columns, User And EarnedAmount

* User: user address
* EarnedAmount: the accumulated amount of reward tokens earned by each user in the campaign

The CSV table sort in descending order by Total Rewards Earned.

