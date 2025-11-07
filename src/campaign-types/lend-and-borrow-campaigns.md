
# Lend and Borrow Campaigns

Incentra supports lending and borrowing protocols to reward users for supplying collateral in a vault or borrowing from a vault.

### Lend/Borrow Campaigns for Euler Finance

* In lending campaigns, rewards are allocated based on each user’s share of the total time-weighted average (TWA) balances of the corresponding eToken among all eligible users.
* In borrowing campaigns, rewards are allocated proportionally to each user’s share of the average debt within the vault. To accommodate the increasing debt due to interests,  each user's averaged debt is calculated using samples at random points of time spacing around 10 minutes.

Brevis fetches eToken and debt data directly from the blockchain, periodically updates balances for all eligible users, calculates individual rewards, and generates zero-knowledge proofs (ZKPs) to ensure the correctness of these calculations. These ZKPs are verified on-chain and the results will be utilized by the rewards distribution contracts to distribute rewards accordingly.

**NOTE**: If the user has multiple sub-accounts, the owner account will receive the rewards for all its sub-accounts.

**NOTE**: The underlying asset token of a vault needs to be whitelisted first before the vault can be used in a campaign. Please contact us if you’d like to whitelist an asset token that isn’t currently available.
