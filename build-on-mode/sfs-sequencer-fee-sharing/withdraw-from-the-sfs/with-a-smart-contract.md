# With a smart contract

## **How To Withdraw funds from Mode SFS programatically.**

Mode Sequencer Fee Sharing is a feature of Mode Network that enables developers to earn a pecentage of the gas fee spent on every transaction that happens on their smart contract.

In this tutorial, you’ll learn how to withdraw funds accumulated in your Mode SFS to your wallet programmatically.

### **Prerequisites**

Before you continue with this tutorial you should:

* Have [Metamask](https://metamask.io/) Installed.
* Create a [thirdweb](https://thirdweb.com/) account.
* [Bridge](https://docs.mode.network/mode-testnet/bridging-to-mode-testnet) Sepolia Eth with Mode Network.

### **How does the SFS Withdraw function work?**

We mentioned earlier that the call to register to the SFS needs to come directly from the smart contract you want to register. To understand how this call works, let’s look at the register function.

Note that this is only a portion of the SFS contract, [check here](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=contract) to see the complete code.

```solidity
function withdraw(uint256 _tokenId, address payable _recipient, uint256 _amount)
       public
       onlyNftOwner(_tokenId)
       returns (uint256)
   {
       uint256 earnedFees = balances[_tokenId];

       if (earnedFees == 0 || _amount == 0) revert NothingToWithdraw();
       if (_amount > earnedFees) _amount = earnedFees;

       balances[_tokenId] = earnedFees - _amount;

       emit Withdraw(_tokenId, _recipient, _amount);

       Address.sendValue(_recipient, _amount);

       return _amount;
   }
```

The withdraw function enables NFT owners to claim their accumulated fees from the smart contract. It takes three parameters: the NFT's unique identifier (\_tokenId), the recipient's wallet address (\_recipient), and the amount to withdraw (\_amount).

#### Key steps and features include:

* **Verification**: Ensures that only the NFT owner can initiate the withdrawal, using the onlyNftOwner modifier.
* **Checks**: Confirms there are sufficient earned fees to withdraw and adjusts the withdrawal amount if it exceeds the available balance.
* **Balance Update:** Deducts the withdrawn amount from the NFT's total earned fees.
* **Funds Transfer:** Sends the specified amount to the recipient's address.
* **Logging:** Emits a Withdraw event with transaction details.
* **Return Value:** The function returns the actual amount withdrawn.

This function offers a secure and straightforward way for users to retrieve their fees directly to their wallets.

### **The Withdraw Function in Practice**

Now let’s take a look and an example and put our knowledge to test.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.13;

interface ISFS {
   function balances(uint256 _tokenId) external view returns (uint256);
   function withdraw(
       uint256 _tokenId,
       address payable _recipient,
       uint256 _amount
   ) external returns (uint256);
}

contract Withdraw {

   //existing code

   function callWithdrawOnFeeSharing(
       uint256 tokenId,
       address recipient,
       uint256 amount
   ) external {
       // Create an instance of the FeeSharingInterface
       ISFS feeSharingContract = ISFS(
           0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6
       );

       // Call the withdraw function
       feeSharingContract.withdraw(tokenId, payable(recipient), amount);
   }

   function checkSFSBalance() public view returns (uint256) {
       // Create an instance of the FeeSharingInterface
       ISFS feeSharingContract = ISFS(
           0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6
       );

       // Call the withdraw function
       return feeSharingContract.balances(11);
       // Replace 11 with the tokenId of the SFS NFT you want to withdraw from.
   }
}
```

We added an additional function checkBalance to help us check our balance in the SFS so we can know how to to withdraw. Remember to change the

#### Here are some things to note:

* Our code defines an interface of the withdraw and balance function.
* Our contract doesn’t show how to register or assign our contract an SFS NFT because the focus of this tutorial is to withdraw but please bear in my that you can only withdraw from a contract that has being registered and already earned fees.
* We made an instance of the SFS contract and called its withdraw function while passing the tokenId of the NFT with right to the contract we want to withdraw from, the recipient address we want to send the money to and finally the amount we want to send withdraw.

### **Deploying Our Contract to Thirdweb**

You can learn in details the step by step guide on how to deploy to Mode using thirdweb from this [article](http://link/).

### **Test**

After you’re done deploying and you have interacted with you smart contract, head over to the explorer section of your contract on thirdweb and check how much your contract has earned by running the checkBalance function.

#### Check balance

<figure><img src="../../../.gitbook/assets/SFS (1).png" alt=""><figcaption></figcaption></figure>

Now you’re sure you have a balance and you also get to know how much to withdraw if you don’t withdraw everything. Remember the unit is in Wei.

#### Withdraw

Click on the Withdraw function, enter the Token Id, the recipient address and the amount you want to send, in this case I just divided my balance into two.

Remember that your contract needs to be in possession of the NFT it is trying to claim with, so if you assigned an already existing NFT token id to your contract then you’ll also need to transfer that NFT to the contract you’re interacting with.

Click on execute!

<figure><img src="../../../.gitbook/assets/SFS Withdrawal Guide Image.png" alt=""><figcaption></figcaption></figure>

It’s going to pop up your wallet and ask you to confirm the transaction.

### Internal transaction

If your using MetaMask the contract interaction will show in your wallet activities but the internal transaction won’t show, the transaction that shows up on your MetaMask won’t show the value sent but your wallet balance will update, the balance update can be significant or not depending on the amount you withdraw form the SFS.

By the way, internal transactions are transactions that are initiated inside code itself, it involves smart contract sending value to a wallet or another smart contract. You can learn more about internal transactions [here](https://support.metamask.io/hc/en-us/articles/360058568312-Internal-transactions)

You can find the internal transaction by opening the transaction hash on Mode explorer and then clicking the internal tnxs tab

<figure><img src="../../../.gitbook/assets/SFS Withdrawal Guide.png" alt=""><figcaption></figcaption></figure>

Here you’ll see the actual transaction and the value sent. You can also click on your wallet address here to see your balance.

### **Summary**

In this article we learnt about the SFS Withdraw function and how it works, we also tested that to see it in action. We also learnt about internal transactions and how to view them on Mode explorer.

To learn more about Mode and how to turn your code into a business, join our [Discord](https://dub.sh/mode-discord) and say hello **👋**
