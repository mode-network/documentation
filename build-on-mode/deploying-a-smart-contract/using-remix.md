---
description: How to deploy with Remix IDE on MODE
---

# Using Remix

Mode is an OP Stack Layer-2 designed for hyper-growth. Since MODE is built with the OP Stack, it is EVM compatible, allowing you to easily port your existing Ethereum-based smart contracts without modifying the code.

Let’s see how to deploy a smart contract on MODE using the [Remix IDE](https://remix.ethereum.org).

{% hint style="info" %}
This guide assumes you have got Sepolia ETH and bridged to the Mode Testnet Network.&#x20;
{% endhint %}

## 1. Deploy using Remix

First of all you will need to have Mode network added to your Metamask. Follow [using-mode-testnet.md](../../mode-testnet/using-mode-testnet.md "mention") for the step-by-step on how to add Mode testnet to Metamask.

We are ready to get started!

[Remix](https://remix.ethereum.org) is a no-setup tool with a graphical interface for developing smart contracts. It’s easy to get started allowing a simple deployment process, debugging, interacting with smart contracts, and more. It’s a great tool to test quick changes and interact with deployed smart contracts.

<figure><img src="https://lh4.googleusercontent.com/AdHTInVXjMKYbUPeok0GuLdiZDDTsdxodDjApKYvJ-kEfqQ2dbgEwp1dHhveeYi0m1VkiW6wnBJV_1Tnn4S4JR6KIvuQGZ5eKukwsWAHxF6PsffOneea6mgZzh_OFZThQok1DkpJmtWLkzN1oCmJEYg" alt="This is a screenshot showing Remix I D E. There is a basic smart contract that will be used for the tutorial."><figcaption></figcaption></figure>

For the sake of this tutorial, we will be deploying the ‘1\_Storage.sol’ smart contract that comes as an example in Remix, but you can use any of your code.\
\
Here is the sample code, you can paste this in any .sol file:

{% code title="1_Storage.sol" fullWidth="true" %}
```solidity
// SPDX-License-Identifier: GPL-3.0

pragma solidity >=0.8.2 <0.9.0;

contract Storage {

    uint256 number;
    
    function store(uint256 num) public {
        number = num;
    }

    function retrieve() public view returns (uint256){
        return number;
    }
}


```
{% endcode %}

To compile your smart contract, go to the Solidity Compiler tab and select the contract you want to compile. Click on "Compile", you can also enable "Auto Compile" for automatic compilation whenever you change the contract code.&#x20;

{% hint style="info" %}
Make sure to open the advanced configurations and setting the EVM version to London. This is to avoid an issue with the PUSH0 opcode. You can read more on the issue with all the Optimism chains [here](https://community.optimism.io/docs/developers/build/differences/#opcode-differences).
{% endhint %}

<div align="center">

<figure><img src="../../.gitbook/assets/image (16).png" alt="" width="371"><figcaption><p>Solidity Compiler Tab</p></figcaption></figure>

</div>

Once the smart contract is compiled successfully, switch to the "Deploy & Run Transactions" tab.

In the "Environment" dropdown menu, select "Injected Provider - MetaMask"; this will connect your MetaMask to Remix and will allow you to make transactions from that connected wallet.&#x20;

{% hint style="info" %}
Make sure to have Mode as your selected network in Metamask before deploying
{% endhint %}

&#x20;\
![](https://lh4.googleusercontent.com/jmsucoJ4vr4ByW3\_0Nt4gwlckzu78pvh7ugVp2nEep9z9LtpY-BuC5WmhX4k\_uKk2vA\_iIvDZg-VEn8YDzKdoSzmE327wjbLiCIpCGe9xc\_GAxBOC5-LYet-qBNPQ54W5waFpeMZak61a-rmk\_ITxog)                   ![](https://lh6.googleusercontent.com/nIYOD8FEnw-1qCtgMI\_uKK4qRwEjciveycdc3q6iLtuW7su7sOQMZHhG1dw8Rwk2ulO4JFlQU8YxQlJIB8c6uMZJ5t19PCikrkIKVsRZW68PVRz8RVs1NtQOxrQ6x7CwZXtwjlv6W4Fe9x45\_44LWSQ)

Select the compiled contract you want to deploy and click ‘Deploy.’&#x20;

Now, MetaMask should pop up and ask you to confirm the transaction with super low fees.&#x20;

<figure><img src="https://lh4.googleusercontent.com/u2Y8C7HIZLdoXt_3UW_bEGSj8fI0oRCoWsvLDfJaHjzviK7ucJKzrCgh8Qiw4OD7Zj8EK3-KGCK7H2fXn5Am5iUbDKHoD44ZDZkHUqC2R8UQmbkvStnjWNMMM9EwDcp_Sgl9Ml-ONlK8wCE0T21wEqo" alt="This image shows a screenshot of Metamask wallet with the transaction to deploy the smart contract. It shows very low fees of around 0.35 dollars or 0.00018852 ETH." width="375"><figcaption></figcaption></figure>



**CONGRATULATIONS! You just deployed your first smart contract to Mode.**

***

### 2. How to explore and interact with your deployed smart contract?

Now that you have deployed your first smart contract to Mode let’s see how to interact with it.&#x20;

You will see your deployed smart contract below in the ‘Deploy & Run Transactions’ tab. You can use the Remix interface to call the methods defined in your smart contract and access it’s public variables.&#x20;

We can also find our deployed smart contract in [Blockscout](https://sepolia.explorer.mode.network/), the Mode block scanner.  Copy the contract address from Remix, go to [Blockscout](https://sepolia.explorer.mode.network/), and paste it into the search bar.

<figure><img src="https://lh5.googleusercontent.com/vNj7xV8ITJhBVEVimTgm6OBRU-9YPTreXCc78v8uoTPMgGQtw6BBBXWwDXZVkC_ZeIrHL5d2ko0a1KS6aSSG6LVidwKgobsQRJuujwjRmeGJG9Aj8ng1mMCiKCN9cdqPjPOLDLlYIL8m5ReZnoNrcXw" alt="" width="375"><figcaption></figcaption></figure>

The screenshot below shows our deployed smart contract, where you can see all transactions, the creator wallet, balance, and more!

Notice that if you call one of the smart contract methods in Remix, you should see the transaction pop up in this explorer. You can directly interact with your deployed smart contract with Remix.

<figure><img src="https://lh5.googleusercontent.com/8ZHx1tXtti3mgDFF8up5unacb3aiFwa5xxI6N2VZOI32G0kXC8XmAFTLeF3im4vHYUiVsM5pYsPKy13pCo-GwiJSTgVFZuRwwml9a8uBWAOE7BADWzE27FuXvOEPdWbQRCYXArfJeh20LdOqamINYQE" alt=""><figcaption><p>Blockscout</p></figcaption></figure>

{% hint style="success" %}
**You now have learned how to deploy a smart contract on Mode using Remix online IDE!**&#x20;
{% endhint %}

In this tutorial, we also went through the Mode bridge, block explorer, and how to interact with your contract.&#x20;

To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋

If you want the next challenge, you can try registering a contract for the SFS following this guide: [sfs-registering-a-contract-with-remix.md](../sfs-sequencer-fee-sharing/register-a-smart-contract/sfs-registering-a-contract-with-remix.md "mention")

\
