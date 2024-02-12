# 🕐 Quick start

In this section we'll get you deploying a sample contract on Mode in less than 10 minutes.\
\
Let’s see how to deploy a smart contract on Mode using the [Remix IDE](https://remix.ethereum.org) for simplicity.

## Get everything ready

Before getting started:

1. Follow [using-mode-testnet.md](../mode-testnet/using-mode-testnet.md "mention") for the step-by-step on how to add Mode testnet to [Metamask](https://metamask.io/download/).
2. This guide assumes you have got Sepolia ETH and bridged to the Mode Testnet Network. Learn how to do that in [testnet-faucets.md](../tools/testnet-faucets.md "mention")

We are ready to get started!

## Remix & Sample Code

[Remix](https://remix.ethereum.org) is a no-setup tool for developing smart contracts. It’s easy to get started allowing a simple deployment process, debugging, interacting with smart contracts, and more. It’s a great tool to test quick changes and interact with deployed smart contracts.

<figure><img src="https://lh4.googleusercontent.com/AdHTInVXjMKYbUPeok0GuLdiZDDTsdxodDjApKYvJ-kEfqQ2dbgEwp1dHhveeYi0m1VkiW6wnBJV_1Tnn4S4JR6KIvuQGZ5eKukwsWAHxF6PsffOneea6mgZzh_OFZThQok1DkpJmtWLkzN1oCmJEYg" alt="This is a screenshot showing Remix I D E. There is a basic smart contract that will be used for the tutorial."><figcaption></figcaption></figure>

For the sake of this tutorial, we will be deploying the ‘1\_Storage.sol’ smart contract that comes as an example in Remix, but you can use any of your code.

We added a few lines of code to register this contract on the SFS. You can copy and then paste this in Remix or use your own contract code.\
\
Here's the sample code:

{% code title="1_Storage.sol" fullWidth="true" %}
```solidity
// SPDX-License-Identifier: GPL-3.0

pragma solidity ^0.8.20;

interface Sfs {
    function register(address _recipient) external returns (uint256 tokenId);
}

contract Storage {

    uint256 number;

    constructor(){
      // This address is the address of the SFS contract on testnet
      Sfs sfsContract = Sfs(0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6); 
      // Registers this contract and assigns the NFT to the deployer of this contract
      sfsContract.register(msg.sender); 
    }
    
    function store(uint256 num) public {
        number = num;
    }

    function retrieve() public view returns (uint256){
        return number;
    }
}
```
{% endcode %}

If you know a little solidity, you must already notice something else in this contract. This contract is being registered to the SFS in the constructor. We won't go over this in depth in this tutorial, please go to [sfs-sequencer-fee-sharing](../build-on-mode/sfs-sequencer-fee-sharing/ "mention")if you want to know more about how it works.



This contract just let's you store a number and then read what that number is while also registering it in the SFS registry.\


## Steps to deploy

1. Copy the sample code and paste it in one of the .sol files in Remix
2. To compile your smart contract, go to the `Solidity Compiler tab` and select the contract you want to compile
3. Click on "Compile", you can also enable "Auto Compile" for automatic compilation whenever you change the contract code.&#x20;

{% hint style="warning" %}
Make sure to open the advanced configurations and setting the EVM version to London. This is to avoid an issue with the <mark style="color:orange;">`PUSH0`</mark> opcode. You can read more on this specification with all Optimism chains [here](https://community.optimism.io/docs/developers/build/differences/#opcode-differences).
{% endhint %}

<div align="center">

<figure><img src="../.gitbook/assets/image (16).png" alt="" width="371"><figcaption><p>Solidity Compiler Tab - correct settings</p></figcaption></figure>

</div>

4. Once the smart contract is compiled successfully, switch to the "`Deploy & Run Transactions`" tab.
5. In the "`Environment`" dropdown menu, select "`Injected Provider - MetaMask`"; this will connect your MetaMask to Remix and will allow you to make transactions from that connected wallet.&#x20;

{% hint style="info" %}
Make sure to have [Mode Testnet ](../mode-testnet/using-mode-testnet.md)as your selected network in Metamask before deploying.
{% endhint %}

&#x20;\
![](https://lh4.googleusercontent.com/jmsucoJ4vr4ByW3\_0Nt4gwlckzu78pvh7ugVp2nEep9z9LtpY-BuC5WmhX4k\_uKk2vA\_iIvDZg-VEn8YDzKdoSzmE327wjbLiCIpCGe9xc\_GAxBOC5-LYet-qBNPQ54W5waFpeMZak61a-rmk\_ITxog)                   ![](https://lh6.googleusercontent.com/nIYOD8FEnw-1qCtgMI\_uKK4qRwEjciveycdc3q6iLtuW7su7sOQMZHhG1dw8Rwk2ulO4JFlQU8YxQlJIB8c6uMZJ5t19PCikrkIKVsRZW68PVRz8RVs1NtQOxrQ6x7CwZXtwjlv6W4Fe9x45\_44LWSQ)

6. Select the compiled contract you want to deploy and click ‘Deploy.’&#x20;

Now, MetaMask should pop up and ask you to confirm the transaction with super low fees.&#x20;

<figure><img src="https://lh4.googleusercontent.com/u2Y8C7HIZLdoXt_3UW_bEGSj8fI0oRCoWsvLDfJaHjzviK7ucJKzrCgh8Qiw4OD7Zj8EK3-KGCK7H2fXn5Am5iUbDKHoD44ZDZkHUqC2R8UQmbkvStnjWNMMM9EwDcp_Sgl9Ml-ONlK8wCE0T21wEqo" alt="This image shows a screenshot of Metamask wallet with the transaction to deploy the smart contract. It shows very low fees of around 0.35 dollars or 0.00018852 ETH." width="375"><figcaption></figcaption></figure>



{% hint style="success" %}
**CONGRATULATIONS! You just deployed your first smart contract to Mode.**
{% endhint %}

If you want to learn how to interact with your recently deployed contact, check [#id-2.-how-to-explore-and-interact-with-your-deployed-smart-contract](../build-on-mode/deploying-a-smart-contract/using-remix.md#id-2.-how-to-explore-and-interact-with-your-deployed-smart-contract "mention")

Or you can read more about the [sfs-sequencer-fee-sharing](../build-on-mode/sfs-sequencer-fee-sharing/ "mention").

To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋

\
