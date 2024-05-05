# ⌨️ Node Operators

### Running the node

If you want to run a node for Mode please follow these instructions:\
[https://github.com/mode-network/rollup-node](https://github.com/mode-network/rollup-node)

### Snapshots

Snapshots will help you save time while synching your node to Mode.

* Mainnet

[https://storage.cloud.google.com/conduit-networks-snapshots/mode/mainnet/latest.tar.gz](https://storage.cloud.google.com/conduit-networks-snapshots/mode/mainnet/latest.tar.gz)

* Testnet

[https://storage.cloud.google.com/conduit-networks-snapshots/mode/sepolia/latest.tar.gz](https://storage.cloud.google.com/conduit-networks-snapshots/mode/sepolia/latest.tar.gz)

{% hint style="warning" %}
* The Ecotone upgrade for OP Sepolia activated at **1708534800 Wed Feb 21 17:00:00 UTC 2024**.
* The Ecotone OP Mainnet upgrade will be at **1710374401 Thu Mar 14 00:00:01 UTC 2024**, pending [governance approval(opens in a new tab)](https://gov.optimism.io/t/upgrade-proposal-5-ecotone-network-upgrade/7669).
{% endhint %}

<details>

<summary>Recommended op-node &#x26; op-geth versions:</summary>

**`op-geth v1.101308.2`** \
**`op-node v1.7.0`**\
\
**For celestia DA:**

[**https://github.com/celestiaorg/optimism/releases/tag/v1.2.0-OP\_v1.7.0-CN\_v0.12.4**](https://github.com/celestiaorg/optimism/releases/tag/v1.2.0-OP\_v1.7.0-CN\_v0.12.4)

</details>

## Getting ready for Ecotone Upgrade (Dencun + EIP-4844)

The Ecotone upgrade contains the Dencun upgrade from L1, and adopts EIP-4844 blobs for data-availability. \
\
To get ready for the ecotone breaking changes please refer to:\
\
[https://docs.optimism.io/builders/notices/ecotone-changes](https://docs.optimism.io/builders/notices/ecotone-changes)

* You need l1 beacon api access for op-node and pass via --l1.beacon param (or OP\_NODE\_L1\_BEACON env).&#x20;
* Consider having full-archive blobs access. if you are on the superchain you don't have to pass any new parameter.

