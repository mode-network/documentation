# SFS - Register a Smart Contract with Hardhat

[Hardhat](https://hardhat.org/) is an Ethereum development framework for creating, testing, and deploying smart contracts. It includes a suite of tools that aid in developing smart contracts and managing the complete development process, allowing developers to write scripts, compile, test, and deploy efficiently.

In this tutorial, you will learn how to register a smart contract to Mode Network’s SFS   (Sequencer Fee Sharing) Contract with Hardhat.

## Prerequisites

Before you continue with this tutorial you should:

* Have [npm](https://www.npmjs.com/) and [node.js](https://nodejs.org/en) installed with the recommended versions.
* Have an Ethereum wallet preferably [Metamask](https://metamask.io/) Installed.
* Have a basic understanding of [Solidity](https://soliditylang.org/).
* [Bridge](https://docs.mode.network/mode-testnet/bridging-to-mode-testnet) Sepolia Eth with Mode Network [bridging-to-mode-testnet.md](../../../general-info/bridge/bridging-to-mode-testnet.md "mention")

{% hint style="success" %}
If you want to jump straight to the code, go [here](sfs-register-a-smart-contract-with-hardhat.md#id-2.-writing-our-smart-contract)
{% endhint %}

## What is Sequencer Fee Sharing (SFS)?

The SFS contract allows developers to earn a portion of the transaction fees from transactions running on their contract when deployed and registered on Mode Network. The SFS contract implements this functionality and permits other contracts to register and earn.

To register, your smart contract has to make a call to the SFS contract, after this is done successfully, you will be issued an NFT (Non-Fungible Token). This NFT allows you to claim your fees accumulated in the SFS contract.



## How does the SFS Register function work?

Let’s look at the SFS contract's register function to understand how the registration works.

Note that this is only a portion of the SFS contract, [check here](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=contract) to see the complete code.

```solidity
function register(address _recipient) public onlyUnregistered returns (uint256 tokenId) {
   address smartContract = msg.sender;

// Check if the recipient address is valid; revert if it's null
   if (_recipient == address(0)) revert InvalidRecipient();
// Generate a unique tokenId, mint an NFT to the recipient with it, and update         //the tracker
   tokenId = _tokenIdTracker.current();
   _mint(_recipient, tokenId);
   _tokenIdTracker.increment();

   emit Register(smartContract, _recipient, tokenId);

// Update the fee recipient mapping for the smart contract, associating it with //the tokenId and registration details
   feeRecipient[smartContract] = NftData({
       tokenId: tokenId,
       registered: true,
       balanceUpdatedBlock: block.number
   });
}
```

This function receives <mark style="color:orange;">`"_recipient"`</mark> as an input and then mints an NFT to this recipient once your smart contract is registered.&#x20;

Then, the msg.sender is picked up as the contract to register in the SFS updating the mapping with relevant information.\


**Here are a few things to note:**

* The Function is specified public meaning an external smart contract can call it.
* The msg.sender is assumed to be a smart contract address, ensuring that a smart contract can register a fee recipient.
* The Function mints an ownership NFT that allows the owner to claim fees earned by the recipient smart contract.

Now that we’ve understood how the register function works, let’s set up our project.



### 1. Setting Up Our Project

Open your terminal to create a new directory for your project.

`mkdir hardhat`

Navigate into your project

`cd hardhat`

Initialize an npm project - This creates your package.json file.

`npm init -y`

`Install hardhat`

`npm install --save-dev hardhat`

To create your project run

`npx hardhat init`

**When prompted make these selections:**

* Choose "Create a TypeScript project".
* For the .gitignore prompt, select "Yes" (or y).
* For installing the project's dependencies select "Yes" (or y).

\


<figure><img src="https://lh7-us.googleusercontent.com/JClQfKJtFAdAWuAM-HT9t3946JV9hQSv-il-NtdpvkJIMDq4BgiwXpESoy0cvb2AWd5dBUPatAwpQyw-RVfVehELCtH2FrmgJfZnDT_VGU_tdI33dTTGIuusPn_HkiuezWfwDV42W-CFcr8oC-ly191Bvk7o8WdyqHkGdyphzvh8bEAJGZZXLM1ycYWmdg" alt="" width="563"><figcaption></figcaption></figure>

### 2. Writing our smart contract

Head to the contracts folder of your project, for the sake of this tutorial we will be making use of the contract provided by Hardhat.

Rename the file names lock.sol to any name of your choice then add the register contract to your file and the register function to your constructor.\


```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;
// Add this
contract Register {
   function register(address _recipient) public returns (uint256 tokenId) {}
}
//
contract Lock {
   uint public unlockTime;
   address payable public owner;
   event Withdrawal(uint amount, uint when);

   constructor(uint _unlockTime) payable {
       require(
           block.timestamp < _unlockTime,
           "Unlock time should be in the future"
       );
       unlockTime = _unlockTime;
       owner = payable(msg.sender);
    //Add this
       Register sfsContract = Register(0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6);
       sfsContract.register(msg.sender); //
   }

   function withdraw() public {
       require(block.timestamp >= unlockTime, "You can't withdraw yet");
       require(msg.sender == owner, "You aren't the owner");

       emit Withdrawal(address(this).balance, block.timestamp);

       owner.transfer(address(this).balance);
   }
}e
```

### 3. Configuring Hardhat for Mode

Head to the hardhat.config.ts file and replace it with this code to set Mode Network Testnet.

```solidity
import { HardhatUserConfig } from "hardhat/config";
import "@nomicfoundation/hardhat-toolbox";

const config: HardhatUserConfig = {
 networks: {
   mode: {
     url: "https://sepolia.mode.network",
     chainId: 919,
     accounts: ["YOUR_METAMASK_PRIVATE_KEY_HERE"] //DO NOT PUSH THIS TO GITHUB
   }
 },
 solidity: "0.8.9",
};

export default config;
```

### 4. Compiling our contract

To compile the smart contract run

`npx hardhat compile`

It would return;

`Successfully generated 8 typings!`

`Compiled 1 Solidity file successfully (evm target: london).`

{% hint style="danger" %}
It's important that the EVM version is set to london. You might get a "PUSH0" error if you don't set the evm version correctly. You can read more about this issue [here](https://docs.optimism.io/chain/differences).
{% endhint %}

### 5. Deploying

To deploy we will make use of the deploy.ts file in the scripts folder, we won’t be changing anything because we didn’t change our smart contract.

To deploy the smart contract to Mode Testnet run

`npx hardhat run scripts/deploy.ts --network mode`

It returns

`Lock with 0.001ETH and unlock timestamp 1702421602 deployed to 0x6900A6158C1BD0C61F1E6a191B1f822EA000E2e8`&#x20;

Congratulations! You just deployed and registered your contract with Hardhat and Typescript.

## Check the Explorer

To view your transaction head to [Mode Testnet](https://sepolia.explorer.mode.network/) and paste the contract address.

Your contract should be registered and your NFT minted.

To import the NFT to your wallet, check our [Adding the SFS NFT to your wallet](https://docs.mode.network/build-on-mode/tutorials/sfs-sequencer-fee-sharing/sfs-check-the-registry#adding-the-sfs-nft-to-your-wallet) tutorial.

To learn more about mode and how to turn your code into a business join our Discord and say hi.



To learn more about mode and how to turn your code into a business join our [Discord](https://discord.com/invite/modenetworkofficial) and say hi.
