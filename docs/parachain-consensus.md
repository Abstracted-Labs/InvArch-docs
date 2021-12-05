# Cumulus Parachain Consensus

## Introduction

Polkadot relies on a [hybrid consensus model](https://wiki.polkadot.network/docs/learn-consensus). In such a scheme, the block finality gadget and the block production mechanism are separate. Consequently, parachains only have to worry about producing blocks and rely on the relay chain to validate the state transitions.

At a parachain level, block producers are called [collators](https://wiki.polkadot.network/docs/learn-collator). They maintain parachains (such as InvArch) by collecting transactions from users and offering blocks to the relay chain [validators](https://wiki.polkadot.network/docs/learn-validator).

However, parachains might find the following problems they need to solve in a trustless and decentralized matter (if applicable):

 - Amongst all of the nodes in the network, which ones are allowed to author blocks?
 - If multiple nodes are allowed, will they be eligible at the same time? Only one? Maybe a few?

[Cumulus](https://github.com/paritytech/cumulus) is a framework for building slot-based consensus algorithms on parachains. It strives to provide standard implementations for the logistical parts of such consensus engines and helpful traits for implementing the elements (filters) that researchers and developers want to customize. These filters can be customizable to define what a block authorship slot is and can be composed, so block authorship is restricted to a subset of collators in multiple steps.

[Cumulus](https://wiki.polkadot.network/docs/build-pdk#cumulus) consensus mechanism that marks  parachain block as best, and ultimately the [BABE](https://wiki.polkadot.network/docs/learn-consensus#babe) and [GRANDPA](https://wiki.polkadot.network/docs/learn-consensus#grandpa-finality-gadget) hybrid consensus model (of the relay chain) that will include this parachain block in the relay chain and finalize it. Once any relay chain forks are resolved at a relay chain level, that parachain block is deterministically finalized.

The following two sections go over the filtering strategy currently used in InvArch.

## Parachain Staking Filtering

Collators can join the candidate pool by simply bonding some tokens via an extrinsic. Once in the pool, token holders can add to the collator's stake via nomination (also referred to as staking), that is, at a parachain level.

Parachain staking is the first of the two Nimbus filters applied to the collator candidate pool. It selects the top {{ networks.moonbase.staking.max_collators }} collators in terms of tokens staked in the network, which includes the collator bond and nominations from token holders. This filtered pool is called selected candidates, and selected candidates are renewed every round (which lasts {{ networks.moonbase.staking.round_blocks }} blocks). For a given round, the following diagram describes the parachain staking filtering:

From this pool, another filter is applied to retrieve a subset of eligible collators for the next block authoring slot.

If you want to learn more about staking, visit our [staking documentation](/staking).

## Fixed Size Subset Filtering

Once the parachain staking filter is applied and the selected candidates are retrieved, a second filter is applied on a block by block basis and helps narrow down the selected candidates to a smaller number of eligible collators for the next block authoring slot.

In broad terms, this second filter picks a pseudo-random subset of the previously selected candidates. The eligibility ratio, a tunable parameter, defines the size of this subset.

A high eligibility ratio results in fewer chances for the network to skip a block production slot, as more collators will be eligible to propose a block for a specific slot. However, only a certain number of validators are assigned to a parachain, meaning that most of these blocks will not be backed by a validator. For those that are, a higher number of backed blocks means that it might take longer for the relay chain to solve any possible forks and return a finalized block. Moreover, this might create an unfair advantage for certain collators that might be able to get their proposed block faster to relay chain validators, securing a higher portion of block rewards (if any).

A lower eligibility ratio might provide faster block finalization times and a fairer block production distribution amongst collators. However, if the eligible collators are not able to propose a block (for whatever reason), the network will skip a block, affecting its stability.

Once the size of the subset is defined, collators are randomly selected using a source of entropy. Currently, an internal coin-flipping algorithm is implemented, but this will later be migrated to use the relay chain's [randomness beacon](https://wiki.polkadot.network/docs/learn-randomness). Consequently, a new subset of eligible collators is selected for every relay chain block. For a given round and a given block `XYZ`, the following diagram describes the fixed-size subset filtering: 

[Cumulus Parachain Consensus Image]()

## Why Cumulus?

In the [relay chain provided consensus](https://github.com/paritytech/cumulus/blob/master/client/consensus/relay-chain/src/lib.rs), each node sees itself as a colator and can propose a parachain candidate block. It is then up to the relay chain to solve any possible forks and finalize a block. 

[AuRa](https://crates.io/crates/sc-consensus-aura) (short for authority-round) consensus mechanism is based on a known list of authorities that take turns to produce blocks in every slot. Each authority can propose only one block per slot and builds on top of the longest chain.