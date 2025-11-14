
# Campaign Rules

## Common Rules

Below is the description of rules that apply to all campaign types.

### Epoch

All users' rewards are attested and updated periodically. The current period is 4 hours. Users might see their rewards updated slightly longer (e.g., 30 minutes) than 4 hours due to the time to generate ZK proofs for users' rewards.

Also, for the 1st epoch after the campaign starts, it may take significantly more time (4 to 12 hours) to update the rewards due to the time to index and fetch relevant historical on-chain data (events, storage, transactions).

In some rare cases (e.g., there is a spike in campaign participants), the rewards update delay may be significantly longer than 4 hours as we expand system capacity and resolve the issues. Rest assured that the rewards in the delayed epochs will still be proved.

### Dust Rewards

For each epoch, if a user's rewards < $0.0001 in the epoch, the user's rewards won't be attested for the epoch.

## Reward Rules for Each Campaign Types

### Concentrated Liquidity Campaign

In a concentrated liquidity campaign, each liquidity provider (LP) is allocated rewards proportional to the fees earned:

_LP campaign reward in an epoch = fees earned by LP in the epoch / total fees earned by all LPs in the epoch \* total campaign rewards in the epoch \* (100% - campaign fee)_&#x20;

Here, _campaign fee_ is the percentage of fees charged by the Incentra platform.

NOTE: If there is no swap during an epoch, this epoch will be skipped and no LPs will get rewards for this empty epoch.

### Token Holding Campaign

In a token holding campaign, each token holder is allocated rewards proportional to the Time-Weighted Averaged (TWA) token balance in the epoch:

_user campaign reward in an epoch = TWA of the user in the epoch / sum of TWAs of all users in the epoch \* total campaign rewards in the epoch \* (100% - campaign fee)_

Here, _campaign fee_ is the percentage of fees charged by the Incentra platform.

NOTE: A user needs to directly hold the token in the wallet to receive the campaign rewards unless explicitly specified (e.g., if specified, staking the token into a staking contract may also earn rewards even if the token is not directly held in the wallet).

### Lend/Borrow Campaign (Euler)

In an Euler supply campaign, each supplier is allocated rewards proportional to the Time-Weighted Averaged (TWA) eToken balance for the vault in the epoch:

_user campaign reward in an epoch = eToken TWA of the user in the epoch / sum of eToken TWAs of all users in the epoch \* total campaign rewards in the epoch \* (1 - campaign fee)_

Here, _campaign fee_ is the percentage of fees charged by the Incentra platform.

In an Euler borrow campaign, each borrower is allocated rewards proportional to the average debt (dToken balance) for t he vault in the epoch:

_user campaign reward in an epoch = user's average debt in the epoch / sum of average debts of all users in the epoch \* total campaign rewards in the epoch \* (100% - campaign fee)_

The average debt is calculated using samples at random points of time every 10 minutes in order to accommodate the increasing debt due to interests.

**NOTE**: If the user has multiple sub-accounts, the owner account will receive the rewards for all its sub-accounts.
