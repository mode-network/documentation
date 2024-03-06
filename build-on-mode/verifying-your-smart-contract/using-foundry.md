---
description: How to verify smart contract on Mode using foundry
---

# Using Foundry

## Introduction

Foundry is the Rust-built toolbox designed to streamline your smart contract development process. It's your comprehensive toolkit for not just creating and testing, but also for the crucial step of verifying your smart contracts. Verification ensures your code's transparency and trustworthiness on the blockchain. This guide focuses on verifying any smart contract on the Mode network's mainnet and testnet using Foundry.

## Getting Ready

Before we dive in, make sure you've got a few things in place:

* Deployed your smart contract to the Mode network. This guide assumes you've completed the deployment process but if you haven' t please check [deploying-a-smart-contract](../deploying-a-smart-contract/ "mention")
* Installed Rust and Foundry, as Foundry leverages Rust for its operations.

Got everything? Great! Let's get started.

## Step 1: Prepare Your Contract for Verification

Ensure your smart contract, such as an ERC20 token, is ready and deployed. Keep the contract's address at hand, as you'll need it for the verification command.

## Step 2: Verifying Your Contract

Verification is a straightforward process with Foundry. Depending on where your contract is deployed, you'll use either the mainnet or testnet command.

**For Testnet Verification**

If your contract is on the Mode testnet, use the following command, replacing `CONTRACT_ADDRESS` with your contract's actual address:

{% code fullWidth="true" %}
```sh
forge verify-contract CONTRACT_ADDRESS src/MyERC20.sol:MyERC20 --verifier blockscout --verifier-url https://sepolia.explorer.mode.network/api\?
```
{% endcode %}

**For Mainnet Verification**

For contracts deployed on the Mode mainnet, the command adjusts slightly to point to the mainnet explorer:

```sh
forge verify-contract CONTRACT_ADDRESS src/MyERC20.sol:MyERC20 --verifier blockscout --verifier-url https://explorer.mode.network/api\?
```

{% hint style="info" %}
Remember to replace CONTRACT\_ADDRESS with your contract's address and src/MyERC20.sol:MyERC20 with the correct path to your contract.
{% endhint %}

## Step 3: Confirm Your Contract's Verification

After executing the relevant command:

* Visit the Mode explorer ([mainnet](https://explorer.mode.network/) or [testnet](https://sepolia.explorer.mode.network/), as applicable).
* Enter your contract's address in the search bar.
* You should find your contract listed and verified, it should have the green checkmark just like the image below.

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-06 at 1.33.40 PM.png" alt=""><figcaption></figcaption></figure>

## Conclusion

And that's it! You've just verified your ERC20 token on the Mode network using Foundry. Not too bad, right? Foundry makes these tasks less of a headache, so you can focus on the fun part: building your project.
