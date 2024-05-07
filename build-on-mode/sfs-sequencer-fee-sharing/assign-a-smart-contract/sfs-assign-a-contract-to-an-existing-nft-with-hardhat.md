# SFS - Assign a contract to an existing NFT with Hardhat

Hardhat is an Ethereum development environment offering tools for smart contract development, and deployment. It supports Solidity, features a testing framework, and allows task automation. With a modular architecture and extensive plugin support,

In this tutorial, you’ll learn how to register our smart contract to the [Mode SFS contract](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6) by assigning our contract to an existing SFS NFT.

### Prerequisites

Before you continue with this tutorial you should have:

* [npm](https://www.npmjs.com/) and [node.js](https://nodejs.org/en) installed.
* Ethereum wallet preferably [Metamask](https://metamask.io/) Installed.
* Basic understanding of [Solidity](https://soliditylang.org/).
* &#x20;Sepolia Eth with Mode Network.
* An SFS NFT token Id.

### What is SFS(Sequencer fee sharing)

Mode’s SFS is one of the primary features of the Mode network, it lets developers get some percentage of the transaction fees from their contracts' activities on the Mode network. For this to work, your smart contract has to be registered to Mode’s SFS contract. Once registered, you get an ERC 721 NFT (Non-Fungible Token) which allows you to claim your share of the transaction fees generated from your contract.

The SFS NFT is transferable and can be used to claim rewards for more than one contract, so you can either get a new NFT for multiple smart contracts deployed on Mode, or you can assign multiple smart contracts to an already existing SFS NFT; which is what we’ll be learning about in this tutorial.

You can explore the full SFS contract code [here](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=contract).

### Assigning smart contract to an existing SFS NFT

Let’s take a look at the <mark style="color:purple;">assign</mark> function in the SFS contract to understand how the assigning works.

Note that this is only a portion of the SFS contract, [check here](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=contract) to see the complete code.



```solidity
function assign(uint256 _tokenId) public onlyUnregistered returns (uint256) {
       address smartContract = msg.sender;


       if (!_exists(_tokenId)) revert InvalidTokenId();


       emit Assign(smartContract, _tokenId);


       feeRecipient[smartContract] = NftData({
           tokenId: _tokenId,
           registered: true,
           balanceUpdatedBlock: block.number
       });


       return _tokenId;
   }
```

This function receives <mark style="color:purple;">\_tokenId</mark> as an input param. It then checks if the tokenId is valid before emitting an Assign event, after which the msg.sender (our smart contract) will be assigned to the <mark style="color:purple;">tokenId</mark> in the SFS, updating the feeRecipient mapping with relevant information.

Here are a few things to note;

* The assign function is specified public, meaning an external smart contract can call it.
* The msg.sender is assumed to be a smart contract address because this function is expected to be called by a smart contract.
* The assign function does not mint an ownership NFT, rather, it assigns your smart contract to an existing SFS NFT.
* Assigning a smart contract to an SFS NFT can only be done once.

\
Now that we’ve understood how the assign function works, let’s set up our project and build our smart contract.\


### 1. Setting up our project

Open your terminal to create a new directory for your project.

`mkdir hardhat`

Navigate into your project

`cd hardhat`

Initialize an npm project - This creates your package.json file.

`npm init -y`

Install hardhat

`npm install --save-dev hardhat`

To create your project run

`npx hardhat init`

When prompted make these selections;

* Choose "Create a TypeScript project".
* For the .gitignore prompt, select "Yes" (or y).
* Select "Yes" (or y) to install the project's dependencies.

\
![](https://lh7-us.googleusercontent.com/\_cX-4P8nGSKmwakBNlASWnGGdiQurBbrQqEC7yrEhhAgpa69gxCTXbWq0wK5HbsbX\_NaXlPMZTy7R7cRW2EUfBtkF1GDKg3iGotPfsW2BwcFS0Q7oA7DyQQ5lRHSiv2aBNIgm\_iS0FVaTN3vhfBInEg)

### 2. Writing our smart contract

Head over to the contracts folder of your project, for the sake of this tutorial we will be making use of the Lock contract provided by Hardhat, and we’ll be making some modifications to it.

First, we added the SFS contract to our file with a register function. Then in the constructor, we invoked the assign function by initializing a new instance of our SFS contract and calling the assign method on it.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;


//Here we created our SFS contract
contract SFS {
   function assign(uint256 _tokenId) public returns (uint256) {}
}


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
    	// Initialize an instance of the SFS contract
	// Note: Here we passed in the testnet SFS contact address as param
       SFS sfsContract = SFS(0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6);
	// Call the assign function with our NFT token Id as param
        // I used 45 as our token Id, you should change it your own token ID 
       sfsContract.assign(45);
   }


   function withdraw() public {
       require(block.timestamp >= unlockTime, "You can't withdraw yet");
       require(msg.sender == owner, "You aren't the owner");
       emit Withdrawal(address(this).balance, block.timestamp);
       owner.transfer(address(this).balance);
   }
}
```

Mode SFS contact has a different address for Mainnet and Testnet and for this tutorial, we’re deploying to Testnet so we’re going to register to the Testnet’s SFS contract.

Mainnet SFS Address:[ 0x8680CEaBcb9b56913c519c069Add6Bc3494B7020](https://explorer.mode.network/address/0x8680CEaBcb9b56913c519c069Add6Bc3494B7020?tab=txs)&#x20;

Testnet SFS Address:[ 0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6)

### 3. Configuring harhat for Mode

Head to the hardhat.config.ts file and replace it with this code to set Mode Network Testnet. Remember to change the account's value to your Metamask private key.

```tsconfig
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

{% hint style="info" %}
For deploying on Mainnet replace the url and chainId to:

url: [https://mainnet.mode.network/](https://mainnet.mode.network/)

chainId: 34443
{% endhint %}



### 4. Compiling our smart contract

To compile the smart contract run

**npx hardhat compile**

It would return;

**Successfully generated 8 typings!**

**Compiled 1 Solidity file successfully (evm target: london).**

### 5. Deploying

To deploy we will make use of the deploy.ts file in the scripts folder, we won’t be changing anything because we didn’t change our smart contract.

To deploy the smart contract to Mode Testnet run

**npx hardhat run scripts/deploy.ts --network mode**

It returns

**Lock with 0.001ETH and unlock timestamp 1702421602 deployed to 0x6900B6158C1BD0C61G1E6a191B1f822EA000E2e8**&#x20;

Congratulations! You just deployed and registered your contract with Hardhat and Typescript.

### Check the Explorer

To view your transaction head to [Mode Testnet](https://sepolia.explorer.mode.network/) and paste the contract address.

Your contract should be assigned to the NFT tokenId. To verify if you assigned your contract correctly, you can check our [“Check the registry”](https://docs.mode.network/build-on-mode/tutorials/sfs-sequencer-fee-sharing/sfs-check-the-registry) guide.\
To import the NFT to your wallet, check our [Adding the SFS NFT to your wallet](https://docs.mode.network/build-on-mode/tutorials/sfs-sequencer-fee-sharing/sfs-check-the-registry#adding-the-sfs-nft-to-your-wallet) tutorial.\


