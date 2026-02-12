---
description: Create and manage a lend or borrow campaign
---

# Lend and Borrow Campaign

Click “Create a new campaign” to create a campaign, and select the Campaign Type you would like to create.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-15 at 17.00.53.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-05-18 at 17.35.29.png" alt=""><figcaption></figcaption></figure>

Select the lending protocol (Euler/Aave/Morpho) to be incentivized.

<figure><img src="../.gitbook/assets/Screenshot 2026-02-12 at 23.52.47 (1).png" alt=""><figcaption></figcaption></figure>

To create a Euler campaign, you need to configure the following info:

* Campaign Name
* Action: the action you would like to incentivize - supply to a vault or borrow from a vault
* Vault Info: select the chain where the vault is deployed and enter the vault address. The vault information should be displayed automatically. You may also enter the vault name if this is the first time setting up a campaign for this vault

<figure><img src="../.gitbook/assets/Screenshot 2025-05-18 at 18.09.35.png" alt=""><figcaption></figcaption></figure>

To create an Aave campaign, you need to configure the following info:

* Campaign Name
* Action: the action you would like to incentivize - supply to a pool or borrow from a pool. For a lending campaign, enabling net lending is optional if you would like to set up a net lending campaign and users will only receive rewards based on their net position values in the pool
* Pool Info: select the chain where the pool is deployed and enter the aToken address. The pool information should be displayed automatically. You may also enter the pool name if this is the first time setting up a campaign for this pool

<figure><img src="../.gitbook/assets/Screenshot 2026-02-13 at 00.02.34.png" alt=""><figcaption></figcaption></figure>

To create a Morpho campaign, you need to configure the following info:

* Campaign Name
* Action: the action you would like to incentivize - supply to a vault. Only lend campaign is currently supported for Morpho
* Vault Info: select the chain where the vault is deployed and enter the vault address. The vault information should be displayed automatically. You may also enter the vault name if this is the first time setting up a campaign for this vault

<figure><img src="../.gitbook/assets/Screenshot 2026-02-13 at 00.10.11.png" alt=""><figcaption></figcaption></figure>

The following parameters may also need to be configured for Euler, Aave, and Morpho campaigns:

* Campaign Start Time and End Time: select the start time and end time, you could also select to set a 7-day/14-day/30-day/90-day campaign and the campaign end time will be displayed automatically
* Blacklist Address List: it is optional to exclude specific addresses from receiving rewards
* Select Reward Token: select the token you would like to use as a reward token and enter the total rewards amount. Only a selected list of reward tokens is supported. Please contact us if you’d like to whitelist a token that isn’t currently available
* URL: enter the URL of the dApp where users could supply or borrow

Once all the required information is provided, you can click the ‘Create Campaign’ button to confirm the campaign settings.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-18 at 18.09.20.png" alt=""><figcaption></figcaption></figure>

Please review and confirm your campaign settings before launching the campaign as the configs cannot be changed after creation.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.10.44.png" alt=""><figcaption></figcaption></figure>

Once the campaign settings are submitted, the campaign will be created.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.11.37 (1).png" alt=""><figcaption></figcaption></figure>

You would see a pop-up with a campaign ID and view the campaign creation tx hash in explorer, confirming that your campaign has been successfully created.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.11.50.png" alt=""><figcaption></figcaption></figure>

You may also see the campaign creation is failed or campaign is creating, and could retry the campaign creation in the campaign page.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-18 at 18.03.23.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
To deposit rewards, you may also directly transfer reward tokens to the campaign contract via a simple ERC-20 transfer from a different address (e.g., a multi-sig) later.
{% endhint %}

Once the campaign is created, please deposit the rewards into the reward contract to enable reward distribution. You may deposit rewards while the campaign is to be started, active, or even ended. By default, the total rewards amount should be deposited.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.12.24.png" alt=""><figcaption></figcaption></figure>

Once the reward tokens are deposited, congratulations — you’re all set!

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.12.55.png" alt=""><figcaption></figcaption></figure>
