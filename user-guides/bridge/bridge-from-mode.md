---
description: Bridging ETH from Mode to Ethereum
---

# ⬅️ Bridge from Mode

Mode's bridge is a fork of Optimism's canonical bridge. With Optimism's Bedrock upgrade, a two-step withdrawal process designed to enhance the safety and integrity of cross-chain transactions was introduced.

{% hint style="info" %}
You can check the status of your withdrawal in the [Transactions](https://app.mode.network/transactions/) section.\
\
The 7 day withdrawal period is due to how optimistic rollups work, it's called the challenge period. Read more about it [here](https://docs.optimism.io/builders/app-developers/bridging/messaging)
{% endhint %}

<details>

<summary>1 - Bridge to Ethereum</summary>

First, go to [Mode's Bridge](https://app.mode.network/), click on **`Switch`** and select the token and input the amount you want to withdraw.

Click on <mark style="color:purple;">**`Review Withdrawal`**</mark> , then check the 7 days checkbox and initiate the withdrawal.

You can see the transaction status of your withdrwal in the [<mark style="color:purple;">**`Transactions`**</mark>](https://app.mode.network/transactions/) section

![](<../../.gitbook/assets/image (20).png>)

**Please wait up to 1 hour until the status of your tx is ready to prove.**

</details>

{% hint style="danger" %}
The steps to Prove and Finalize withdrawals are executed on Ethereum Mainnet. You will need ETH on Ethereum Mainnet to pay for these fees. This is also why these fees may seem high.\
\
Make sure you have ETH on Ethereum to pay for gas.
{% endhint %}

<details>

<summary>2 - Prove Withdrawal</summary>

After waiting for 1 hour, your transaction should be ready to "Prove withdrawal".

<img src="../../.gitbook/assets/image (18) (1).png" alt="" data-size="original">\
\
Now click <mark style="color:purple;">**`Prove`**</mark> and submit the transaction, this will start the[ 7 day waiting period for the withdrawal.](#user-content-fn-1)[^1]

</details>

<details>

<summary>3 - Finalize Withdrawals</summary>

After proving the transaction you will have to wait 7 days until the status of the transaction is ready to finalise.\
\
![](<../../.gitbook/assets/image (21).png>)\
\
You can now click <mark style="color:purple;">**`Claim`**</mark> and after approving the transcation you should see the funds in your wallet on the Ethereum network shortly.\
\
The fees paid here are on Ethereum network.

</details>

[^1]: The waiting period will only start counting after proving the withdrawal.
