# Slashing

Running a validator is an important responsibility. Validators must meet strict standards and constantly monitor the network and participate in [consensus](./#consensus). Validators that misbehave and fail to meet these standards are slashed as a penalty.

**When a validator is slashed, they lose a small portion of their self-staked KUJI as well as a small portion of their delegators' stakes.** Slashed validators are jailed and excluded from securing the network until they take appropriate action to unjail themselves. While validators are jailed, they cannot be slashed any further and this gives them time to gather their bearings while minimizing any damage to their delegators.

Slashing occurs under each of the following circumstances:

**Double Signing**: A validator signs two different blocks with the same chain ID at the same height

Make sure validators you delegate to are protected against Double Signing. This suffers the most severe slashing penalty of 5% of the validator's and each delegator's staked positions.

**Downtime**: A Validator cannot be reached and is unresponsive for a period of time.

This can happen to interruption of service. This receives a less severe slashing penalty of 0.01% of the validator's and each delegator's staked positions.

**Missed votes**: Validators must vote as part of Kujira blockchain consensus.

Validators on the Kuijra network may miss votes on Kujira price oracles, for example. It is important to stake with validators that minimize any missed votes. This also receives a less severe slashing penalty of 0.01% of the validator's and each delegator's staked positions.
