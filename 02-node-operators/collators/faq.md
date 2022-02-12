# FAQ

### Introduction <a href="#introduction" id="introduction"></a>

Collators are an integral part of the parachains they take part in. They receive transactions and create state transition proofs for the relay chain validators.

Running a Moobeam collator requires Linux systems administration skills, careful monitoring, and attention to detail. Below are some tips and tricks that have been accumulated which should help you get up and running quickly.

### Q & A <a href="#q-a" id="q-a"></a>

**Q: Where can I get help?**

**A:** There is an active and friendly [Discord](https://discord.com/invite/invarch) community for collators. Join the server and introduce yourself even before you need help. Send **Gabriel** or **Kresna** a DM and let them know who you are, and they can reach out to you if they see any issues with your node.

***

**Q: How do I stay up to date?**

**A:** All upgrades and important technical information are announced on [Discord](https://discord.com/invite/invarch), in the **#tech-upgrades-announcements** channel. Join and follow this channel. You can set up integrations to Slack or Telegram if those are your preferred communication channels.

***

**Q: How do I register my node?**

**A:** There is a [questionnaire](https://docs.google.com/forms/d/e/1FAIpQLSfjmcXdiOXWtquYlBhdgXBunCKWHadaQCgPuBtzih1fd0W3aA/viewform), in which you will be able to provide your contact information as well as some basic hardware specs. You must be running a collator node on Tinker to fill out the questionnaire.

***

**Q: What are the hardware requirements?**

**A:** Running a collator requires top of the line hardware to be able to process transactions and maximize your rewards. This is a very important factor in block production and rewards.

Run a systemd service on a top of the line bare-metal machine (i.e. run a physical server, not a cloud VM, or a docker container). You can run your own, or select a provider to manage the server for you.

Run only one service at a time per bare-metal machine. Do not run multiple instances.

***

**Q: What is the recommended hardware to run a collator?**

**A:**

Hardware recommendations:

* Top of the line CPU:
  * Ryzen 9 5950x or 5900x
  * Intel Xeon E-2386 or E-2388
* Primary and backup bare metal servers in different data centers and countries (Hetzner is OK for one of them)
* Dedicated server for Tinker that isn't shared with any other apps
* 1 TB NVMe HDD
* 32 GB RAM

***

**Q: What about backup nodes?**

**A:** Run two bare-metal machines of the same specifications, in different countries and service providers. If your primary fails you can quickly resume services on your backup and continue to produce blocks and earn rewards. Please refer to the Q\&A on [failovers](https://docs.moonbeam.network/node-operators/networks/collators/faq/#:\~:text=What%20is%20the%20failover%20process%20if%20my%20Primary%20node%20is%20down) below.

***

**Q: What are the different networks?**

**A:** There are three networks, each will require dedicated hardware. The Tinker TestNet is free and should be used to familiarize yourself with the setup.

* **InvArch** - production network on Polkadot
* **Tinker TestNet** - development network

***

**Q: What ports do I allow on my firewall?**

**A:**

* Allow all incoming requests on TCP ports 30333 and 30334
* Allow requests from your management IPs on TCP port 22
* Drop all other ports

***

**Q: Is there a CPU optimized binary?**

**A:** On each **release page** are CPU optimized binaries. Select the binary for your CPU architecture.

* **InvArch-znver3** - Ryzen 9
* **InvArch-skylake** - Intel
* **InvArch** - generic can be used for all others

***

**Q: What are the recommendations on monitoring my node?**

**A:** Monitoring is very important for the health of the network and to maximize your rewards. We recommend using [Grafana Labs](https://grafana.com). They have a free tier which should handle 6+ InvArch servers.

***

**Q: What are the KPIs I should be monitoring?**

**A:** The main key performance indicator is blocks produced. The prometheus metric for this is called `substrate_proposer_block_constructed_count`.

***

**Q: How should I setup alerting?**

**A:** Alerting is critical to keeping your Tinker node producing blocks and earning rewards. We recommend [pagerduty.com](https://www.pagerduty.com), which is supported by [Grafana Labs](https://grafana.com). Use the [KPI query](https://docs.moonbeam.network/node-operators/networks/collators/faq/#:\~:text=substrate\_proposer\_block\_constructed\_count) above and set an alert when this drops below 1. The alert should page the person on-call 24/7.

***

**Q: What are Nimbus keys?**

**A:** Nimbus keys are just like [session keys in Polkadot](https://wiki.polkadot.network/docs/learn-keys#session-keys). You should have unique keys on your primary and backup servers. Save the key output somewhere safe where you can access it in the middle of the night if you receive an alert. To create your keys, please refer to the **Session Keys** section of the documentation.

***

**Q: What is the failover process if my primary node is down?**

**A:** When the primary server is down, the best way to perform a failover to the backup server is to perform a key association update. Each server should have a unique set of **keys** already. Run the `updateAssociation` author mapping extrinsic. You can follow the **Mapping Extrinsic** instructions and modify the instructions to use the `updateAssociation` extrinsic.

***

**Q: Should I set up centralized logging?**

**A:** [Grafana Labs](https://grafana.com) can also be configured for centralized logging and is recommended. You can see all your nodes in one place. [Kibana](https://www.elastic.co/kibana/) has a more robust centralized logging offering, but Grafana is simple and good enough to start.

***

**Q: What should I look for in the logs?**

**A:** Logs are very useful to determine if you are in sync and ready to join the collators pool. Look at the tail end of the logs to determine if:

1. Your Relay chain is in sync
2. Your parachain is in sync

You should see **Idle** in your logs when your node is in sync.

![In sync Relay chain and parachain](https://docs.moonbeam.network/images/node-operators/networks/collators/account-management/account-1.png)

A common issue is joining the pool before your node is in sync. You will be unable to produce any blocks or receive any rewards. Wait until you are in sync and idle before joining the candidate pool.

![Relay chain not in sync yet](https://docs.moonbeam.network/images/node-operators/networks/run-a-node/docker/full-node-docker-2.png)

The relay chain takes much longer to sync than the parachain. You will not see any finalized blocks until the relay chain has synced.

***

**Q: How much is the bond to become a collator?**

**A:** There are two bonds you need to be aware of. Make sure your node is configured and in sync before proceeding with these steps.

The first is the **bond to join the collator**s pool:

* **InvArch**- minimum of 100000 VARCH
* **Tinker** - minimum of 500 TINK

The second is the **bond for key association**:

* **InvArch** - minimum of 10000 VARCH
* **Tinker** - minimum of 100 TINK

***

**Q: How do I set an identity on my collator account?**

**A:** Setting an identity on chain will help to identify your node and attract delegations. You can set an identity by following the instructions on the **Managing an Identity** page of our documentation.
