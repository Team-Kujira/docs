# Staking UI

At Kujira, we have created a custom [staking UI](../../dapps-and-infrastructure/blue/stake.md) to support network decentralization on proof of stake (PoS) blockchains. The degree of decentralization on a PoS blockchain can be determined, in part, by the Nakamoto coefficient. This coefficient represents the smallest number of validators that could potentially collude and take control of the network. A more uniform distribution of validator delegations leads to a higher Nakamoto coefficient and increased decentralization.

It is not uncommon for individuals to assume that validators with larger delegations are inherently superior and therefore the best choice for delegating. However, this can create security issues and hinder decentralization, as the values and actions of these validators may not align with the delegator's own.

To address this, our staking UI includes visual indicators to help users make informed decisions about which validators to delegate to. Validators with voting power exceeding the equal power threshold (indicating a more centralized distribution) are highlighted in red, while those with medium voting power are highlighted in yellow. Validators with voting power below the equal power threshold (indicating a more decentralized distribution) are highlighted in blue.

In addition, the staking UI includes an "optimize" feature. When you enter the amount of KUJI you want to stake and select optimize, the UI will automatically select all the blue validators (those with voting power below the equal power threshold) that are safe to delegate to in order to bring the network closer to a uniform staking distribution. While this is a convenient option, users are also welcome to research and select validators that align with their own values.

We will continue to improve the staking UI based on user feedback and innovation. An extended version of this UI that applies to all Cosmos network chains can also be found.
