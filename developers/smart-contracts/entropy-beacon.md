# Entropy Beacon

We give a big thanks to [Entropic Labs](https://entropiclabs.io/beacon/) who are bringing cryptographically verifiable on-chain randomness to Kujira.

Their Entropy Beacon is a decentralized source of randomness for blockchain developers that provides secure random number generation in trustless on-chain environments, the first to do so on Cosmos based blockchains.&#x20;

Let's cover a few main aspects of the Entropy Beacon below:

### On-chain Entropy&#x20;

It is currently impossible to generate completely unpredictable random numbers on-chain. Beacon intends to provide a secure, unpredictable, cheap random number generator.

### Free Submissions

When smart contracts need on-chain entropy, they request it from the Beacon. Off-chain workers pick up the request, generate it, and call the Beacon contract. At this point, the Entropy Beacon uses gas to call the callback function on the requesting contract. Kuijra has set up a feegrant paid from a protocol wallet to incentivize off-chain workers to call the function and cover Beacon gas fees. As a result, protocols consuming randomness do not need to take on any extra fees or pass them to users.

### Streamlined Development

Beacon provides the most comfortable developer experience of any existing randomness solution, with no complex tokenomics and subscription models, and an ergonomic API for interacting with the system.

### Enabling Next-Gen dApps

An on-chain entropy beacon opens up hundreds of previously unachievable usecases. Lottery systems, tamper-proof giveaways, complex DeFi games, and countless others all require the decentralized generation of secure random numbers.

### How it works

Beacon uses VRF Cryptography to enforce generated random numbers are verifiably unbiased. A more detailed explanation can be found[ here](https://entropiclabs.io/beacon/docs/how-it-works/) in Entropic Labs' docs.

### Quickstart

For developers looking to develop contracts that utilize the Entropy Beacon, Entropic Labs' docs have a substantive explanation covering everything you need to know from start to finish right [here](https://entropiclabs.io/beacon/docs/quickstart/).

### Integration

Furthermore, for developers looking to integrate the Entropy Beacon into existing smart contracts, Entropic Labs' docs also have a substantive explanation on this topic that you can find [here](https://entropiclabs.io/beacon/docs/integration/).&#x20;

### Mainnet Address

Entropy Beacon's mainnet address is [kujira1x623ehq3gqx9m9t8asyd9cgehf32gy94mhsw8l99cj3l2nvda2fqrjwqy5](https://finder.kujira.app/kaiyo-1/contract/kujira1x623ehq3gqx9m9t8asyd9cgehf32gy94mhsw8l99cj3l2nvda2fqrjwqy5)

### Helpful Links

More information can be found on Entropic's [Github](https://github.com/EntropicLabs), [Twitter](https://twitter.com/Entropic\_Labs), and [Discord](https://discord.com/invite/Qp9ZcZJnKC).



