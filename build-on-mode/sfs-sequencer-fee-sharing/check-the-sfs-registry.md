---
description: >-
  This is a tutorial on how to check the SFS registry to see if you correctly
  registered your smart contract
---

# Check the SFS registry

When registering a smart contract in the [SFS (Sequencer Fee Sharing) contract](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=txs) an NFT gets minted to the <mark style="color:orange;">`_receiver`</mark> address that enables that wallet to claim the corresponding fees.

In this tutorial, we will cover two potential checks:

1. Check if your wallet has the NFT minted during the registry
2. Check if the contract is registered in the SFS contract-=

If it’s your first time registering a contract and you don't see the NFT, you may need to add the new token to your wallet. For this, you will need the SFS contract address and the number of the token minted when registering the contract.

### Adding the SFS NFT to your wallet

Go to blockscout and look for the transaction that registered your smart contract.&#x20;

This is an example one on testnet:\
\
[https://sepolia.explorer.mode.network/tx/0x233e46178a8bc1bf7497b2b73591eb8d7f1dbcb33b6263b817c3777ad4041b6b](https://sepolia.explorer.mode.network/tx/0x233e46178a8bc1bf7497b2b73591eb8d7f1dbcb33b6263b817c3777ad4041b6b)

<figure><img src="https://lh4.googleusercontent.com/vH8UzqvN_-eDp1SN0brDKw7JN6OeQ0jeAdb8BUgWtb7njLCC5OEMuX6JJgMnhiPZapE_DBCnEviCPxMuGhqCff43qQp0Vrury3fBUAtKs1TYIUpgWCSoMyTMRP76aD9vKxetGQQKP7xc6kcro4TMKKQ" alt=""><figcaption><p>Example transaction showing the register transaction</p></figcaption></figure>

In the register transaction you will find the token ID (see screenshot above). You can also find this value as the output of the register function of the SFS.

With the SFS contract address and the token ID, you can add the NFT to our wallet to see it. \


<figure><img src="https://lh5.googleusercontent.com/dcYLa2nT8gns3QseNkvi0PIvh20meDMvQm9Lhqu6ONZNyhD5vmAIQDlLeaJgIxjXSYViuOErK7dutb7L6h9zBIlwVSBpu1Rp7XTSoKab2FVJGGoZ9rm1QK4WrtGeAWS_3aBfxoOsdO0pGphZehJ9RyY" alt="" width="188"><figcaption></figcaption></figure>

If you can see the NFT in your wallet, most probably the register was done successfully! You can already use this wallet to claim rewards, if any are available.

### Checking the SFS registry

The SFS smart contract keeps track of all the registered smart contracts. You can always go and check if any smart contract is registered or not.&#x20;

To do this go to the [SFS contract in blockscout](https://sepolia.explorer.mode.network/address/0xBBd707815a7F7eb6897C7686274AFabd7B579Ff6?tab=read\_contract). You should go to the “Contract” tab and inside go to the “Read contract” tab.

Look for the <mark style="color:orange;">`isRegistered`</mark> function. Paste the contract address of your smart contract in the field, in my case, it’s <mark style="color:orange;">`0xcc9c90501678de6E0c6340E702e0482E95516eac`</mark>. Click on Query and see the response you get below.\
\
If it says “true” it means that smart contract is registered!

<figure><img src="https://lh5.googleusercontent.com/GSBvJzAW2LOFckVDFBzJqulzRacgZ8fdzhxwp0HLj611wt2Hnupy6Sr7AikZ64_N6aCUewgngZgcD5a4_xHcH0xvUYddeKzGxcSxjmu2akW__XYCUMk7AKcFiuoLjo76foqKSzcxzBVGx0dRpaF_mLY" alt=""><figcaption></figcaption></figure>

That's all you need to know on how to check if a smart contract is registered in the SFS.

To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋
