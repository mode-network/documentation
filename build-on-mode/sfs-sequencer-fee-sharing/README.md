---
description: Intro to the Sequencer Fee Sharing
hidden: true
noIndex: true
---

# SFS - Sequencer Fee Sharing

When building a layer 2 with the OP stack, block production is primarily managed by a single party, called the sequencer, which helps the network by providing the following services:

* Providing transaction confirmations and state updates
* Constructing and executing L2 blocks
* Submitting user transactions to L1\
  \
  Until fault proofs are implemented in the OP ecosystem these sequencers are centralized for security and managed by Mode (as every other OP chain) and that’s why Mode benefits from all the sequencer fees generated. That’s where the SFS comes in, giving part of these fees and sharing them with developers that deploy smart contracts.

{% hint style="success" %}
Developers can earn a share of the network sequencer fees just by registering their contracts in the Fee Sharing Contract.\
\
You have to add logic to your smart contract in order to register it in the SFS
{% endhint %}

\
The Sequencer Fee Sharing (SFS) contract acts as a registry where all the balances are tracked and stored. Once you deploy your contract and register it in the SFS, you will instantly start earning fees whenever your contract is used.\
\
When you register your contract, the SFS mints an NFT as a claim to the earned fees. This NFT is sent to the <mark style="color:orange;">**`_recipient`**</mark> that you specify when calling the register function. The SFS NFT allows anyone who possesses it to claim the rewards for that particular smart contract. Whether the NFT is in your wallet or a smart contract, whatever entity tries to withdraw the earnings needs to hold the NFT in order to withdraw funds.
