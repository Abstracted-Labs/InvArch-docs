# Tinker TestNet

### Goal&#x20;

The first InvArch TestNet, named Tinker, aims to provide developers with a place to start experimenting and building on InvArch in a shared environment. Since InvArch will be deployed as a parachain on Polkadot, we want our TestNet to reflect our production configuration. For this reason, we decided that it needed to be a parachain-based configuration rather than a Substrate development setup.&#x20;

In order to collect as much feedback as possible and provide fast issue resolution, we have set up a Tinker Testnet channel on [InvArch Discord server.](../01-learn/01-platform/08-important-links.md)&#x20;

### Run a Collator (Tinker)&#x20;

This guide will instruct you how to set up a collator node on the InvArch Tinker Testnet.
- **Github**: 
- **Bootnode IP address**: 
- **Bootnode Peer ID**: 
- **customSpecRaw.json** 

### Initial Configuration&#x20;

Tinker Testnet has the following configuration:&#x20;

* Tinker Testnet runs as a parachain connected to a relay chain&#x20;
* The parachain has two collators (hosted by InvArch) that are collating blocks. External collators can join the network. Only the top 60 collator nodes by stake are chosen in the active set&#x20;
* The relay chain hosts three validators (hosted by InvArch) to finalize relay chain blocks. One of them is selected to finalize each block collated by InvArch’s collators. This setup provides room to expand to a two-parachain configuration in the future&#x20;
* There are two RPC endpoints (hosted by InvArch). People can run full nodes to access their own private RPC endpoints&#x20;

#### Requirements&#x20;

The most common way for a beginner to run a collator is on a cloud server running Linux. You may choose whatever VPS provider you prefer, and whichever operating system you are comfortable with. For this guide we will be using **Ubuntu 20.04**, but the instructions should be similar for other platforms.

The transaction weights in Polkadot were benchmarked on standard hardware. It is recommended that validators run at least the standard hardware in order to ensure they are able to process all blocks in time. The following are not minimum requirements but if you decide to run with less than this, you may experience performance issues.

#### Standard Hardware

For the full details of the standard hardware please see [here](https://github.com/paritytech/substrate/pull/5848)

- **CPU** - Intel(R) Core(TM) i7-7700K CPU @ 4.20GHz
- **Storage** - A NVMe solid state drive. Should be reasonably sized to deal with blockchain growth. Starting around 80GB - 160GB will be okay for the first six months of Tinker, but will need to be re-evaluated every six months.
- **Memory** - 64GB

The specs posted above are by no means the minimum specs that you could use when running a validator, however you should be aware that if you are using less you may need to toggle some extra optimizations in order to match up to other validators that are running the standard.

### Node Prerequisites: Install Dependencies and Rust

Once you choose your cloud service provider and set-up your new server, the first thing you will do is install the necessary dependencies.

```
sudo apt install make clang pkg-config libssl-dev build-essential curl git
```

If you intend to build from source you need to install Rust first.

If you have already installed Rust, run the following command to make sure you are using the latest version.

```
rustup update
```

If not, this command will fetch the latest version of Rust and install it.

```
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

Add the required toolchains with rustup

```
source $HOME/.cargo/env
rustup toolchain add nightly-2021-06-28
rustup target add wasm32-unknown-unknown --toolchain nightly-2021-06-28
rustup target add x86_64-unknown-linux-gnu --toolchain nightly-2021-06-28

```

Verify your installation.

```
rustc --version
```

Note - if you are using OSX and you have Homebrew installed, you can issue the following equivalent command INSTEAD of the previous one:

```
brew install cmake pkg-config openssl git llvm
```

### Install & Configure Network Time Protocol (NTP) Client

[NTP](https://en.wikipedia.org/wiki/Network_Time_Protocol) is a networking protocol designed to synchronize the clocks of computers over a network. NTP allows you to synchronize the clocks of all the systems within the network. Currently it is required that validators' local clocks stay reasonably in sync, so you should be running NTP or a similar service. You can check whether you have the NTP client by running:

If you are using Ubuntu 18.04 / 20.04, NTP Client should be installed by default.

```
timedatectl
```

If NTP is installed and running, you should see `System clock synchronized: yes` or a similar message. If you do not see it, you can install it by executing:

```
sudo apt-get install ntp
```

ntpd will be started automatically after install. You can query ntpd for status information to verify that everything is working:

```
sudo ntpq -p
```


### Connect to Tinker Testnet&#x20;

#### Network Endpoints&#x20;

Tinker Testnet has two types of endpoints available for users to connect to: one for HTTPS and one for WSS.&#x20;

If you're looking for your own endpoints suitable for production use, you can check out the Endpoint Providers section of our documentation. Otherwise, to get started quickly you can use one of the following public HTTPS or WSS endpoints:&#x20;

HTTPS&#x20;

* InvArch       [https://rpc.testnet.invarch.io ](https://rpc.testnet.invarch.io)
* OnFinality   [https://tinker.api.onfinality.io/public](https://tinker.api.onfinality.io/public)

WSS&#x20;

* InvArch        [wss://wss.testnet.invarch.io](wss://wss.testnet.invarch.io)
* OnFinality    [wss://tinker.api.onfinality.io/public-ws](wss://tinker.api.onfinality.io/public-ws)&#x20;

To connect to the Tinker relay chain, you can use the following WS Endpoint:&#x20;

* InvArch         [wss://wss-relay.testnet.invarch.io ](wss://wss-relay.testnet.invarch.io)

#### Quick Start&#x20;

For the web3.js library, you can create a local Web3 instance and set the provider to connect to Tinker Testnet (both HTTP and WS are supported):

`const Web3 = require('web3'); //Load Web3 library . . . //Create local Web3 instance - set Tinker as provider const web3 = new Web3('https://rpc.testnet.invarch.io');`

For the ethers.js library, define the provider by using `ethers.providers.StaticJsonRpcProvider(providerURL, {object})` and setting the provider URL to Tinker Testnet:

const ethers = require('ethers');

`const providerURL = 'https://rpc.testnet.invarch.io'; // Define Provider const provider = new ethers.providers.StaticJsonRpcProvider(providerURL, { chainId: 4471, name: 'tinker-testnet' });`

#### Chain ID&#x20;

Tinker TestNet chain ID is: `4471`, which is `0x1177` in hex.&#x20;

#### Relay Chain&#x20;

To connect to the Tinker relay chain, managed by InvArch, you can use the following WS Endpoint: `wss://wss-relay.testnet.invarch.io`

Telemetry You can see current Tinker telemetry information visiting this link: `https://telemetry.polkadot.io/#list/TinkerTestnet`

#### Tokens&#x20;

Tokens on Tinker Testnet, named TNKR, will be issued on demand. **TINK tokens hold no value and can be freely acquired**. Currently, there are three ways you can get access to this token: through a Discord bot, Twitter faucet, or manually.&#x20;

#### Discord - Faucet Drip&#x20;

To request tokens automatically, we've created a Discord bot (named Faucet Drip) that will automatically send a maximum of 5 TNKR tokens every 24 hours (per Discord user) when you enter your address. You can check it out on our Discord channel. For more information, please visit this site.&#x20;

Under the category "Miscellaneous", you will find our Tinker testnet bot channel. Enter the following message, replacing `<enter-address-here>` **** with your Polkadot address:&#x20;

`!faucet send <enter-address-here>`

#### Twitter Faucet&#x20;

For token requests of more than the limited account allowed by our Discord bot, share your address and tag our moderator on our official [Twitter](https://twitter.com/InvArchNetwork) account. We are happy to provide the tokens needed to test your applications.&#x20;

#### Manual Procedure&#x20;

For token requests of more than the limited account allowed by our Discord bot, contact a moderator directly via our [Discord](http://discord.gg/invarch) channel. We are happy to provide the tokens needed to test your applications.&#x20;

### Proof of Stake&#x20;

The Tinker TestNet is a fully decentralized Nominated Proof of Stake (NPoS) network where users of the network can nominate collator candidates to produce blocks and "earn rewards" for testing purposes. Please note that the Tinker Testnet TNKR tokens have no real value. The number of candidates in the active set will be subject to governance. The active set will consist of the top candidates by stake, including nomination.&#x20;

### Limitations&#x20;

This is the first TestNet for InvArch, so there are some limitations.&#x20;

However, all built-in functions are still under development. Users only have access to the InvArch parachain. In future networks, we will add access to the relay chain so users can test transferring tokens.&#x20;