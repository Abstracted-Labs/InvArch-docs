# Staking in InvArch

## Introduction
InvArch uses a block production mechanism based on Polkadot's [Proof-of-Stake](https://wiki.polkadot.network/docs/learn-consensus) model, where there are ***collators*** and ***validators***. [Collators](https://wiki.polkadot.network/docs/learn-collator) maintain parachains (in this case, InvArch) by collecting transactions from users and producing state transition proofs for the relay chain [validators](https://wiki.polkadot.network/docs/learn-validator).

The collators' set (nodes that produce blocks) are selected based on their stake in the network. And here is where staking comes in.

Collators (and token holders if they nominate) have a stake in the network. The top N collators by staked amount are chosen to produce blocks with a valid set of transactions, where N is a configurable parameter. Part of each block reward goes to the collator that produced the block, who then shares it with the nominators considering their percental contributions towards the collator's staked. In such a way, network members are incentivized to stake tokens to improve the overall security.

General Definitions
Some important parameters to understand in relation to the staking system in InvArch include:

- **Collators** — block producers. They collect transactions from users and produce state transition proofs for the relay chain to validate. Have a stake in the network that get slashed if they misbehave
- **Nominators** — token holders who stake tokens, vouching for specific collators. Any user that holds a minimum amount of tokens as free balance can become a nominator
- **Minimum nomination stake** — minimum amount of total tokens staked a user must have to be in the set of nominators
- **Minimum nomination** — minimum amount of tokens to nominate other collators once a user is in the set of nominators
- **Maximum nominators per collator** — maximum number of nominators a collator can have
- **Maximum collators per nominator** — maximum number of collators a nominator can nominate
- **Round** — a specific number of blocks around which staking actions are enforced. For example, new nominations are enacted when the next round starts. When revoking nominations, funds are returned after a certain amount of rounds

## Quick Reference

|  | InvArch | Tinker | 
| --- | --- | --- |
| **Minimum nomination amount** | 5 VARCH | 5 TNKR |
| **Round duration** | 300 blocks, time per round is approximately 1 hour | 300 blocks, time per round is approximately 1 hour |
| **Max eligible nominators per collator** | for a given round, only the top 100 nominators by staked amount are eligible for staking rewards | for a given round, only the top 100 nominators by staked amount are eligible for staking rewards |
| **Max collators per nominator** | a nominator can nominated 25 different collators | a nominator can nominated 25 different collators |
| **Bonding duration** | nomination takes effect in the next round (funds are withdrawn immediately) | nomination takes effect in the next round (funds are withdrawn immediately) |
| **Unbonding duration** | 2 rounds | 2 rounds |
| **Reward payout time** | 2 rounds. Rewards are distributed automatically to the free balance | 2 rounds. Rewards are distributed automatically to the free balance |
| **Collator commission** | fixed at 20% of the annual inflation (5%). Not related to the nominators reward pool | fixed at 20% of the annual inflation (5%). Not related to the nominators reward pool |
| **Nominators reward pool** | 50% of the annual inflation | 50% of the annual inflation
 |
| **Nominator rewards** | variable. It's the aggregate nominator rewards distributed over all eligible nominators, taking into account the relative size of stakes | variable. It's the aggregate nominator rewards distributed over all eligible nominators, taking into account the relative size of stakes |
| **Slashing** | currently, there is no slashing. This can be later changed through governance. Collators who produce blocks that are not finalized by the relay chain won't receive rewards | currently, there is no slashing. This can be later changed through governance. Collators who produce blocks that are not finalized by the relay chain won't receive rewards |
| **Collator information** | list of collators: [InvArch Subscan](https://). Collator data for the last two rounds: [InvArch Explorer](https://) | list of collators: [Tinker Subscan](https://). Collator data for the last two rounds: [Tinker Explorer](https://) |
| **Manage staking related actions**  | visit the [InvArch dApp](https://) | visit the [Tinker dApp](https://) |

To learn how to get the current value of any of the parameters around staking, check out the [Retrieving Staking Parameters]() section of the [How to Stake your Tokens]() guide. 

<!-- TODO: WIP -->

## Reward Distribution

Collators are rewarded at the end of every round (300 blocks) for their work from 2 rounds ago.

The distribution of the 5% annual inflation goes as follows:

 - 1% goes to incentivizing collators
 - 1.5% goes to the parachain bond reserve
 - The remaining 2.5% will go to users that stake their tokens

Out of that 2.5%, collators gets the rewards corresponding to their stake in the network.The rest are distributed among nominators by stake.

Mathematically speaking, for collators, the reward distribution per block proposed and finalized would look like this:

```
 reward = (0.2 x amount _due) + (0.5 x amount_due x stake)
```

Where `amount_due` is the corresponding inflation being distributed in a specific block, the `stake` corresponds to the number of tokens bonded by the collator in respect to the total stake of that collator (accounting nominations).

For each nominator, the reward distribution (per block proposed and finalized by the nominated collator) would look like this:

```
    reward = (0.5 x amount_due x stake)
```

Where `amount_due` is the corresponding inflation being distributed in a specific block, the `stake` corresponds to the amount of tokens bonded by each nominator in respect to the total stake of that collator.
