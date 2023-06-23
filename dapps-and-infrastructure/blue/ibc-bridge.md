---
description: Transferring assets to and from Kujira
---

# 🌐 IBC / Bridge

## Overview

The IBC / Bridge tab has 4 further subtabs that allow users to perform different activities: using IBC, using the Axelar Bridge, using the Gravity, Bridge, and using the Nomic Bitcoin bridge.

## IBC Tab

[https://blue.kujira.app/ibc](ibc-bridge.md#https-blue.kujira.app-ibc) or [https://blue.kujira.network/ibc](ibc-bridge.md#https-blue.kujira.app-ibc-or-https-blue.kujira.network-ibc)

The Inter-Blockchain Communication (IBC) Protocol allows blockchains to communicate with each other and exchange data about state or transactions. It is particularly useful for application-specific blockchains in the Cosmos network and offers a standardized way for applications on different chains to communicate. IBC is a permissionless way to relay data packets between blockchains and relies on the security of the participating chains.

Migrating assets between two IBC powered chains (chain A and chain B) takes two steps. First, withdraw an asset from chain A to its home chain--for example, ATOM on Terra must be bridged to the Cosmos hub. Next, deposit the asset from the home chain into chain B--for example, use the BLUE IBC tab to move ATOM from the Cosmos hub to the Kujira blockchain.

Therefore, the BLUE IBC page allows users to deposit any IBC compatible asset from its home chain to Kujira or withdraw it from Kujira to its home chain using a simple UI. Read more [here](https://docs.kujira.app/dapps-and-infrastructure/blue/product-guides/how-to-use-ibc).&#x20;

## Bridge Tabs

### Axelar Bridge Tab

[https://blue.kujira.app/bridge](ibc-bridge.md#https-blue.kujira.app-bridge) or [https://blue.kujira.network/bridge](ibc-bridge.md#https-blue.kujira.app-bridge-or-https-blue.kujira.network-bridge)

The Axelar Bridge is a decentralized network that enables cross-chain communication and asset transfers between different blockchain networks. It utilizes Gateway smart contracts, validators, and relayer servers to facilitate cross-chain transactions and pass messages between chains. The Axelar Bridge aims to provide a secure and efficient way for users to access a wider range of assets and utilize the benefits of the Axelar network, including low fees and improved trade execution. [https://satellite.money/](https://satellite.money/)

All compatible assets other than axlUSDC can be bridged over to Kuijra from compatible chains using the Axelar Bridge BLUE tab. To bridge axlUSDC into or out of Kujira, use [https://satellite.money/](https://satellite.money/) for the process.

### Gravity Bridge Tab

[https://blue.kujira.app/gravity](ibc-bridge.md#https-blue.kujira.app-gravity) or [https://blue.kujira.network/gravity](ibc-bridge.md#https-blue.kujira.app-gravity-or-https-blue.kujira.network-gravity)

The Gravity Bridge is a purpose-built, fully decentralized, trustless blockchain which bridges assets between the Ethereum and Cosmos ecosystems. Ethereum and EVM compatible tokens can be transferred across the Gravity Bridge to a Cosmos wallet and then onto other Cosmos wallets or DEXs (such as FIN or Gravity DEX). Cosmos SDK based blockchains can similarly send tokens across Gravity Bridge to the Ethereum ecosystem, making them available for transfer or potentially trading on Uniswap or other ETH DEXs. [https://bridge.blockscape.network/](https://bridge.blockscape.network/)

At the moment, the Gravity bridge can be used to bridge PAXG (Paxos Gold, a cryptocurrency fully backed by gold) from Ethereum to Kujira as gPAXG.&#x20;

### Nomic Bridge Tab

[https://blue.kujira.app/nomic](ibc-bridge.md#https-blue.kujira.app-nomic) or [https://blue.kujira.network/nomic](ibc-bridge.md#https-blue.kujira.app-nomic-or-https-blue.kujira.network-nomic)

The Nomic bridge is a design for a Bitcoin sidechain that enables decentralized networks to manage reserves of Bitcoin and use custom application code and smart contracts. It uses the Tendermint consensus protocol and timestamps the sidechain on the Bitcoin blockchain for security and BFT finality. It also includes mechanisms to prevent loss of funds and disincentivize malicious behavior.

Nomic Bridge BLUE usage is currently limited to testnet.&#x20;

