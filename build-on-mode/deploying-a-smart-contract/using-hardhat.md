---
description: How to deploy a sample smart contract with Hardhat on Mode
---

# Using Hardhat

This tutorial will guide you through the process of deploying a smart contract on Mode's Ethereum L2 using Hardhat and TypeScript.

#### Prerequisites

* **Node.js and npm:** Ensure both are installed. [Download here](https://nodejs.org/).
* **Ethereum Wallet:** A private key for the Mode Testnet that has testnet ETH. You can follow [bridging-to-mode-testnet.md](../../mode-testnet/bridging-to-mode-testnet.md "mention") to get some or go to [testnet-faucets.md](../../tools/testnet-faucets.md "mention"). We recommend using a new wallet without real funds in case the PK gets compromised.
* **Solidity and CLI knowledge:** A little knowledge is always helpful to follow along but it's not mandatory!

## What you'll accomplish

* Initialize a TypeScript-based Hardhat project.
* Craft a basic Ethereum smart contract.
* Set up Hardhat for Mode Testnet deployment.
* Deploy your smart contract on Mode.

## 1. Initialize a Hardhat TypeScript project&#x20;

Open your terminal and create a new directory for your project, then navigate into it:

```bash
mkdir my-hardhat-project && cd my-hardhat-project
```

Initialize an npm project:

```bash
npm init -y
```

Install the necessary packages for Hardhat and TypeScript:

```bash
npm install --save-dev hardhat ts-node typescript @nomiclabs/hardhat-ethers ethers
```

Start a new Hardhat project with TypeScript:

```bash
npx hardhat init
```

When prompted, make the following selections:

* Choose "Create a TypeScript project".
* For the `.gitignore` prompt, select "Yes" (or `y`).
* For installing the projects dependencies select "Yes" (or `y`).

```bash
[~/Mode/my-hardhat-project]$ npx hardhat

888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888      88b 888P   d88  888 888  88b      88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888  Y888888 888      Y88888 888  888  Y888888  Y888

👷 Welcome to Hardhat v2.18.2 👷‍

✔ What do you want to do? · Create a TypeScript project
✔ Hardhat project root: · /Users/Mode/my-hardhat-project
✔ Do you want to add a .gitignore? (Y/n) · y
✔ Do you want to install this sample project's dependencies with npm (@nomicfoundation/hardhat-toolbox)? (Y/n) · y
```

## 2. Drafting the Smart Contract

&#x20;In the `contracts` directory,  delete the sample smart contract `Lock.sol` and then create a new file named `HelloWorld.sol`:&#x20;

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract HelloWorld {
    string public greet = "Hello, Mode!";

    function setGreet(string memory _greet) public {
        greet = _greet;
    }

    function getGreet() public view returns (string memory) {
        return greet;
    }
}
```

## 3. Configuring Harhdat for Mode

&#x20;Edit the `hardhat.config.ts` file to include Mode Testnet settings:

```typescript
import "@nomiclabs/hardhat-ethers";

import { HardhatUserConfig } from "hardhat/config";

const config: HardhatUserConfig = {
  networks: {
    mode: {
      url: "https://sepolia.mode.network",
      chainId: 919,
      accounts: ["YOUR_PRIVATE_KEY_HERE"] //BE VERY CAREFUL, DO NOT PUSH THIS TO GITHUB
    }
  },
  solidity: "0.8.0",
};

export default config;
```

Replace `YOUR_PRIVATE_KEY_HERE` with your Mode Testnet private key.

{% hint style="danger" %}
<mark style="color:red;">**IMPORTANT:**</mark> Do not push your <mark style="color:yellow;">`hardhat.config.ts`</mark> file to github nor share your private key with anyone. It is a very common mistake to push your PK to github so make sure that in the .gitignore you add the <mark style="color:yellow;">`hardhat.config.ts`</mark>
{% endhint %}

## 4. Compilation

Compile the smart contract:

```bash
npx hardhat compile
```

## 5. Deployment&#x20;

In the `scripts` directory, create a new file named `deploy.ts`:

```typescript
import { ethers } from "hardhat";

async function main() {
    const gasPrice = ethers.utils.parseUnits('10', 'gwei'); // Adjust the '10' as needed
    const gasLimit = 500000; // Adjust this value based on your needs
    const HelloWorld = await ethers.deployContract("HelloWorld", {
      gasPrice: gasPrice,
      gasLimit: gasLimit,
    });
    await HelloWorld.waitForDeployment();
    console.log("HelloWorld deployed to:", HelloWorld.getAddress());
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

{% hint style="warning" %}
If you get any gas related issues you will need to check what's the best gasPrice and gasLimit, you can find some info about the state of the chain in [BlockScout](https://sepolia.explorer.mode.network/)
{% endhint %}

Deploy the smart contract to the Mode Testnet:

```bash
npx hardhat run scripts/deploy.ts --network mode
```

####

## 6. Check your contract in a block explorer&#x20;

Verify your smart contract's deployment on the Mode Testnet block explorer: [https://sepolia.explorer.mode.network/](https://sepolia.explorer.mode.network/). \
\
Input the contract address from the console to view its details.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 7. Conclusion

Congratulations! You've successfully deployed a smart contract on the Mode Testnet using Hardhat and TypeScript.\
\
To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋

If you want the next challenge, you can try registering a contract for the SFS following this guide: [sfs-registering-a-contract-with-remix.md](../sfs-sequencer-fee-sharing/register-a-smart-contract/sfs-registering-a-contract-with-remix.md "mention")\
\
