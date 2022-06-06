# Why Polkadot

After extensive research, we decide to build InvArch using the Substrate development framework and deploy InvArch as a parachain on the Polkadot network.

## Substrate Blockchain Framework

Substrate is a good technical fit for InvArch. By building on top of this framework, we can leverage the extensive functionality that Substrate includes out-of-the-box, rather than building it ourselves. This includes per-to-peer networking, consensus mechanisms, governance functionality, EVM implementation, and many more.

Overall, using Substrate will dramatically reduce the time and implementation effort needed to implement InvArch. Substrate allows a great degree of customization, which is necessary in order to achieve our Ethereum compatibility goals. And, by using Rust, we benefit from both safety guarantees and performance gains.

## Polkadot Network and Ecosystem

The Polkadot Network is also a good fit for InvArch. As a parachain on Polkadot, InvArch will be able to directly integrate with -- and move tokens between -- any other parachains and parathreads on the network.

We can also leverage any of the bridges that are independently built to connect non-Polkadot chains to Polkadot, including bridges to Ethereum and any other non-Substrate chains. Polkadot's interoperability model uniquely supports InvArch's cross-chain integration goals and is a key enabling technology to support the InvArch vision.

But perhaps just as important as the technical criteria above, we are impressed with the community in the Polkadot ecosystem. This includes individuals at Parity, the Web3 Foundation, and other projects within the ecosystem. We have built many valuable relationships and find the people to be both extremely talented, helpful and the kind of people we want to be around.

## Kusama Network and the Tinker Parachain

The Tinkernet Parachain is the canary network of the InvArch Network, designed as the IP Asset & accelerated development staging grounds for the [Kusama](https://kusama.network/) ecosystem. The Tinkernet serves a trio of testing purposes, one for the developers who maintain the network, one for the developers who build on top of the network, and one for the end-users of dApps & applications in the ecosystem.

The InvArch team & its aspiring developers can test changes on the Tinkernet through forkless runtime upgrades before any possibility of deploying them directly on the InvArch Parachain. This way, Kusama can provide an experimental proving ground & a “first-to-market” experience that helps reinforce the security & “best-to-market” environment found on the Polkadot Network. This also allows for the Tinkernet to act as a proving ground to the broader community before seeking a full launch on the InvArch Network Parachain.

## Brainstorm testnet

The Brainstorm testnet is a sandbox for no-consequences exploration and prototyping of ideas. It aims to replicate the Tinker experience as close as possible while relying on valueless tokens that can be claimed at any time. On this testnet (that will be running indefinitely), users are able to make mistakes and go back to their drawing board until they have something worthy of going to Tinkernet with.
