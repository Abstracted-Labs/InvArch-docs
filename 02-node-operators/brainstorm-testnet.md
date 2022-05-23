# Brainstorm Testnet

### Goal

The first permanent InvArch TestNet, named Brainstorm, aims to provide developers with a place to start experimenting and building on InvArch in a shared environment. Since InvArch's Tinker Parachain will be deployed as a parachain on Kusama, we want our testnet to reflect our production configuration.

In order to collect as much feedback as possible and provide fast issue resolution, we have set up a Brainstorm Testnet channel on [InvArch Discord server.](https://discord.com/invite/invarch)

### Run a Collator (Brainstorm)

This guide will instruct you how to set up a collator node on the InvArch Brainstorm Testnet.

* **Github**:
* **Bootnode IP address**:
* **Bootnode Peer ID**:
* **customSpecRaw.json**

### Initial Configuration

Brainstorm Testnet has the following configuration:

* Brainstorm Testnet runs as a parachain with mock validation (No relay chain)
* The parachain has two collators (hosted by InvArch) that are collating blocks. External collators can join the network.
* There is one WSS endpoint (hosted by InvArch). People can run full nodes to access their own private WS/RPC endpoints.

#### Requirements

The most common way for a beginner to run a collator is on a cloud server running Linux. You may choose whatever VPS provider you prefer, and whichever operating system you are comfortable with. For this guide we will be using **Ubuntu 20.04**, but the instructions should be similar for other platforms.


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

[NTP](https://en.wikipedia.org/wiki/Network\_Time\_Protocol) is a networking protocol designed to synchronize the clocks of computers over a network. NTP allows you to synchronize the clocks of all the systems within the network. Currently it is required that validators' local clocks stay reasonably in sync, so you should be running NTP or a similar service. You can check whether you have the NTP client by running:

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

### Connect to Brainstorm Testnet

#### Network Endpoints

Brainstorm Testnet has a WSS endpoint available.

If you're looking for your own endpoints suitable for production use, you can check out the Endpoint Providers section of our documentation. Otherwise, to get started quickly you can use the following public WSS endpoint:


* InvArch [wss://brainstorm.invarch.network](wss://brainstorm.invarch.network)

#### Quick Start

#### Tokens

Tokens on Brainstorm Testnet, named 🧠⛈️, will be issued on demand. **🧠⛈️ tokens hold no value and can be freely acquired**. Currently, there is a single faucet where you can acquire tokens automatically: [https://brainstorm.invarch.network](https://brainstorm.invarch.network).

### Limitations

All built-in functions are still under development.
