---
description: Bridging ETH from Mode to Ethereum
---

# ⬅ Bridge from Mode

Mode's bridge is a fork of Optimism's canonical bridge. With Optimism's Bedrock upgrade, a two-step withdrawal process designed to enhance the safety and integrity of cross-chain transactions was introduced.

{% hint style="info" %}
We understand that the 7 days finalisation period may be inconvenient but this is a decision made by Optimism to give higher security to the bridge. Security is our number one priority.\
\
Third party bridges will be available soon to improve withdrawal times.
{% endhint %}

## The three steps to withdraw:

<details>

<summary>Bridge to Ethereum</summary>

First, go to [Mode's Bridge](https://app.mode.network/), click on **`Switch`** and select the token and input the amount you want to withdraw.&#x20;

Click on <mark style="color:purple;">**`Bridge to ethereum`**</mark> and approve the transaction.&#x20;

If you click on <mark style="color:purple;">**`Pending withdrawals`**</mark> you can check the status of your transaction.&#x20;

Your withdrawal should be in status `Submitting to L1`. &#x20;

**Please wait up to 1 hour until the status of your tx is `Submitted, ready to confirm`**

</details>

<details>

<summary>Prove Withdrawal </summary>

After waiting for 1 hour, your transaction should be in status `Submitted, ready to confirm`.\
\
Now click <mark style="color:purple;">**`Prove Withdrawals`**</mark> and submit the transaction, this will start the[ 7 day waiting period for the withdrawal.](#user-content-fn-1)[^1]

</details>

<details>

<summary>Finalize Withdrawals</summary>

After proving the transaction you will have to wait 7 days until the status of the transaction is `Ready to finalise`. \
\
You can now  click <mark style="color:purple;">**`Finalize withdrawals`**</mark> and you should see your funds on Ethereum Mainnet shortly.

</details>

## Withdrawal Status Cheatsheet

<table data-full-width="true"><thead><tr><th width="240">Status</th><th>What should I do next?</th><th>Image</th></tr></thead><tbody><tr><td><strong>Submitting to L1</strong></td><td>Wait up to 1 hour until the status changes to<br><br><code>Submitted, ready to confirm</code></td><td><img src="../../.gitbook/assets/image (3).png" alt="" data-size="original"></td></tr><tr><td><strong>Submitted, ready to confirm</strong></td><td>Click on <code>Prove Withdrawals</code> and approve the transaction in your wallet.<br><br>Wait 7 days until the status is<br><strong><code>Ready to finalise</code></strong></td><td><img src="../../.gitbook/assets/image (6).png" alt="" data-size="original"></td></tr><tr><td><strong>Ready to finalise</strong></td><td>Click on <code>Finalize withdrawals</code> to get your funds in Ethereum</td><td><img src="../../.gitbook/assets/image (9).png" alt="" data-size="original"></td></tr></tbody></table>



[^1]: The waiting period will only start counting after proving the withdrawal.
