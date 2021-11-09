---
title: Home
description: Welcome to the documentation website for the InvArch IP Management & Decentralized Development platform, a parachain on Polkadot that is fully Ethereum compatible.
---

# Welcome to InvArch

![Main Page Banner](assets/images/cover.png)

This site provides documentation for InvArch, an IP management and decentralized development parachain on the Polkadot network that is fully Ethereum compatible. Here, you'll find both high-level and technical information for developers, collators, end-users, and other InvArch network participants.

This site will grow and be refined over time as InvArch is developed.  We welcome you to join the InvArch community and contribute to this site and to the project.

---

## What is InvArch? {: #what-is-invarch } 

InvArch is an IP management and development protocol with smart contract functionality. It is a future Polkadot parachain that will allow users to tokenize their ideas and developers to build new and exciting applications that utilize this database.

InvArch will also be a parachain on the Polkadot network. That means it will get shared security from the Polkadot relay chain and will be able to integrate with other chains that are connected to Polkadot (once that functionality is available on Polkadot).

---

## How to Get Started with InvArch {: #how-to-get-started-with-invarch } 

### Networks {: #networks } 

Currently, there are a few ways you can start building on InvArch: 

 - Build your own InvArch instance as a [development node](/builders/get-started/InvArch-dev/)
 - [Connect](/builders/get-started/moonbase/) to the [Moonbase Alpha TestNet](/learn/platform/networks/moonbase/)
 - [Connect](/builders/get-started/moonriver/) to [Moonriver](/learn/platform/networks/moonriver/)


### Deploy a Contract {: #deploy-a-contract } 

Because of InvArch's Ethereum compatibility features, you can use the development tools you know and love to deploy a contract:

 - [Ethereum Libraries](/builders/interact/eth-libraries/)
 - [Remix](/builders/interact/remix/)
 - [OpenZeppelin and Remix](/builders/interact/oz-remix/)
 - [HardHat](/builders/interact/hardhat/)
 - [Truffle](/builders/interact/truffle/)
 - [Waffle and Mars](/builders/interact/waffle-mars/)


### Tools and Integrations {: #tools-and-integrations } 

 - [Web3.js](/builders/tools/eth-libraries/web3js/)
 - [Ethers.js](/builders/tools/eth-libraries/etherjs/)
 - [Web3.py](/builders/tools/eth-libraries/web3py/)
 - [The Graph](/builders/integrations/indexers/thegraph/)
 - [Covalent API](/builders/integrations/indexers/covalent/)
 - [Debug & Trace](/builders/tools/debug-trace/)

### Oracles {: #oracles } 

 We also have a number of Oracles that can serve as data feed to your smart contracts:

 - [Chainlink](/builders/integrations/oracles/chainlink/)

### Bridges {: #bridges } 

Currently, we have a fully functioning bridge implementation that connects Ethereum's Rinkeby/Kovan TestNets and Tinker Alpha:

 - [ChainBridge](/builders/integrations/bridges/eth/chainbridge/)

---

## How to Engage With the InvArch Community {: #how-to-engage-with-the-invarch-community } 

### :fontawesome-brands-discord:  Discord {: #fontawesome-brands-discord-discord } 
Instructions for our TestNet and other development-focused conversation is found on our [Discord channel](https://discord.com/invite/UDuyBC2EC7).

<!-- ### :InvArch-element:  Element {: #InvArch-element-element } 
Technical discussions and support are encouraged in our Element (formerly Riot) room that can be found [here](https://app.element.io/#/room/#InvArch:matrix.org). -->

### :fontawesome-brands-telegram-plane:  Telegram {: #fontawesome-brands-telegram-plane-telegram } 
General information and other non-technical topics can be discussed in our Telegram group [here](https://t.me/InvArch).

### :fontawesome-brands-twitter:  Twitter {: #fontawesome-brands-twitter-twitter } 
Follow us on Twitter for regular updates: [@InvArchNetwork](https://twitter.com/InvArchNetwork).

### :fontawesome-brands-youtube:  YouTube {: #fontawesome-brands-youtube-youtube } 
For video-tutorials and related content, subscribe to our YouTube channel [here](https://www.youtube.com/channel/UCSUD4kuRxXfOuRkVL0hpxXg).

### :fontawesome-solid-envelope:  Newsletter {: #fontawesome-solid-envelope-newsletter } 
We send a monthly newsletter with project updates that you can sign up for [here](https://InvArch.network/newsletter/).

## About This Site {: #about-this-site } 
This site is generated using [mkdocs](https://www.mkdocs.org/) and [Material for MKDocs](https://squidfunk.github.io/mkdocs-material/) theme and is based on content in the InvArch-docs repo, which can be found [on :fontawesome-brands-github: GitHub](https://github.com/InvArch/InvArch-docs).

### Getting Started with MkDocs

- Install MkDocs
To install MkDocs, run the following command from the command line:

```bash
pip install mkdocs
```

For more details, see the [MkDocs Installation Guide](https://github.com/mkdocs/mkdocs/blob/master/docs/user-guide/installation.md).

- Clone this repo
```
git clone https://github.com/InvArch/InvArch-docs
cd InvArch-docs
```

- Open in your browser
then start the server by running the `mkdocs serve`
command:

```bash
$ mkdocs serve
INFO    -  Building documentation...
INFO    -  Cleaning site directory
[I 160402 15:50:43 server:271] Serving on http://127.0.0.1:8000
[I 160402 15:50:43 handlers:58] Start watching changes
[I 160402 15:50:43 handlers:60] Start detecting changes
```

Open up `http://127.0.0.1:8000/` in your browser, and you'll see the
home page being displayed.