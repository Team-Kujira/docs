# 🏛 Govern

## Overview

The Govern tab on BLUE allows users to interact with Kujira Governance. Nominate Senators; track, vote, or change your vote on active governance proposals; review the specifics of old governance proposals including how validators and users voted and the breakdown of overall votes between yes, no, abstain, and no with veto; or review the Treasury (Community Pool).

For the time being, Governance proposals can be assigned to two discrete categories: Senate and Chain Governance. Senate proposals relate in essence to the expenditure of community funds on projects wishing to launch on Kujira, public initiatives for the Kujira blockchain, public infrastructure, and other miscellaneous services which require community funding. Chain Governance is everything else, but can be thought of more specifically as a category encompassing all technical upgrades to the chain.  &#x20;

## Senate

[https://blue.kujira.app/senate](govern.md#https-blue.kujira.app-senate-or-https-blue.kujira.network-senate) or [https://blue.kujira.network/senate](govern.md#https-blue.kujira.app-senate-or-https-blue.kujira.network-senate)

This tab has the Kujira senators listed each with links to their keybase.io. It is also possible to nominate Senators on this tab. Furthermore, there is a [link](https://medium.com/team-kujira/kujira-governance-grows-up-ca8b7c87753b) to reading more about the role of the Senate. More up to date information can also be found in the Senate [section](../senate.md) of the docs.

On the right side of the page, there is a detailed breakdown of the Senate Treasury (Community Pool) in terms of every asset and the amount of each asset in the Treasury wallet as well as the current total dollar value of the fund. Furthermore, there is a link to the wallet address on FINDER on the bottom right for the sake of transparency.&#x20;

In the future, it will be possible to submit Senate grant proposals on the BLUE senate tab. Senate proposals will take up to 2 weeks of review, but may pass sooner as long as at least 6 senators vote yes on a proposal. The result will automatically be a no if consensus is not achieved within that period.

## Sentinel

[https://blue.kujira.app/sentinel](govern.md#https-blue.kujira.app-sentinel-or-https-blue.kujira.network-sentinel) or [https://blue.kujira.network/sentinel](govern.md#https-blue.kujira.app-sentinel-or-https-blue.kujira.network-sentinel)

The Kujira Sentinel is a technical companion to the Senate. By providing the CW4 multisig contract address with chain-wide contract instantiate permissions, Sentinel creates better development velocity and autonomy for protocol builders, without sacrificing security.&#x20;

Furthermore, by delegating contract instantiation permissions to a multisig of a select group of trusted technical experts, deployed code can be assessed and verified more rigorously than is currently possible with global governance deployments.

Long-term, the Kujira Sentinel will create a foundation for a peer-led audit and review process, significantly reducing the cost to teams launching new protocols, a competitive edge for Kujira.

## Chain Governance

[https://blue.kujira.app/govern](govern.md#https-blue.kujira.app-govern-or-https-blue.kujira.network-govern) or [https://blue.kujira.network/govern](govern.md#https-blue.kujira.app-govern-or-https-blue.kujira.network-govern)

Governance proposals are submitted by members of the Kujira community and can cover a wide range of topics, including updates to the Kujira platform, changes to network parameters, and new features or services. These proposals are discussed and debated in the Kujira community, and then put to a vote for approval or rejection.

By staking KUJI, anyone can help shape the future of Kujira by submitting or voting on governance proposals. Governance proposals are typically voted on in the form of chain governance polls. There are multiple phases to chain governance.&#x20;

The first phase is the initial deposit phase. Once a proposal is submitted, there is a 24-hour deposit window during which a threshold of 10,000 KUJI must be reached from the proposer's wallet or any other community member's wallet in order for the proposal to be deposited on-chain and the voting period to begin. The KUJI tokens deposited must be liquid (not staked) and will be returned to the wallet after the threshold is met. If the threshold is not met during the deposit period, the deposited tokens will be burned. Refer [here](https://docs.kujira.app/governance/submit-a-proposal) for more details.

The second phase is the voting phase. Once a proposal achieves a sufficient deposit within 24 hours, the 48 hour voting period immediately begins. If delegators do not vote on a proposal, their vote will be deferred to their staked validator(s). So is it best to choose trusted validators with aligned interests. For a proposal to pass governance, three conditions must be met within 48 hours:

* At least 33% of staked KUJI must actively vote on the proposal either yes, no, no with veto, or abstain.
* At least 50% of the total non-abstain votes yes. Alternatively, the yes percentage of the total vote must be higher than the no and no with veto percentages of the total vote combined. Votes are weighted based on amount of KUJI staked on a 1 to 1 basis.
* Finally, fewer than 33% of votes may be no with veto. No with veto is reserved for bad faith proposals and and a no with veto percentage over 33% burns the proposer's 10K KUJI deposit at the end of the voting period.&#x20;

Finally, at the end of the voting period the vote passes. Read more [here](https://docs.kujira.app/governance/vote-on-proposals).&#x20;

The Chain Governance tab allows anyone to browse through past governance proposals, observe which validators or wallets voted in a certain and/or reasons for their votes, as well as the overall results (the percentage breakdown of yes, no, abstain, no with veto). The Kujira Discord has a governance forum meant for discussing regular chain governance proposals. Read more [here](../../governance/discord-governance-forum.md).&#x20;



