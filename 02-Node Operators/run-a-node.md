# Run a Node

## Introduction

Running a full node on a InvArch-based network allows you to connect to the network, sync with a bootnode, obtain local access to RPC endpoints, author blocks on the parachain, and more.

There are multiple deployments of InvArch, including the Brainstorm Testnet, Tinkernet Parachain on Kusama, and eventually there will be InvArch on Polkadot. Here's how these environments are named and their corresponding [chain specification](https://docs.substrate.io/v3/runtime/chain-specs/) file names:

| Network    | Hosted by | Chain Name |
| ---------- | --------- | ---------- |
| Brainstorm | InvArch   | brainstorm |
| Tinkernet  | Kusama    | tinkernet  |
| InvArch    | Polkadot  | invarch    |

{% hint style="info" %}
Brainstorm is a testnet, and as such _will not_ have 100% uptime. The parachain might be purged as needed. During the development of your application, make sure you implement a method to redeploy your contracts and accounts to a fresh parachain quickly. If a chain purge is required, it will be announced via our [Discord ](https://discord.com/invite/invarch)channel at least **24 hours** in advance.
{% endhint %}

## Requirement

Running a parachain node is similar to a typical Substrate node, but there are some differences. A Substrate parachain node is a bigger build because it contains code to run the parachain itself, as well as code to sync the relay chain, and facilitate communication between the two. As such, this build is quite large and may take over 30 min and require 32GB of memory.

The minimum specs recommended to run a node are shown in the following table. For our Kusama and Polkadot MainNet deployments, disk requirements will be higher as the network grows.



| Chain         | Component                                                                                                            | Requirement                      |
| ------------- | -------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| Tinker (TNKR) | CPU                                                                                                                  | 8 Cores (Fastest per core speed) |
| RAM           | 16 Gb                                                                                                                |                                  |
| SSD           | 250 GB (to start)                                                                                                    |                                  |
| Firewall      | <p>P2P port must be open to incoming traffic:</p><ul><li>Source: Any</li><li>Destination: 30333, 30334 TCP</li></ul> |                                  |

{% hint style="info" %}
If you don't see an `Imported` message (without the `[Relaychain]` tag) when running a node, you might need to double-check your port configuration.
{% endhint %}

## Running Ports

As stated before, the relay/parachain nodes will listen on multiple ports. The default Substrate ports are used in the parachain, while the relay chain will listen on the next higher port.

The only ports that need to be open for incoming traffic are those designated for P2P.

### Default Ports for a Parachain Full-Node

| Description    | Port        |   |   |
| -------------- | ----------- | - | - |
| **P2P**        | 30333 (TCP) |   |   |
| **RPC**        | 9933        |   |   |
| **WS**         | 9944        |   |   |
| **Prometheus** | 9615        |   |   |

### Default Ports of Embedded Relay Chain

| Description    | Port        |
| -------------- | ----------- |
| **P2P**        | 30334 (TCP) |
| **RPC**        | 9934        |
| **WS**         | 9945        |
| **Prometheus** | 9916        |

## Installation

There are a couple different guides to help you get started running a InvArch-based node:

* [Using Docker](run-a-node.md) - this method provides a quick and easy way to get started with a Docker container
* [Using Systemd](run-a-node.md) - this method is recommended for those with experience compiling a Substrate node

## Debug, Trace and TxPool APIs

You can also gain access to some non-standard RPC methods by running a tracing node, which allow developers to inspect and debug transactions during runtime. Tracing nodes use a different Docker image than a standard Tinker Alpha or Tinker node. Check out the [Run a Tracing Node](run-a-node.md) guide and be sure to switch to the right network tab throughout the instructions. Then to interact with your tracing node, check out the [Debug & Trace](run-a-node.md) guide.

## Logs and Troubleshooting

You will see logs from both the relay chain and the parachain. The relay chain will be prefixed by `[Relaychain]`, while the parachain has no prefix.

### P2P Ports Not Open

If you don't see an `Imported` message (without the `[Relaychain]` tag), you need to check the P2P port configuration. P2P port must be open to incoming traffic.

### In Sync

Both chains must be in sync at all times, and you should see either `Imported` or `Idle` messages and have connected peers.

### Genesis Mismatching

The Tinker TestNet may need to be purged and upgraded once in a while. Consequently, you may see the following message:

```
DATE [Relaychain] Bootnode with peer id `ID` is on a different
chain (our genesis: GENESIS_ID theirs: OTHER_GENESIS_ID)
```

This typically means that you are running an older version and will need to upgrade.

We announce the upgrades (and corresponding chain purge) via our [Discord ](https://discord.com/invite/invarch)channel at least **24 hours** in advance.

Instructions for purging chain data will vary slightly depending on how you spun up your node:

* For Docker, you can check out the [Purge Your Node](run-a-node.md) section of the [Using Docker](run-a-node.md) page
* For Systemd, you can take a look at the [Purge Your Node](run-a-node.md) section of the [Using Systemd](run-a-node.md) page
