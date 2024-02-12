---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 🤝 Sequencer Fee Sharing

Roll-ups such as Mode earn revenues from the network sequencer. With Mode’s Sequencer Fee Sharing (SFS) module developers can register contracts and receive a proportion of Mode’s sequencer revenue based on the transaction fees of smart contracts they deploy.

You can find more info and technical guides on the[sfs-sequencer-fee-sharing](../../build-on-mode/sfs-sequencer-fee-sharing/ "mention")tutorials.

### Overview

Developers can earn a share of the network Sequencer fees by registering their contracts in the Fee Sharing Contract.\
\
A portion of transaction fees of all transactions involving their smart contract will accumulate in the Fee Sharing Contract.

The SFS contract issues an NFT as a claim to the earned fees by the recipient specified in the call to register the smart contract. This NFT is transferable and can be used to claim fees for multiple contracts. Several contracts can be assing to one SFS NFT, but each contract will only be linked to one SFS NFT.

An offchain component will process the transactions for each smart contract to calculate it's share of fees. This component will also deposit the earned fees in the SFS contract for devs to later withdraw. Note that withdrawals can be done in the end of each epoch which on mainnet happens every 2 weeks and every 24 hours on testnet.
