---
description: >-
  This is the actual Governance Season and all the details about the Mode
  Governance.
---

# 4️⃣ Mode Governance Season 4

## Season 4

### Overview

Building on the Season 3 framework of community-driven decision-making, Season 4 refines Mode’s governance with enhanced clarity, transparency, and accountability. It introduces:

* Stricter gauge eligibility tied to timely distribution and reporting of incentives.
* Formal bribe marketplace integration (Hidden Hand) to standardize bribe distribution and claims.
* Anytime unstaking within an epoch (no longer limited to voting windows).

### Introduction

Season 4 continues to use veTokens (veMODE and veBPT) for voting and distributing OP incentives to protocols. With each epoch (two-week period), voting power and incentive emissions gradually increase. Protocols compete for gauge votes to secure OP rewards, which must be used to drive on-chain adoption and ecosystem growth.

### **Governance Model Overview**

Mode uses two types of veTokens to facilitate governance decisions:

• **veMODE:** Stake MODE tokens.

• **veBPT:** Stake 80/20 MODE/ETH Balancer Pool Tokens.

Each veToken directs a separate allocation of OP incentives (10:1 ratio in favor of veMODE), and both accrue voting power gradually over the season (up to 6x max voting power). Participants can stake one or both, receiving OP rewards for active voting.

#### **Voting Power: Increases on Curve**

Stakers who commit from the first epoch and remain staked through all six epochs will see their voting power climb steadily from 1x to 6x by the final epoch. This growth applies regardless which epoch stakers begin staking.

#### **Emissions and Incentive Distribution**

Season 4 has up to $2M in OP incentives which follow a multi-epoch structure with a gradually increasing emission schedule. Participants vote for their preferred protocols, influencing the share of OP each protocol receives.

* **OP Rewards:** Entirely OP-based, no MODE tokens are distributed.
* **Gauge Voting:** Active voters earn OP each epoch, and protocols receive OP allocations proportional to their gauge votes.
* **Eligibility Requirements:** Protocols must adhere to distribution and reporting rules (detailed below) to remain gauge-eligible.

#### **Protocol Voting and Bribes**

Voting windows open every two weeks, during which veMODE and veBPT holders assign votes to protocols. The Season 4 bribe system integrates with Hidden Hand, allowing protocols to deposit bribes for voters. At the end of the voting period, a snapshot determines bribe distribution, and users can easily claim via the Hidden Hand UI.\


**Updated Unstaking and Cooldown Windows**

A key Season 4 improvement is the ability to initiate cooldown at any time during an epoch:

* **Initiate Unstake:** Your votes are removed, and your staked veTKN NFT enters an exit queue.
* **Cooldown (3–6 Days):** Overlaps with voting or distribution windows.
* **Withdrawal**: After cooldown, retrieve your tokens at your convenience.

**Epoch Timeline and Process Flow**

Season 4 maintains a two-week epoch structure, but with more fluidity in cool-down initiation and more rigorous gauge eligibility. A typical epoch includes:

* **Staking (Ongoing):** Users add or remove stake, with at least a short warm-up before newly staked tokens can vote.
* **Voting Window (7 Days):** veTKN holders vote for protocols, and protocols can deposit bribes via Hidden Hand.
* **Distribution Window (\~7 Days):** Protocols receive OP based on the last epoch’s voting results. They must distribute it promptly and transparently.
* **Protocol Eligibility Window:** Protocols must submit or update distribution plans/reports to maintain gauge eligibility for the next epoch (unless using Merkl, in which Merkl will stream the data on protocols’ behalf).

### **Step-by-Step Guide to Participate**

1. Acquire MODE or 80/20 MODE/ETH BPT.
2. Stake on gov.mode.network to receive veMODE or veBPT.
3. Warm Up until the next checkpoint interval.
4. Vote during the 7-day voting window, optionally collecting bribes from Hidden Hand.
5. Earn OP Rewards each epoch for staking and voting.

Unstake Anytime via the new flexible cooldown process.\


### Maintaining Protocol Eligibility

Season 4 introduces stricter reporting requirements. Protocols have two options:

* **Register with Merkl (Preferred):**

Fill out the [Merkl form](https://tally.so/r/wQ82Zl) (one submission per epoch). Merkl automates your campaigns. If no new form is submitted, the campaign from the previous epoch continues.

* **Custom Distribution & Reporting:**

[Submit](https://forum.mode.network/c/governance/incentive-distributions/8) a detailed distribution plan within 48 hours of receiving OP. Provide a follow-up report (or API/data feed) for each epoch’s distribution by the beginning of the voting window two epochs later.

Failure to comply may result in your gauge being toggled off until the missing distribution data or plan is provided.\


### Transitional Details (Season 3 → Season 4)

**January 9–15** is reserved for protocol documentation submissions, ensuring compliance and gauge eligibility prior to the first epoch’s voting.

### Benefits of **Participating**

* **Flexible Unstaking:** Enter cooldown any time, not confined to a single voting window.
* **Active Role:** Influence incentive flows to protocols and applications you care about.
* **Transparent & Accountable:** Bribes are centralized in a single marketplace (Hidden Hand), while protocols have clear reporting obligations.
* **Long-Term Rewards:** Earn OP and watch your voting power grow linearly up to 6x when staked for the entire season.
