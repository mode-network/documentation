# 🔁 Bridge

{% hint style="success" %}
If you want third party options for bridging you can check the [ecosystem page](https://www.mode.network/ecosystem) in our main website. Please be careful when interacting with any bridge.
{% endhint %}

### **Mode Mainnet Bridge**&#x20;

You can use the Mode bridge to deposit and withdraw from Ethereum to Mode. Check out [bridge-to-mode.md](../user-guides/bridge/bridge-to-mode.md "mention")

[Access the Mode Mainnet Bridge here](https://app.mode.network/)

***

### **Mode Testnet Bridge**&#x20;

You can use the Mode bridge to deposit and withdraw ETH from Ethereum Sepolia to the Mode Sepolia Testnet. Checkout [bridging-to-mode-testnet.md](../user-guides/bridge/bridging-to-mode-testnet.md "mention")

[**Access the Mode Testnet Bridge here**](https://sepolia-bridge.mode.network/)

## thirdweb 

[**Universal Bridge**](https://thirdweb.com/connect/universal-bridge) is a comprehensive Web3 payment solution to help you monetize any app or game.  

With Universal Bridge, your users can **onramp, bridge, and swap** on any EVM chain — with any EVM token or fiat — thanks to its **automatic cross-chain routing**.  

Plus, developers can **earn from day one** using the **fee-sharing mechanism** and **easy implementation**.

**Supported Networks**
- [Mode Mainnet](https://thirdweb.com/bridge?chainId=34443)

### Universal Bridge Features

- Let users pay for assets in any EVM token on Mode right in your app  
- Automatic cross-chain routing for seamless transactions  
- Earn from day one with fee-sharing mechanism
- Access ready-made UI component for easy implementation  

[Learn more in the full documentation on thirdweb’s Universal Bridge](https://portal.thirdweb.com/connect/pay/overview)

### Get Started with thirdweb Universal Bridge

[How to get started with Universal Bridge](https://portal.thirdweb.com/connect/pay/get-started)

### See Universal Bridge in Action
Want to see how Universal Bridge works? Check it out under the hood

```jsx
import { createThirdwebClient } from "thirdweb";
import { PayEmbed } from "thirdweb/react";

import { createWallet } from "thirdweb/wallets";
import { defineChain } from "thirdweb";

const client = createThirdwebClient({
  clientId: "....",
});

function Example() {
  return (
    <PayEmbed
      client={client}
      payOptions={{
        mode: "fund_wallet",
        prefillBuy: {
          chain: defineChain(34443),
          amount: "0.01",
        },
      }}
    />
  );
}

```
[**See how the Buy Crypto flow works in the playground**](https://playground.thirdweb.com/connect/pay)
