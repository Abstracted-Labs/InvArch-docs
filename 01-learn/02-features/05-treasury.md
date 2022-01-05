# Treasury

## Introduction

A treasury is an on-chain managed collection of funds. InvArch will have a community treasury for supporting network initiatives to further the network. This treasury will be funded by a percentage of transaction fees of the network and will be managed by the Council.

Each InvArch-based network will have it's own treasury. In other words, the Tinker Alpha TestNet, Tinker Beta on Westend/ Rococo, Tinker on Kusama, and InvArch on Polkadot will each have their own respective treasury.

## General Definitions

Some important terminology to understand in regards to treasuries:

- **Council** — a group of elected individuals that control how treasury funds will be spent
- **Proposal** — a plan or suggestion to further the network that is put forth by stakeholders to be approved by the council
- **Proposal bond** — a deposit equal to a percentage of the total proposal spend amount
- **Proposal bond minimum** — minimum amount for a proposal bond. This amount must be paid as the bond if it is higher than the deposit percentage
- **Spend period** — the amount of days, in blocks, during which the treasury funds as many proposals as possible without exceeding the maximum
- **Maximum approved proposals** — the maximum amount of proposals that can wait in the spending queue

| Variable | InvArch | Tinker |
| --- | --- | --- |
| **Proposal bond** |5% of the proposed spend | 5% of the proposed spend |
| **Proposal bond minimum** | 1 VARCH | 1 TNKR) |
| **Spend period** | 43200 blocks (6 days) | 43200 blocks (6 days) |
| **Maximum approved proposals** | 100 | 100 |
| **% transaction fees allocated** | 20 | 20 |

## Community Treasury

To fund the Treasury, a percentage of each block's transactions fees will be allocated to it. The remaining percentage of the fees are burned (check table above). The Treasury allows stakeholders to submit spending proposals to be reviewed and voted on by the Council. These spending proposals should include initiatives to further the network or boost network engagement. Some network initiatives could include funding integrations or collaborations, community events, network outreach, and more.

To deter spam, proposals must be submitted with a deposit, also known as a proposal bond.The proposal bond needs to be higher than the minimum amount, known as the proposal bond minimum, which can be changed by a governance proposal. So, any token holder that has enough tokens to cover the deposit can submit a proposal. If the proposer doesn't have enough funds to cover the deposit, the extrinsic will fail due to insufficient funds, but transaction fees will still be deducted.

Once a proposal has been submitted, is subject to governance, and the council votes on it. If the proposal gets rejected, the deposit will be lost and transfered to the treasury pot. If approved by the council, the proposal enters a queue to be placed into a spend period. If the spending queue happens to contain the number of maximum approved proposals, the proposal submission will fail similarly to how it would if the proposer's balance is too low.

Once the proposal is in a spend period, the funds will get distributed to the beneficiary and the original deposit will be returned to the proposer. If the treasury runs out of funds, the remaining approved proposals will remain in storage until the next spend period when the Treasury has enough funds again.
