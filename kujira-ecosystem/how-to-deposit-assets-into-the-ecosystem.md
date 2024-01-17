---
description: How to deposit funds in the ecosystem
cover: ../.gitbook/assets/Kujira docs is for everyone (2).jpeg
coverY: 0
---

# Moving Funds to Kujira

There are several options available for moving funds to the Kujira blockchain. Depending on your level of experience with decentralized finance (DeFi) and where your funds are located, you can choose the most appropriate method for your needs.

### Option 1: Using a Fiat Onramp

If you are new to DeFi, it may be easiest to use a fiat onramp to move your funds to Kujira in one step. Kado and Local Money are two examples of fiat onramps that can be used to onramp funds to Kujira.

### Option 2: Migrating Terra KUJI

If you were a KUJI holder on Terra and held KUJI or sKUJI at 1:58 AM UTC on May 13, 2022 after the UST collapse, you can migrate your Terra KUJI to the Kujira network to receive a corresponding amount of native KUJI. We have a detailed migration guide available to help you through this process.

### Option 3: Bridging & Cross-chain Tools

If you are an experienced DeFi user, there are several bridging tools available that you can use to move your funds to Kujira. Some examples include Axelar, IBC, Squid, Maya, and Rango. Our detailed guide below breaks down the different options and provides more information on how to use these tools.

## On-Ramping Funds to Kujira

If you are new to cryptocurrencies, one easy way to move funds into the Kujira blockchain is to use a user-friendly on-ramping tool. These tools allow you to transfer funds directly from your bank account into the Kujira ecosystem. Below is a list of some of the easiest on-ramping tools for beginners to use:

### Kado Money

[Kado](../dapps-and-infrastructure/basics.md#funding-your-wallet-using-kado) is a platform that allows users to easily enter and exit the DeFi ecosystem without the need for a centralized exchange. It offers low fees and enables users to move between fiat and web3 directly from their wallets, as well as off-ramp from DeFi to their bank accounts. Kado believes in the importance of self-custody and aims to empower users to take control of their financial freedom.

### Local Money

[Local](https://localmoney.io/) is a decentralized P2P marketplace for the multi-chain world with fast and easy on-off ramps. Local Money enables peer to peer transactions that greatly reduces the burden of moving funds on or off chain. Created as a decentralized alternative built on the success of P2P giants Binance P2P, Localbitcoins, and LocalCryptos who have more than 10 million monthly visits–Local Money is set to expand crypto-fiat access.

## Migrating Terra KUJI to Kujira

If you held KUJI tokens on Terra Classic and held them during the snapshot (13th of May, 2022 at 1:58 AM UTC), you can migrate them to the Kujira blockchain by following the guide provided in this article. sKUJI holders will receive KUJI at a ratio of 1sKUJI = 1.228 KUJI. KUJI holders will receive KUJI at a ratio of 1 Terra KUJI = 1 Kujira KUJI. LPers will need to reach out directly to Jan or Alex for assistance.&#x20;

[https://medium.com/team-kujira/migration-to-kujira-mainnet-cc04d88da338](https://medium.com/team-kujira/migration-to-kujira-mainnet-cc04d88da338)

## Bridging & Cross-chain Tools

Experienced users with funds already in DeFi

### Gravity Bridging

The Gravity Bridge is a purpose-built, fully decentralized, trustless blockchain which bridges assets between the Ethereum and Cosmos ecosystems. Ethereum and EVM compatible tokens can be transferred across the Gravity Bridge to a Cosmos wallet and then onto other Cosmos wallets or DEXs (such as FIN or Gravity DEX). Cosmos SDK based blockchains can similarly send tokens across Gravity Bridge to the Ethereum ecosystem, making them available for transfer or potentially trading on Uniswap or other ETH DEXs. [https://bridge.blockscape.network/](https://bridge.blockscape.network/)

### Axelar Bridging

The Axelar Bridge is a decentralized network that enables cross-chain communication and asset transfers between different blockchain networks. It utilizes Gateway smart contracts, validators, and relayer servers to facilitate cross-chain transactions and pass messages between chains. The Axelar Bridge aims to provide a secure and efficient way for users to access a wider range of assets and utilize the benefits of the Axelar network, including low fees and improved trade execution. [https://satellite.money/](https://satellite.money/)

#### Bridging to the Kujira Ecosystem

The Kujira ecosystem offers several options for bridging assets from other networks to Kujira mainnet. This allows users to access a wider range of assets and take advantage of the benefits of the Kujira ecosystem, such as low fees and improved trade execution.

Here is a step-by-step guide to the bridging process:

1. Go to[ https://blue.kujira.app/bridge](https://blue.kujira.app/bridge).
2. Connect your Keplr wallet and configure the bridge to show the network where you currently have your axlUSDC (Avalanche, Polygon, or Fantom) on the left, and axlUSDC on the right.
3. Click "Connect Wallet" next to "Source Balance" and approve the popup on MetaMask.
4. Input the amount of axlUSDC you wish to migrate to Kujira, remembering to have some AVAX/MATIC/FTM for fees. You'll need to pay both a bridge fee and the normal gas fee to transfer between wallets.
5. Click "Initiate Bridge". Once a deposit address has been created, the "Initiate Bridge" button should change to say "Sign and Send". Click this and approve the transaction to finish the bridging process.
6. Bridging can take up to 5 minutes to complete, so you can track the progress by clicking the text in the green box.

If you have native USDC on Ethereum, you can bridge it to Kujira mainnet by following the same steps as above, but configuring the left side of the bridge to show "Ethereum" instead.

Alternatively, you can deposit USDC directly from a centralized exchange (CEX) into Kujira. To do this, navigate to the "Crosschain Bridge" section of the bridging page and follow the steps

### Nomic Bridging

The Nomic bridge is a design for a Bitcoin sidechain that enables decentralized networks to manage reserves of Bitcoin and use custom application code and smart contracts. It uses the Tendermint consensus protocol and timestamps the sidechain on the Bitcoin blockchain for security and BFT finality. It also includes mechanisms to prevent loss of funds and disincentivize malicious behavior.

### IBC Bridging

The Inter-Blockchain Communication (IBC) Protocol allows blockchains to communicate with each other and exchange data about state or transactions. It is particularly useful for application-specific blockchains in the Cosmos network and offers a standardized way for applications on different chains to communicate. IBC is a permissionless way to relay data packets between blockchains and relies on the security of the participating chains. It is much more secure than traditional bridging methods.&#x20;

[Here](https://winkhub.app/posts/depositing-funds-to-kujira#Cosmos-Chains) is a quick guide on how to use IBC to bridge assets to the Kujira ecosystem.

### 0xSquid

Squid is a protocol for cross-chain swaps and liquidity routing on the Axelar Network. It enables the easy exchange of any native token between different chains and can be used with custom smart contracts. It connects all applications and users on all chains with a single click and is built on top of the Axelar Network, which allows for secure communication and execution of any action between any chain.

### Maya Protocol

Maya Protocol is a powerful cross-chain DEX. MAYAChain is a cross-chain AMM that facilitates cross-chain swaps without the need for bridging or wrapped assets. Maya is a powerful tool for empowering KUJI and USK decentralized self-custody swaps to and from native BTC, ETH, USDT (ERC20), USDC (ERC20), RUNE, DASH and more upcoming assets. This allows for secure asset onboarding without ever needing to use a centralized exchange.&#x20;

### Rango

Rango is a multi-chain DEX and bridge aggregator that facilitates the transfer of funds between different blockchains. Integrated with Kujira, Rango empowers blockchain users on many different chains to efficiently and smoothly transfer assets from Kujira to other networks and vice-versa.
