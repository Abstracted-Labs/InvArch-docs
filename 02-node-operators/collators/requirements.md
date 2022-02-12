# Requirements

### Introduction <a href="#introduction" id="introduction"></a>

There are some requirements to keep in mind before diving into running a collator node. You need to have top of the line hardware, securely created and stored accounts, meet bonding requirements, and fill out a collator questionnaire.

It is recommended to go through all of the necessary requirements on the Tinker TestNet before collating on a production network like InvArch.

This guide will help you to get started fulfilling the collator requirements so you can get your node up and running in no time.

### Hardware Requirements <a href="#hardware-requirements" id="hardware-requirements"></a>

Collators must have a full node running with the collation options. To do so, follow the Run a Node tutorial and installation steps for [Using Systemd](https://docs.moonbeam.network/node-operators/networks/run-a-node/systemd/). Make sure you use the specific code snippets for collators.

{% hint style="info" %}
Running a **collator** node has higher CPU requirements than the ones provided in the above tutorial. In order for your collator node to be able to keep up with a high transaction throughput a CPU with high clock speed and single-core performance is important, as the block production/import process is almost entirely single-threaded. Running your collator node in Docker is also not recommended, as it will have a significant impact in performance.
{% endhint %}



From a hardware perspective, it is important to have top of the line hardware to maximize block production and rewards. The following are some hardware recommendations that have performed well and provided the best results:

* **Recommended CPUs** - Intel Xeon E-2386/2388 or Ryzen 9 5950x/5900x
* **Recommended NVMe** - 1 TB NVMe
* **Recommended RAM** - 32 GB RAM

In addition, you should take into account the following considerations:

* As most cloud providers focus on multi-thread rather than single-thread performance, using a bare-metal provider is recommended
* You should have primary and backup bare metal servers in different data centers and countries. Hetzner is OK for one of these servers, but shouldn't be used for both
* Your Tiker server should be dedicated for Tinkeronly, please do not use the same server for other apps

### Account Requirements <a href="#account-requirements" id="account-requirements"></a>

Similar to Polkadot validators, you need to create an account. For Tinker, this is an H160 account or an Ethereum-style account from which you hold the private keys. As a collator, you are responsible for correctly managing your own keys. Incorrectly doing so can result in a loss of funds.

There are many Ethereum wallets that can be used, but for production purposes it is recommended to generate keys as securely as possible. It is also recommended to generate backup keys. You can actually generate keys using the Tinker binary through a tool called **InvArchKey**.

To generate keys securely it is recommended to do so on an air-gapped machine. Once you generate your keys make sure you store them safely. To securely store your keys, here are some recommendations, from least to most secure:

* Write down and laminate your keys
* Engrave your keys into a metal plate
* Shard your keys using a tool like [Horcrux](https://gitlab.com/unit410/horcrux)

As always, it is recommended to do your own research and use tools that you vet as trustworthy.

#### Getting Started with InvArchKey <a href="#getting-started-with-moonkey" id="getting-started-with-moonkey"></a>

The first step is to fetch the **invarchkey** binary file hosted on GitHub. To do so, you can download a binary file (tested on Linux/Ubuntu):

`https://github.com/InvArch/invarch-node/releases/download/v0.1.0/invarchkey`

Once you’ve downloaded the tool, ensure you have the correct access permissions to execute the binary file. Next, check that you have the right version by checking the downloaded file hash.

For Linux-based systems such as Ubuntu, open the terminal and head to the folder where the InvArchKey binary file is located. Once there, you can use the sha256sum tool to calculate the SHA256 hash:

```
019c3de832ded3fccffae950835bb455482fca92714448cc0086a7c5f3d48d3e
```

After you’ve verified the hash, it is recommended to move the binary file to an air-gapped machine (no network interfaces). You can also check the hash of the file in the air-gapped device directly.

#### Generating an Account with InvArchKey <a href="#generating-an-account-with-moonkey" id="generating-an-account-with-moonkey"></a>

Using the InvArchKey binary file is very straightforward. Every time you execute the binary, the information related to a newly created account is displayed.

This information includes:

* Mnemonic seed: a 24-word mnemonic that represents your account in readable words. This gives direct access to your funds, so you need to store these words securely
* Private key: the private key associated with your account, used for signing. This is derived from the mnemonic seed. This gives direct access to your funds, so you need to store it securely
* Public address: your account’s address
* Derivation path which tells the Hierarchical Deterministic (HD) wallet how to derive the specific key

{% hint style="info" %}
Please safely store the private key/mnemonic and do not share it with anyone. Private keys/mnemonics provide direct access to your funds.
{% endhint %}

It is recommended that you use the binary file in an air-gapped machine.

#### Other InvArchKey Features <a href="#other-moonkey-features" id="other-moonkey-features"></a>

InvArchKey provides some additional functionalities. The following flags can be provided:

* `-help` – prints help information
* `-version` – prints version of InvArchKey you are running
* `-w12` – generates a 12 words mnemonic seed (default is 24)

The following options are available:

* `-account-index` – provide as input the account index to use in the derivation path
* `-mnemonic` – provide as input the mnemonic

### Bonding Requirements <a href="#bonding-requirements" id="bonding-requirements"></a>

There are two bonds for you to be aware of: a bond to join the collator pool and a bond for key association.

#### Minimum Collator Bond <a href="#minimum-collator-bond" id="minimum-collator-bond"></a>

First, you will need a minimum amount of tokens staked (self-bonded) to be considered eligible and become a candidate. Only a certain number of the top collator candidates by total stake, including self-bonded and delegated stake (total bonded), will be in the active set of collators.

| Variable                  | Value        |
| ------------------------- | ------------ |
| Minimum self-bound amount | 100000 VARCH |
| Minimum total bond amount | 100000 VARCH |
| Active set size           | 50 collators |

#### Key Association Bond <a href="#key-association-bond" id="key-association-bond"></a>

Secondly, you will need a bond for key association. This bond is sent when **mapping your author ID** (session keys) with your account for block rewards, and is per author ID registered.

| Variable     | Value       |
| ------------ | ----------- |
| Minimum bond | 10000 VARCH |

### Collator Questionnaire <a href="#collator-questionnaire" id="collator-questionnaire"></a>

There is a **Collator Questionnaire**, that aims to assess the state of all collators on Tinker. You should be running a collator node on Tinker before filling out this form. You will be able to provide your contact information as well as some basic hardware specs. It provides a way to... "give us your contact info so we can contact you if we see your node isn't running well"
