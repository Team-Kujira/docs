# Core Module Accounts

There are a few "Core Module" accounts on the Kujira Blockchain. These are created by modules within the Cosmos SDK and our own bespoke modules. Generally they are of little significance when building on the chain, but a few such as `fee_collector` are critical to the operation of the chain.&#x20;

## fee\_collector

[kujira17xpfvakm2amg962yls6f84z3kell8c5lp3pcxh](https://finder.kujira.app/kaiyo-1/address/kujira17xpfvakm2amg962yls6f84z3kell8c5lp3pcxh?p=1)

This account acts as the collection point for all 3rd part fee on the Kujira network. FIN, USK, Orca, and all other protocols send tokens to this address. From here, they're pased to the `distribution` module, which distributes them amongst validators and stakers

This is used frequently enough in smart contracts that it's available in `kujira-rs` at `kujra::utils::fee_address()`

## gov

[kujira10d07y265gmmuvt4z0w9aw880jnsr700jt23ame](https://finder.kujira.app/kaiyo-1/address/kujira10d07y265gmmuvt4z0w9aw880jnsr700jt23ame?p=1)

This is the address of the governance module. If you need to set privileged actions on your contract that can only be called from a governance proposal, use this address. Alternatively, you may find the `sudo` entrypoint more suitable.

In general, contracts should be instantiated with the `gov` module as the `admin` parameter, to ensure that subsuequent code changes are subject to the same governance process as the initial instantiation.&#x20;

##
