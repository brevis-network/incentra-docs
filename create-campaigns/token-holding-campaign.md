---
description: Create and manage a Token Holding campaign
---

# Token Holding Campaign

Click “Create a new campaign” to create a campaign, and select the Campaign Type you would like to create.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-15 at 17.00.53.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/Screenshot 2025-05-19 at 01.03.25.png" alt=""><figcaption></figcaption></figure>

To create a Token Holding campaign, you need to config the following info:

* Campaign Name
* Protocol Name and Logo
* ERC-20 Token Info: please select the ERC-20 token you would like users to hold. Only a selected list of tokens is supported. Please contact us if you’d like to whitelist a token that isn’t currently available

<figure><img src="../.gitbook/assets/Screenshot 2025-05-19 at 01.20.39.png" alt=""><figcaption></figcaption></figure>

* Campaign Start Time and End Time: select the start time and end time, you could also select to set a 7-day/14-day/30-day/90-day campaign and the campaign end time will be displayed automatically
* Blacklist Address List: it is optional to exclude specific addresses from receiving rewards
* Select Reward Token: select the token you would like to use as a reward token and enter the total rewards amount. Only a selected list of reward tokens is supported. Please contact us if you’d like to whitelist a token that isn’t currently available
* URL: enter the URL of the dApp where users could get the ERC-20 token

Once all the required information is provided, you can click the ‘Create Campaign’ button to confirm the campaign settings.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-19 at 01.22.15.png" alt=""><figcaption></figcaption></figure>

Please review and confirm your campaign settings before launching the campaign as the configs cannot be changed after creation.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-19 at 01.23.20.png" alt=""><figcaption></figcaption></figure>

Once the campaign settings are submitted, the campaign will be created.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.11.37.png" alt=""><figcaption></figcaption></figure>

You would see a pop-up with a campaign ID and view the campaign creation tx hash in explorer, confirming that your campaign has been successfully created.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2025-05-19 at 01.23.46.png" alt=""><figcaption></figcaption></figure>

You may also see the campaign creation is failed or campaign is creating, and could retry the campaign creation in the campaign page.

{% hint style="warning" %}
To deposit rewards, you may also directly transfer reward tokens to the campaign contract via a simple ERC-20 transfer from a different address (e.g., a multi-sig) later.
{% endhint %}

Once the campaign is created, please deposit the rewards into the reward contract to enable reward distribution. You may deposit rewards while the campaign is to be started, active, or even ended. By default, the total rewards amount should be deposited.

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.12.24.png" alt=""><figcaption></figcaption></figure>

Once the reward tokens are deposited, congratulations — you’re all set!

<figure><img src="../.gitbook/assets/Screenshot 2025-05-17 at 19.12.55.png" alt=""><figcaption></figcaption></figure>
