---
description: Everything you need to launch your first campaign
---

# Getting Started

On Incentra, campaigns can be created and managed in the [Brevis Incentra Portal](https://incentra-portal.brevis.network/). Here is a checklist before you create a campaign:

* Whitelist your campaign creator address
* Whitelist the tokens relevant to your campaigns
* Check if your data source chain and reward claim chain is supported
* Contact us if there is any reward forwarding requirements

### Campaign Creator Whitelist

Before getting started, please note that **your wallet address must be whitelisted first** to create a campaign. While anyone can create a campaign through the smart contract, Incentra exclusively recognizes and processes those created by whitelisted addresses.  Please contact us to get whitelisted.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-05-15 at 17.01.27.png" alt=""><figcaption></figcaption></figure>

### Check Supported Chains

In the Brevis Incentra Portal, you will need to select the "data source chain" and the "reward claim chain". Data source chain is where your protocol is deployed and reward claim chain is where your reward token is deployed.

Please contact us if you cannot find the data source chain or the reward claim chain that suits your needs. We are happy to add for your requirements.

### Token Whitelist

All tokens need to be first whitelisted before they can be configured in the Brevis Incentra Portal, including:

* Reward token in campaign types
* Underlying asset token of an Euler vault in a Lend/Borrow campaign (Euler).
* DEX pool token 0/token 1 in a Concentrated Liquidity campaign.
* Token to be held in a Token Holding campaign

Campaign creators can contact us to whitelist the relevant tokens.

### Reward Forwarding Requirements

If your campaign requires advanced reward forwarding, please contact us for support. Common reward forwarding requirements include:

* You would like the campaign to also incentivize users who stake their tokens into a staking contract
* You would like to incentivize users who interact with your protocol with some intermediary such as Active Liquidity Management solutions (e.g., Beefy, Gamma).

### Next Steps

The following sections offer step-by-step instructions to guide you through creating different types of campaigns:

* [Create a Token Holding Campaign](token-holding-campaign.md)
* [Create a Concentrated Liquidity Campaign](concentrated-liquidity-campaign.md)
* [Create a Lend and Borrow Campaign (Euler)](lend-and-borrow-campaign-euler.md)
