# 🥩 Staking

Staking is a core component of the Kujira blockchain. It is also a fundamental aspect driving KUJI's underlying value proposition which can be read more about [here](staking-overview.md). It is also an important part of securing the Kujira blockchain that revolves around bonding KUJI to specific validators.

Before diving deeper into Staking, it first helps to discuss Kujira blockchain consensus.&#x20;

### Consensus

As a proof of stake blockchain, the Kujira network is secured by a verification system called the Tendermint Consensus and is powered by the [Cosmos SDK](https://cosmos.network/).&#x20;

The following sequence of steps gives a simple breakdown of Tendermint Consensus works:

1. A validator called a proposer is chosen to submit a new block of transactions.&#x20;
2. Validators vote in two rounds on whether they decide to accept or reject the proposed block. If it is rejected, a new proposer is selected and the process restarts.&#x20;
3. If accepted, the block gets signed and is added to the chain.&#x20;
4. Transaction fees and gas fees from the block are distributed to the Treasury and to validators and delegators as staking rewards. Proposers are rewarded extra for their participation.&#x20;

As this process repeats, new blocks are added to the chain. Each validators contains a copy of all transaction that are made on the Kujira network, which is compared against the proposed blocks of transactions before voting. Multiple independent validators participate in consensus voting, which makes it infeasible to accept false blocks. This allows validators to secure the Kujira blockchain and ensure the validity of each transaction.

A more detailed explanation on Tendermint consensus can be found [here](https://docs.tendermint.com/).
