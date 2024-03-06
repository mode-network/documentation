---
description: How to verify smart contract on Mode using hardhat
---

# Using Hardhat

## Introduction

Verifying a smart contract on the blockchain is an essential step to ensure its transparency, security, and ease of interaction for users and other developers. Hardhat has emerged as a powerful tool for compiling, testing, deploying, and verifying smart contracts.

This tutorial will guide you through the process of verifying your smart contract on Mode network using Hardhat.

## Prerequisites

Before diving into the verification process, ensure you have the following ready:

1. Hardhat Installed: A foundational requirement, as Hardhat will be used for compiling, deploying, and verifying your smart contract.
2. Node.js and NPM: Hardhat runs on Node.js, and you'll use NPM (Node Package Manager) to install the Hardhat verification package.
3. Ethereum Wallet: A wallet like MetaMask, connected to the Mode network, is essential for deploying and managing your contracts.
4. Your Smart Contract Deployed: A smart contract already deployed on the Mode network. This guide assumes you've completed the deployment process but if you haven' t please check [deploying-a-smart-contract](../deploying-a-smart-contract/ "mention")

### Step 1: Installing Hardhat Verify Package

The first step is to integrate verification capabilities into your Hardhat environment. This is achieved by installing the @nomicfoundation/hardhat-verify plugin. Run the following command in your project's root directory:

```sh
npm install --save-dev @nomicfoundation/hardhat-verify
```

### Step 2: Configuring Hardhat

With the verification plugin installed, you need to import it and enable Sourcify integration in your `hardhat.config.ts`. This configuration aids in the verification process by ensuring your source code is published and verified through Sourcify. \
\
Add the following lines to your hardhat.config.ts:

```typescript
import "@nomicfoundation/hardhat-verify";
// Your existing configuration
module.exports = {
  // Other configurations
  sourcify: { enabled: true },
};
```

You hardhat.config file should look something like this:

{% tabs %}
{% tab title="TypeScript" %}
```typescript
import "@nomiclabs/hardhat-ethers";
import "@nomicfoundation/hardhat-verify";

import { HardhatUserConfig } from "hardhat/config";

const config: HardhatUserConfig = {
  networks: {
    modeTestnet: {
      url: "https://sepolia.mode.network",
      chainId: 919,
      accounts: ["YOUR_PRIVATE_KEY"],
    },
    modeMainnet: {
      url: "https://mainnet.mode.network/",
      chainId: 34443,
      accounts: ["YOUR_PRIVATE_KEY"],
    },
  },
  sourcify: {
    enabled: true,
  },
  solidity: "0.8.0",
};

export default config;
```
{% endtab %}
{% endtabs %}

### Step 3: Verifying Your Contract

With your project configured for verification, you're ready to verify your smart contract on the Mode network. Replace \<contract-address> with the actual address of your deployed contract. The command below initiates the verification process:

**For Testnet Verification**

If your contract is on the Mode testnet, use the following command, replacing `CONTRACT_ADDRESS` with your contract's actual address:

{% code fullWidth="true" %}
```sh
npx hardhat verify --network modeTestnet <contract-address>
```
{% endcode %}

**For Mainnet Verification**

For contracts deployed on the Mode mainnet, the command adjusts slightly to point to the mainnet explorer:

```sh
npx hardhat verify --network modeMainnet <contract-address>
```

{% hint style="info" %}
NB: Ensure the network name in your command aligns with your `hardhat.config.ts` setup.
{% endhint %}

This command communicates with the Mode network (as defined in your Hardhat configuration) and submits your contract's source code and metadata for verification. Upon successful verification, your contract's source code will be publicly visible on the blockchain, associated with its on-chain address.\
\
You should get a similar response to the one below:

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-29 at 3.21.50 PM.png" alt=""><figcaption></figcaption></figure>

### Conclusion

Verifying your smart contract on Mode using Hardhat not only enhances the transparency and credibility of your project but also significantly improves the end-user experience by facilitating easier interactions and verifications. Following the steps outlined in this guide, developers can ensure their contracts are verified and open for scrutiny, fostering a more secure and trustworthy ecosystem.



**Further Resources**

[Hardhat Documentation](https://hardhat.org/docs)

[Mode Network Explorer](https://explorer.mode.network/) (For checking contract verification status)
