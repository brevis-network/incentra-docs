
# Technical Architecture

The diagram below shows Incentra's high-level architecture and workflow to support a campaign.&#x20;

<img src="../.gitbook/assets/Screenshot 2025-05-02 at 4.16.53 PM.png" alt=""><figcaption></figcaption>

A campaign is divided into multiple epochs (e.g., 4 hours per epoch). Once a campaign is created, the Incentra server performs the following actions during _each epoch_:

1. Fetches blockchain data relevant to the campaign.
2. Sends the data to Brevis provers to generate rewards info and corresponding ZK proofs for all users.
3. Submit the rewards info and ZK proofs to the campaign contract to update rewards on-chain.

Users (i.e., reward earners) can claim their rewards directly from the campaign contract once the rewards info has been updated on-chain.
