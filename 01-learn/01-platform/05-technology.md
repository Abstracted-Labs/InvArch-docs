# Technology

## The InvArch Development Stack

InvArch is an IP management with smart contract functionality platform built in the Rust programming language using the Substrate framework.

## Rust Programming Language

Rust is a good language for implementing a blockchain, as it is highly performant like C and C++, but has built-in memory safety features that are enforced at compile time, which prevents many common bugs and security issues that can arise from C and C++ implementations.

## Substrate Framework

Substrate provides a rich set of tools for creating blockchains, including a runtime execution environment that enables a generic state transition function, and a pluggable set of modules that provide implementations of various blockchain subsystems.

InvArch leverages multiple existing Substrate frame pallets to provide key blockchain services and functionality, including core blockchain data structures, peer-to-peer networking, consensus mechanisms, accounts, assets, and balances. Custom pallets and logic in the runtime implement InvArch-specific behavior and functionality, such as cross-chain token integration. For leveraged pallets, InvArch will strive to stay as close as possible to the upstream Substrate codebase and incorporate Substrate bug fixes, enhancements, and new features on an ongoing basis.

## Blockchain Runtime

The core InvArch runtime specifies the state transition function and behavior of the InvArch blockchain. The InvArch runtime is built using FRAME. It includes several standard pallets as well as several custom ones. The runtime is compiled to a WebAssembly (Wasm) binary as well as a native binary. These compiled versions will be executed in the Polkadot relay chain and InvArch node environments.
