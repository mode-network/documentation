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

## Step-By-Step How to Withdraw:

<details>

<summary>1 - Bridge to Ethereum</summary>

First, go to [Mode's Bridge](https://app.mode.network/), click on **`Switch`** and select the token and input the amount you want to withdraw.&#x20;

Click on <mark style="color:purple;">**`Review Withdrawal`**</mark> , then check the 7 days checkbox and initiate the withdrawal.&#x20;

If you click on <mark style="color:purple;">**`Transaccions`**</mark> on the top right of the page you can check the status of your transaction.

![](<../../.gitbook/assets/image (20).png>)

**Please wait up to 1 hour until the status of your tx is ready to prove.**

</details>

{% hint style="danger" %}
The steps to Prove and Finalize withdrawals are executed on Ethereum Mainnet. You will need ETH on Ethereum Mainnet to pay for these fees. This is also why these fees may seem high.\
\
Make sure you have ETH on Ethereum to pay for gas.
{% endhint %}

<details>

<summary>2 - Prove Withdrawal </summary>

After waiting for 1 hour, your transaction should be ready to "Prove withdrawal".

<img src="../../.gitbook/assets/image (19).png" alt="" data-size="original">\
\
Now click <mark style="color:purple;">**`Prove`**</mark> and submit the transaction, this will start the[ 7 day waiting period for the withdrawal.](#user-content-fn-1)[^1]&#x20;

</details>

<details>

<summary>3 - Finalize Withdrawals</summary>

After proving the transaction you will have to wait 7 days until the status of the transaction is ready to finalise.\
\
![](<../../.gitbook/assets/image (21).png>) \
\
You can now  click <mark style="color:purple;">**`Claim`**</mark> and after approving the transcation you should see the funds in your wallet on the Ethereum network shortly. \
\
The fees paid here are on Ethereum network.

</details>

### Understanding the Bridge Interface

<figure><img src="../../.gitbook/assets/Pasted Graphic 3 copy.png" alt=""><figcaption></figcaption></figure>

1. <mark style="color:red;">**Transactions:**</mark> This button takes you to the pending withdrawals you started. If you started a withdrawal your transaction should be shown here until it's finalized.
2. <mark style="color:red;">**Switch:**</mark> This button switches the "From" and "To". It's the switch to deposit or withdraw from Mode.
3. <mark style="color:red;">**Estimated Gas Fees:**</mark> These is the estimated gas fees are what Mode estimates you will spend.
4. <mark style="color:red;">**Switch Network:**</mark> If you are seeing this button, it means your wallet is set to the incorrect chain. Clicking it will ask you to change chains from Mode to Ethereum or viceversa.



[^1]: The waiting period will only start counting after proving the withdrawal.
