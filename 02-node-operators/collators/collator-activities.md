# Collator Activities

### Introduction <a href="#introduction" id="introduction"></a>

Becoming a collator on InvArch/Tinkre networks require you to meet **bonding requirements** and join the candidate pool. Once you're in the candidate pool, you can then adjust your self-bond amount or decide to leave the pool at any time.

If you wish to reduce your self-bond amount or leave the candidate pool, it requires you to first schedule a request to leave and then execute upon the request after a **delay period** has passed.

This guide will take you through the important timings to be aware of when leaving or reducing your self-bond amount, how to join and leave the candidate pool, and adjust your self-bond.

### Collator Timings <a href="#collator-timings" id="collator-timings"></a>

Before getting started, it's important to note some of the timings of different actions related to collation activities:

|                 Tinker                |         Value        |
| :-----------------------------------: | :------------------: |
|             Round duration            | 600 blocks (2 hours) |
|            Leave candidates           |  2 rounds (4 hours)  |
|           Revoke delegation           |  2 rounds (4 hours)  |
|         Reduce self-delegation        |  2 rounds (4 hours)  |
| Rewards payouts (after current round) |  2 rounds (4 hours)  |

{% hint style="info" %}
The values presented in the previous table are subject to change in future releases.
{% endhint %}

### Become a Candidate <a href="#become-a-candidate" id="become-a-candidate"></a>

#### Get the Size of the Candidate Pool <a href="#get-the-size-of-the-candidate-pool" id="get-the-size-of-the-candidate-pool"></a>

First, you need to get the `candidatePool` size (this can change through governance) as you'll need to submit this parameter in a later transaction. To do so, you'll have to run the following JavaScript code snippet from within **Polkadot.js**:

```
// Simple script to get candidate pool size
const candidatePool = await api.query.parachainStaking.candidatePool();
console.log(`Candidate pool size is: ${candidatePool.length}`);
```

1. Head to the **Developer** tab
2. Click on **JavaScript**
3. Copy the code from the previous snippet and paste it inside the code editor box
4. (Optional) Click the save icon and set a name for the code snippet, for example, "Get candidatePool size". This will save the code snippet locally
5. To execute the code, click on the run button
6. Copy the result, as you'll need it when joining the candidate pool

#### Join the Candidate Pool <a href="#join-the-candidate-pool" id="join-the-candidate-pool"></a>

Once your node is running and in sync with the network, you become a candidate (and join the candidate pool). Depending on which network you are connected to, head to **Polkadot.js** and take the following steps:

1. Navigate to the **Developer** tab and click on **Extrinsics**
2. Select the account you want to be associated with your collation activities
3. Confirm your account is funded with at least the **minimum stake required** plus some extra for transaction fees
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Open the drop-down menu, which lists all the possible extrinsics related to staking, and select the **joinCandidates()** function
6. Set the bond to at least the **minimum amount** to be considered a candidate. As an example, the minimum bond of 500 TINK in Tinker would be `500000000000000000000` in Wei (500 + 18 extra zeros). Only the candidate bond counts for this check. Additional delegations do not count
7. Set the candidate count as the candidate pool size. To learn how to retrieve this value, check the **Get the Size of the Candidate Pool** section
8. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

{% hint style="info" %}
Function names and the minimum bond requirement are subject to change in future releases.
{% endhint %}

As mentioned before, only the top candidates by delegated stake will be in the active set of collators. The exact number of candidates in the top for each network and the minimum bond amount can be found in the **Minimum Collator Bond** section.

### Stop Collating <a href="#stop-collating" id="stop-collating"></a>

To stop collating and leave the candidate pool, you must first schedule a request to leave the pool. Scheduling a request does not automatically remove you from the candidate pool, you must wait an **exit delay**. After the delay you will be able to execute the request and stop collating. While you are waiting the specified number of rounds, you will still be eligible to produce blocks and earn rewards if you're in the active set.

#### Schedule Request to Leave Candidates <a href="#schedule-request-to-leave-candidates" id="schedule-request-to-leave-candidates"></a>

To get started and schedule a request, take the following steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your candidate account
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Select the **scheduleLeaveCandidates** extrinsic
6. Enter the `candidateCount` which you should have retrieved in the **Get the Size of the Candidate Pool** section
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

#### Execute Request to Leave Candidates <a href="#execute-request-to-leave-candidates" id="execute-request-to-leave-candidates"></a>

After the waiting period has passed, you'll be able to execute the request. To execute the request, you can follow these steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your candidate account
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Select the **executeLeaveCandidates** extrinsic
6. Select the target candidate account (anyone can execute the request after the exit delay has passed after submitting the `scheduleLeaveCandidates` extrinsic)
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

#### Cancel Request to Leave Candidates <a href="#cancel-request-to-leave-candidates" id="cancel-request-to-leave-candidates"></a>

If you scheduled a request to leave the candidate pool but changed your mind, as long as the request has not been executed, you can cancel the request and remain in the candidate pool. To cancel the request you can follow these steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your candidate account
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Select the **cancelLeaveCandidates** extrinsic
6. Provide the `candidateCount` which you should have retrieved in the **Get the Size of the Candidate Pool** section
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

### Change Self-Bond Amount <a href="#change-self-bond-amount" id="change-self-bond-amount"></a>

As a candidate, changing your self-bond amount varies slightly depending on if you're bonding more or less. If you're bonding more, it is a straightforward process where you can increase your stake via the `candidateBondMore()` extrinsic. You do not have to wait any delays and you do not need to schedule a request and then execute it, instead your request will be executed instantly and automatically.

If you wish to bond less, you have to schedule a request, wait an [exit delay](https://docs.moonbeam.network/node-operators/networks/collators/activities/#collator-timings), and then you will be able to execute the request and get a specified amount of tokens back into your free balance. In other words, scheduling the request doesn't decrease the bond instantly or automatically, it will only be decreased once the request has been executed.

#### Bond More <a href="#bond-more" id="bond-more"></a>

As a candidate, there are two options for increasing one's stake. The first and recommended option is to send the funds to be staked to another owned address and **delegate to your collator**. Alternatively, collators that already have at least the **minimum self-bond amount** staked can increase their bond from **Polkadot JS Apps** as follows:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your collator account (and verify it contains the additional funds to be bonded)
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Open the drop-down menu, which lists all the possible extrinsics related to staking, and select the **candidateBondMore()** function
6. Specify the additional amount to be bonded in the **more: BalanceOf** field
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

#### Bond Less <a href="#bond-less" id="bond-less"></a>

In order to bond less, you have to first schedule a request, wait the duration of the **exit delay**, and then execute the request. You can **cancel a request** at any time, as long as the request hasn't been executed yet.

**Schedule Bond Less Request**

To schedule a request to bond less, you can follow these steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your candidate account
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Open the drop-down menu and select the **scheduleCandidateBondLess()** function
6. Specify the amount to decrease the bond by in the **less: BalanceOf** field
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

Once the transaction is confirmed, you must wait the duration of the exit delay and then you will be able to execute and decrease the bond amount. If you try to execute the request before the exit delay, your extrinsic will fail and you'll see an error in Polkadot.js for `parachainStaking.PendingDelegationRequest`.



**Execute Bond Less Request**

After the exit delay has passed from scheduling a request to decrease your bond, you can execute the request to actually decrease the bond amount by following these steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select an account to execute the request with
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Select the **executeCandidateBondLess** extrinsic
6. Select the target candidate account (anyone can execute the request after the exit delay has passed since the `scheduleCandidateBondLess` was submitted)
7. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

Once the transaction has been confirmed, you can check your free and reserved balances from the **Accounts** tab and notice now that the execution has gone through, your balances have been updated.



**Cancel Bond Less Request**

If you scheduled a request to bond more or less but changed your mind, as long as the request has not been executed, you can cancel the request at any time and keep your bond amount as is. To cancel the request you can follow these steps:

1. Navigate to the **Developer** tab
2. Click on **Extrinsics**
3. Select your candidate account (and verify it contains the additional funds to be bonded)
4. Select **parachainStaking** pallet under the **submit the following extrinsic** menu
5. Select the **cancelCandidateBondRequest** extrinsic
6. Submit the transaction. Follow the wizard and sign the transaction using the password you set for the account

\
