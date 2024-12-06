# ⌨️ Node Operators

### Running the node

If you want to run a node for Mode you can follow these instructions:\
[https://github.com/mode-network/rollup-node](https://github.com/mode-network/rollup-node)

{% hint style="warning" %}
**UPCOMING HOLOCENE UPDATE**

Optimism Fork (Holocene) will be activated on ​Mainnet​ on ​`Thu 09 Jan 2025 18:00:01 UTC`Prior to the update, for nodes/integrators:\


* run op-geth >= [v1.101411.2](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Fop-geth%2Freleases%2Ftag%2Fv1.101411.2\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T)
* run op-node >= [v1.10.0](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Foptimism%2Freleases%2Ftag%2Fop-node%252Fv1.10.0\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T) (for alt-da, consider respective forks like celestia/eigen)
* set on both the flag  `--override.holocene=1736445601`
{% endhint %}

### Snapshots

Snapshots will help you save time while synching your node to Mode.&#x20;

* Mainnet

Tuesday 3rd September **(latest)** -&#x20;

{% embed url="https://storage.googleapis.com/conduit-networks-snapshots/mode/mainnet/2024-09-03.tar" %}

* Testnet

{% embed url="https://storage.cloud.google.com/conduit-networks-snapshots/mode/sepolia/latest.tar.gz" %}

## Past updates

<details>

<summary>HOLOCENE</summary>

* run op-geth >= [v1.101411.2](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Fop-geth%2Freleases%2Ftag%2Fv1.101411.2\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T)
* run op-node >= [v1.10.0](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Foptimism%2Freleases%2Ftag%2Fop-node%252Fv1.10.0\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T) (for alt-da, consider respective forks like celestia/eigen)
* set on both the flag  `--override.holocene=1736445601`

Optimism Fork (Holocene) will be activated on your ​Mainnet​ on ​`Thu 09 Jan 2025 18:00:01 UTC`Prior to the update, please confirm the following on external nodes/integrators:

* run op-geth >= [v1.101411.2](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Fop-geth%2Freleases%2Ftag%2Fv1.101411.2\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T)
* run op-node >= [v1.10.0](https://pylonlinks.com/link?url=https%3A%2F%2Fgithub.com%2Fethereum-optimism%2Foptimism%2Freleases%2Ftag%2Fop-node%252Fv1.10.0\&utm_campaign_id=b0864ff3-1c35-4e96-87fc-2c2706284a23\&utm_slack_channel=C05T5A68H9T) (for alt-da, consider respective forks like celestia/eigen)
* set on both the flag  `--override.holocene=1736445601`\
  \
  If you are not using the previous fork, Granite, on your external nodes (check the following flags is set ​`--override.granite`​), please reach out. In the case, you might need to enable the Granite hard fork flags two days before ​`Tue 07 Jan 2025 18:00:01 UTC`​. You can use the same software version and configure it with ​`--override.granite=1736272801`

</details>

<details>

<summary><strong>GRANITE UPDATE</strong> </summary>

the Optimism Granite Hard Fork happened on `Wed 11 Sep 2024 16:00:01 UTC` . More info [here](https://docs.optimism.io/builders/notices/granite-changes).For external nodes/integrators:

* run op-geth >= [v1.101408.0](https://github.com/ethereum-optimism/op-geth/releases/tag/v1.101408.0)
* run op-node >= [v1.9.1](https://github.com/ethereum-optimism/optimism/releases/tag/v1.9.1) (for alt-da, consider respective forks like celestia/eigen)
* set on op-geth and op-node the flag `--override.granite=1726070401`

</details>

<details>

<summary><a href="https://github.com/ethereum-optimism/specs/blob/main/specs/fjord/overview.md">Optimism Fjord Hard Fork</a></summary>

**FJORD UPDATE -** `Wed Jul 10 16:00:01 UTC 2024`\
\
Node operators will need to upgrade to Fjord before the activation date. For Sepolia, the op-node release [v1.7.7(opens in a new tab)](https://github.com/ethereum-optimism/optimism/releases/tag/v1.7.7) and op-geth release [v1.101315.2(opens in a new tab)](https://github.com/ethereum-optimism/op-geth/releases/tag/v1.101315.2) contain these changes.\
\
Please update to the latest releases of [op-geth](https://github.com/ethereum-optimism/op-geth/releases/tag/v1.101315.2) and [op-node](https://github.com/ethereum-optimism/optimism/releases/tag/v1.7.7).

\
**VERIFY**

Make the following checks to verify that your node is properly configured.

* `op-node` and `op-geth` will log their configurations at startup
* Check that the Fjord time is set to `activation-timestamp` in the op-node startup logs
* Check that the Fjord time is set to `activation-timestamp` in the op-geth startup logs

\
**For more information please visit** [**Optimism's documentation**](https://docs.optimism.io/builders/notices/fjord-changes#verify-your-configuration)**.**

</details>

<details>

<summary>Ecotone Upgrade (Dencun + EIP-4844)</summary>

_The Ecotone upgrade for OP Sepolia activated at **1708534800 Wed Feb 21 17:00:00 UTC 2024**._

## Getting ready for Ecotone Upgrade (Dencun + EIP-4844)

The Ecotone upgrade contains the Dencun upgrade from L1, and adopts EIP-4844 blobs for data-availability. \
\
Please refer to:\
\
[https://docs.optimism.io/builders/notices/ecotone-changes](https://docs.optimism.io/builders/notices/ecotone-changes)

* You need l1 beacon api access for op-node and pass via --l1.beacon param (or OP\_NODE\_L1\_BEACON env).&#x20;
* Consider having full-archive blobs access. if you are on the superchain you don't have to pass any new parameter.

</details>
