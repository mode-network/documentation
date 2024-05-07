---
description: How to register a smart contract on Mode’s SFS register contract.
---

# SFS - Registering a contract with Remix

This tutorial will teach you about the SFS (Sequencer Fee Sharing) contract and how to register a newly deployed contract.&#x20;

if you want to go straight to the code examples go to [#sample-smart-contract](sfs-registering-a-contract-with-remix.md#sample-smart-contract "mention").

### Introducing SFS (Sequencer Fee Sharing)

Developers can earn a share of the network Sequencer fees by registering their contracts in the Fee Sharing Contract (based on Canto's Turnstile.sol) deployed at [0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=txs) on Mode testnet. A portion of transaction fees of all transactions involving their smart contract will accumulate in the Fee Sharing Contract.

When registering your contract, the registry contract issues an NFT as a claim to the earned fees by the recipient specified in the call to register the smart contract. This means your smart contract needs to make the call to the SFS contract in order to register. The minted NFT is transferable and can be used to claim fees for multiple contracts.&#x20;

An offchain component will process the transactions for each smart contract to calculate it's share of fees. This component will also distribute the fees to registered smart contracts in the SFS contract. Note that there may be a lockup period on withdrawal of distributed funds for up to 2 weeks.\
You can see the code of the SFS contract [here](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=contract). If you are a little bit familiar solidity, we would recommend you to take a look at the “register” function. We'll go over it later in this tutorial.

Now that we know what the SFS registry is, let’s register a sample smart contract to start earning fees.

### SFS register function review

Let’s take a quick look at the SFS contract. More specifically, the register function. There are 2 interesting things to note from this function. The first one is that the parameter the function receives (<mark style="color:orange;">`address`</mark>` ``_recipient`) is the address of the recipient of the earned fees. The second one is that, to know what smart contract is being registered, the SFS contract looks at the msg.sender. This is why you need to call this register function from the contract you want to register. You can only register your contract once.

```sol
    /// @notice Mints ownership NFT that allows the owner to collect fees earned by the smart contract.
    ///         `msg.sender` is assumed to be a smart contract that earns fees. Only smart contract itself
    ///         can register a fee receipient.
    /// @param _recipient recipient of the ownership NFT
    /// @return tokenId of the ownership NFT that collects fees
    function register(address _recipient) public onlyUnregistered returns (uint256 tokenId) {
        address smartContract = msg.sender;

        if (_recipient == address(0)) revert InvalidRecipient();

        tokenId = _tokenIdTracker.current();
        _mint(_recipient, tokenId);
        _tokenIdTracker.increment();

        emit Register(smartContract, _recipient, tokenId);

        feeRecipient[smartContract] = NftData({
            tokenId: tokenId,
            registered: true,
            balanceUpdatedBlock: block.number
        });
    }
```

For this tutorial, we will be using Remix to deploy and interact with the contracts, but you can deploy with any tools you prefer.

### Sample smart contract

This is a basic [ERC-20](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v5.0.0/contracts/token/ERC20/ERC20.sol) token using the [OpenZepellin](https://docs.openzeppelin.com/contracts/4.x/erc20) contract. In the example code snippet below, you will find a Register contract with the signature of the register function following the SFS contract.

We will be using the tesnet SFS address, but if you want to register a contract on Mainnet, you should change the address on line 19.\
\
Mainnet SFS Address: [0x8680CEaBcb9b56913c519c069Add6Bc3494B7020](https://explorer.mode.network/address/0x8680CEaBcb9b56913c519c069Add6Bc3494B7020?tab=txs)\
Testnet SFS Address: [0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6)

{% hint style="info" %}
<mark style="color:yellow;">**IMPORTANT:**</mark> In order to register your smart contract in the SFS, it’s mandatory to have a call to the register function in your smart contract. This call needs to be made from your contract.
{% endhint %}

{% code lineNumbers="true" %}
```solidity
// SPDX-License-Identifier: GPL-3.0

pragma solidity ^0.8.20;

import "https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v5.0.0/contracts/token/ERC20/ERC20.sol";


interface ISFS {
    function register(address _recipient) external returns (uint256 tokenId);
}

contract ModeToken is ERC20 {

    address feeReceiver = msg.sender;
    
    constructor() ERC20("ModeTokenSFSTest", "SFST2") {
        _mint(msg.sender, 1000 * 10 ** 18); //Example amount to mint our ERC20
        feeReceiver = msg.sender; //The deployer of the contract will get the NFTto widthraw the earned fees
        ISFS sfsContract = ISFS(0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6); // This address is the address of the SFS contract
        sfsContract.register(msg.sender); //Registers this contract and assigns the NFT to the owner of this contract
    }
}
```
{% endcode %}

In this case, our <mark style="color:purple;">`constructor()`</mark> creates an instance of the Register contract using the SFS contract address passed as an argument and then calls the register function in the SFS contract, passing the <mark style="color:orange;">`msg.sender`</mark> as parameter.&#x20;

That’s all we need to add to our smart contract to register it! The contract will register itself on deployment, so let's go do that.

### Deploying and registering the contract

We will be using Remix, so we'll go to the deploy tab and use the “Injected Provider - Metamask” to connect Metamask and deploy our contract. Please make sure in the compiler’s tab that the EVM version is set to london or else you'll get a <mark style="color:orange;">`PUSH0`</mark> error message.

{% hint style="warning" %}
With Remix, is important that you pay attention to which network you are connected. In this case we are using Mode's testnet but the same process applies for Mainnet.
{% endhint %}

<img src="https://lh5.googleusercontent.com/UuqgaKWhd4ZTVVhd4GTyEq-Fy6Qnd7YXR4WDT4YMtx8pLEfGtbOoUEZ7lqHTMfdjTeLsx0bN798XLOC2BV0MLmDkIz-MSVd-CelSmiBxMkmuJyZ1h-LMBERcDuWxU1oesscYg9dcrzsHDsui3hAWWok" alt="" data-size="original"><img src="https://lh3.googleusercontent.com/wPmRh3XEuQcqeT17Kwi_nOpgwAMSvoazjCkl-iaTFq4sJfPXLQKsH5S4LpRVvN6hsxWiOxRICQwGhHYdR5p60h8DmiOGCxX_cG51g0jzLM6UGYWT3QEyhFrIDB14tNT2HugPIg9XP9CwjKA89xBaUlM" alt="" data-size="original">

After deploying and confirming the transaction in Metamask that’s it! \
\
If the transaction was successful, your contract should be registered and your wallet should have the SFS NFT minted. This NFT is the one that allows you to claim your rewards.

To validate if the registration was done correctly check our [check-the-sfs-registry.md](../check-the-sfs-registry.md "mention") tutorial.\
\
To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋\
