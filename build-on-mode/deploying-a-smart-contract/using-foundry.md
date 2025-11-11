---
description: How to deploy with Foundry on Mode
---

# Using Foundry

This guide will walk you through the deployment of an ERC20 token on MODE using [Foundry](https://book.getfoundry.sh/). \
Foundry is a smart contract development toolchain written in Rust.

Foundry manages your dependencies, compiles your project, runs tests, deploys, and lets you interact with the chain from the command-line and via Solidity scripts.

Given that MODE is built on the OP Stack and is EVM-compatible, you can easily port any Ethereum-based smart contract without modifying the core code, requiring only minor setting adjustments.

## Prerequisites

Even if you need to do these 3 steps, it won’t take more than 10 minutes to set up:

* Have some ETH on Mode Testnet Network. You can follow our guide on [how to bridge](../../user-guides/bridge/bridging-to-mode-testnet.md). Or use [this faucet](https://faucet.modedomains.xyz/) to claim some ETH on Mode.
* Rust must be installed on your computer. If it's not, [follow this guide](https://doc.rust-lang.org/book/ch01-01-installation.html).
* Foundry must be installed on your computer. If it’s not, [follow this guide](https://book.getfoundry.sh/getting-started/installation).

{% hint style="info" %}
If you just want to skip to the build & deploy section of this tutorial, you can clone [this repository](https://github.com/LuchoLeonel/foundry-mode-boilerplate) that contains a boilerplate Foundry project and skip to [step 3](using-foundry.md#3.-building-the-contract).
{% endhint %}

Let's get started!

## 1. Setting up the project

1.1 Initialize a new Foundry project:

Forge is the command-line interface (CLI) tool for Foundry, allowing developers to execute operations directly from the terminal.

Open up a terminal and run this command:

<pre class="language-bash"><code class="lang-bash"><strong>forge init my-project
</strong></code></pre>

1.2. Install the OpenZeppelin contracts library inside your project, which provides a tested and community-audited implementation of ERC20:

<pre class="language-bash"><code class="lang-bash"><strong>forge install OpenZeppelin/openzeppelin-contracts
</strong></code></pre>

## 2. Writing the ERC20 token contract

2.1. In **/src** of your project directory, create a text file named **MyERC20.sol** and add:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "lib/openzeppelin-contracts/contracts/token/ERC20/ERC20.sol";

contract MyERC20 is ERC20 {
    constructor() ERC20("MyToken", "MTK") {}
}
```

This is a simple ERC20 token named "MyToken" with the symbol "MTK". You can name it any way you want and also write any other contracts. Just remember that if your file name is called differently, the commands to deploy will be slightly different.&#x20;

This is what you should have up to now:

<figure><img src="https://lh6.googleusercontent.com/1jahpfwmFhOAiT_xMNIb0-kux3ARUGOy-3euxZ7_gT6Gg17CnCIGNbaeLIqrisbaNa1ZyJ_npaKhMyHNnyZCZ_fnmWknw3fo4P_1immNKd6fDyWDYc8rU6srodquISlaY64TTpbdar9d57v5RSuWWFk" alt=""><figcaption></figcaption></figure>

## 3. Building the contract

3.1. Use Foundry to compile your smart contract running the following command:

{% code fullWidth="false" %}
```bash
forge build
```
{% endcode %}

## 4. Deploying the ERC20 token contract

4.1. To deploy your contract you will need to run the following command and replace \<YOUR\_PRIVATE\_KEY> with your credentials:

{% hint style="warning" %}
Never share or expose your private key publicly. This will grant complete control to whoever has it. Please store it safely.
{% endhint %}

{% code overflow="wrap" lineNumbers="true" %}
```bash
forge create --rpc-url https://sepolia.mode.network --private-key <YOUR_PRIVATE_KEY> src/MyERC20.sol:MyERC20
```
{% endcode %}

{% hint style="success" %}
PRO TIP: You can add the --verify flag and use blockscout to verify your contract while deploying.&#x20;
{% endhint %}

The following is the command to deploy and verify the contract. If you already deployed your contract but still want to verify it, don't panic! Next step will walk you through that case.

{% code overflow="wrap" lineNumbers="true" %}
```bash
forge create --rpc-url https://sepolia.mode.network --private-key <YOUR_PRIVATE_KEY> src/MyERC20.sol:MyERC20 --verify --verifier blockscout --verifier-url https://sepolia.explorer.mode.network/api\?
```
{% endcode %}

In the output you should get something like:

{% code overflow="wrap" %}
```
[⠢] Compiling... No files changed, compilation skipped 
Deployer: 0x3F26b51E23D01b09f4079B2a9e00e6873a8409D8 
Deployed to: 0x628F56856386A4De8414A4D8217D519bF94d03f0 
Transaction hash: 0xbe2d27554f130a720c4dd82dad055c941ca44dee836f6333a8507d76022c158
```
{% endcode %}

Copy the “Deployed to” value and store it somewhere to use later. This is the address of your contract.

4.2. Create a deployment script:
In the **/script** directory of your project, create a file named **DeployMyERC20.s.sol** and add the following content:

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import {Script} from "forge-std/Script.sol";
import {MyERC20} from "../src/MyERC20.sol";

contract DeployMyERC20 is Script {
    function run() external {
        uint256 deployerPrivateKey = vm.envUint("PRIVATE_KEY");
        vm.startBroadcast(deployerPrivateKey);
        MyERC20 token = new MyERC20();
        vm.stopBroadcast();
    }
}
```

```bash
forge script script/DeployMyERC20.s.sol:DeployMyERC20 --rpc-url <RPC_URL> --broadcast --private-key <YOUR_PRIVATE_KEY>
```

## 5. Verifying the ERC20 token contract after deployment

5.1. For already deployed contracts you can use the verify-contract command:

{% code overflow="wrap" lineNumbers="true" %}
```bash
forge verify-contract <CONTRACT_ADDRESS> src/MyERC20.sol:MyERC20  --verifier blockscout --verifier-url https://sepolia.explorer.mode.network/api\?
```
{% endcode %}

## 6. Exploring and interacting with your deployed contract

Use the [blockscout](https://sepolia.explorer.mode.network/) explorer to view your contract's details. Paste your contract's address you saved from the deployment output into blockscout's search bar.

In the "Contract" tab you'll find your verified contract.

<figure><img src="https://lh5.googleusercontent.com/OJLvZ0NHyU_z-JXDaPXZGfjMhAPsWr0PENTz5FCGAvB89b57lT05jwVJu6CFwW-isDp_5ySWmP55IS4mP7QO9ybM5J0N88dcHLHXSJo_f-IGaXxbb-oEUUGj5mjG6J64Tmb-oxNYKD1A3Xpg6hXZ_gk" alt=""><figcaption></figcaption></figure>

***

Congratulations, you just deployed and verified a contract on Mode Network using Foundry.&#x20;

To learn more about Mode and how to turn your code into a business, join our [Discord](https://discord.gg/modenetworkofficial) and say hello 👋
