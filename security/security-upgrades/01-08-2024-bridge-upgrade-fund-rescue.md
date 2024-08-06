# 01/08/2024 Bridge Upgrade Fund Rescue

**Bridge Upgrade to Rescue Stuck Funds**

On 1st August 2024 Mode ran a planned upgrade to rescue 4880 ETH in funds sent to an incorrect L2 proxy address by Etherfi. \
\
[**Full post-mortem on the EtherFi github here.** ](https://github.com/etherfi-protocol/postmortems/?tab=readme-ov-file)\
[**Bridge upgrade transaction to rescue funds.** ](https://etherscan.io/tx/0x9154d2b581e84b15615b4a857476af9fa6b682622d6e30e7c28bae6331a5fe39)

**Overview**\
\
On May 8, 2024, Etherfi generated a proof using an incorrect messenger for withdrawals on the Mode Bridge \
\
Shortly after the event, the EtherFi team reached out to Mode and an initial proposal was made by Nethermind ([link](https://github.com/etherfi-protocol/postmortems/blob/master/1715209000-l2-l1-sync-misconfiguration/NM0243-ETHERFI-REPORT.pdf)) to rescue the funds. \
\
After multiple security reviews, Mode executed an upgrade to rescue the stuck funds and return them to Etherfi. The upgrade was successfully completed with minimal disruption to Mode Network. \
&#x20;\
**Why was this rescue not disclosed in advance?**&#x20;

There were concerns of making this rescue public due to the risk of the message not being finalized or a malicious actor sending a proof. After multiple security reviews we found a safer solution which bypassed these risks and executed this.&#x20;

**For further details see the** [**full post-mortem on the EtherFi github here.** ](https://github.com/etherfi-protocol/postmortems/?tab=readme-ov-file)

{% embed url="https://github.com/etherfi-protocol/postmortems/?tab=readme-ov-file" %}
