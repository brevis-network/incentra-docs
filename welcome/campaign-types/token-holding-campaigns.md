---
description: Token holders are rewarded based on the TWA balance of a ERC-20 token
---

# Token Holding Campaigns

For a token holding campaign on Incentra, users earn rewards based on the time-weighted average (TWA) balance of a specified ERC-20 token. Rewards are distributed proportionally to each user’s share of the total TWA balances among all eligible users.

By retrieving and calculating token holding data directly from the blockchain, Brevis periodically updates the reward data for all eligible token holders, calculates individual reward allocations, and generates ZK Proofs (ZKPs) to validate the results. These verified results are then utilized by the reward distribution smart contracts to allocate rewards to each individual holder.

The entire process is fully transparent and trustless, allowing users to independently verify their reward amounts through ZKPs while eliminating the need for manual intervention or reliance on a potentially fallible centralized party.

Incentra also provides flexibility through additional features:

* Blacklist: Incentive providers can exclude specific addresses from receiving rewards.
* Staking: Users who stake their tokens in external contracts (such as staking LP tokens in gauge contracts) can still receive rewards.

Note that only a selected list of whitelisted ERC-20 tokens and reward tokens are supported. Please contact us if you’d like to whitelist a token that isn’t currently available.
