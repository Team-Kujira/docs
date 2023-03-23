# 🖨 How to Mint USK

## [https://blue.kujira.app/mint](https://blue.kujira.app/mint)

## Overview

This section explains some basics around minting USK and managing collateral positions as well as keeping track of them. At the moment, the easiest way to mint USK is to use the [BLUE](../blue/) application user interface linked above. It is also possible to open margin positions using i[solated FIN margin](../fin/how-to-use-fin/spot-and-margin-trade-ui/isolated-fin-margin.md#overview) which effectively [mints USK in reverse](../fin/how-to-use-fin/spot-and-margin-trade-ui/isolated-fin-margin.md#mechanism).

There are a few different steps involved in minting USK, but the process has been streamlined via conveniences such as Squid, Gravity Bridge, the BLUE UI, and Sea Shanty to make it as simple as possible. The first is obtaining compatible collateral that is allowed as a backing asset for USK, the second is supplying the collateral and minting a corresponding amount of USK, the third is managing the health of the collateral debt position (CDP) over time and accounting for any interest accrued over time.

## Step 1: Selecting USK collateral&#x20;

Kujira governance is extremely active bringing constant evolution to the Kujira blockchain. As a result, new USK collateral can be added relatively quickly. One way to stay on top of possible options for minting USK is to look at the USK collateral dashboard at the bottom of the page on [blue.kujira.app](https://blue.kujira.app) or directly look through all the available collateral types using the [blue.kujira.app/mint](https://blue.kujira.app/mint) user interface.

The first step of the USK mint process is to select preferred backing collateral. After all, minting USK is akin to a leveraged bet on the provided collateral. USK is programmatically coded to be 166% collateralized. As a result, any mint positions backed by underlying collateral also need to be 166% collateralized and cannot have too much downside volatility to avoid being liquidated via [ORCA](../orca/).

It is important to select backing collateral that you are confident in over the duration of opening a USK mint position. There are three main considerations: performance & volatility, ease of acquiring and/or bridging over to Kujira, and security.&#x20;

A first consideration is the price performance and volatility of the collateral. Some backing collateral such as wETH, wBNB are long established tokens that appear likely to remain relatively more stable over time throughout the volatility of decentralized finance. On the other hand, collateral tokens such as ATOM, DOT, LUNA may have substantially more upside in a strong market. This can create a larger safety net for provided collateral against liquidations (but on the flipside is riskier in a weak market). At the same time, backing collateral such as gPAXG is based around the price of gold which has been quite stable over time.

A second consideration is the ease of acquiring the collateral and/or bridging it over to Kujira. Purchasing collateral on FIN removes the need to bridge it over. However, for existing holders of various USK collateral compatible assets, it is necessary to first bridge those assets over to the Kujira blockchain to use them to mint USK. Assuming familiarity with a collateral option that has satisfactory price performance and volatility, ideally it should be easy to acquire and bridge over to Kujira. Squid Router (an application built on the Axelar Network) has made it possible to bridge various assets such as wETH and wBNB over to Kujira in just one click. Gravity Bridge has also made it possible to bridge USK and KUJI to Ethereum and also PAXG (a gold backed digital asset) to Kujira.

One last consideration is the security of the USK backing collateral. LUNA, ATOM, and other Cosmos tokens are bridged over to Kujira using IBC. Tokens from other chains such as wBNB and wETH rely on the bridge provider (in this case Axelar) or gPAXG which is facilitated by Gravity Bridge. How effective are the entities behind the tokens themselves, etc. Generally, the attractiveness of the USK mint value proposition derives from the underlying benefits from the unlocked direct access to cutting edge financial applications and services on Kujira.

Assuming those three considerations are satisfactory, then a specific collateral or multiple collaterals can be selected to mint independent USK collateral debt positions. All USK debt positions minted using the same collateral type by the same wallet are consolidated into one overall mint position unlike when using different backing collateral types. The next step in the process is depositing the backing collateral in the BLUE UI and minting USK.

## Step 2: Depositing collateral and minting USK

The second step in the USK mint process is to interact with the BLUE mint user interface [blue.kujira.app/mint](https://blue.kujira.app/mint), deposit collateral(s) chosen in step 1, and mint a corresponding amount of USK. Detail steps about how to use the mint user interface can be found in the '[How to Mint USK](../blue/product-guides/how-to-mint-usk.md)' product guide and a short synopsis about the mint tab can be found in the BLUE '[Mint](../blue/mint.md)' entry.

The main gist of the process is to navigate to the part of the page where to deposit collateral, then provide a selected amount of that collateral and pay gas fees. The next action is the most important part of step 2, choosing an amount of USK to mint.&#x20;

As explained in the '[Technical Specifics](technical-specifics.md)' section, USK must be 166% collateralized at all times by design. As part of ensuring that USK is fully overcollateralized, if backing collateral used to mint USK ever goes below the 166% collateralization ratio, it will start to be liquidated on Kujira's public liquidation marketplace ORCA. Therefore, as part of avoiding liquidation of provided collateral, it is important to choose to mint an amount of USK that preserves a healthy collateral debt position risk ratio. Read more [here](technical-specifics.md) about risk ratios and how they work. The maximum allowed risk ratio is 100% before liquidation begins. Therefore, it is recommended based on user specific risk tolerance to account for expected collateral price volatility and plan accordingly by leaving sufficient leeway to avoid liquidation if the backing collateral's price suddenly drops. Kujira's price oracles are robust aggregating price data from all 75 active validators who all use 3 different exchanges as a source to prevent price manipulation. Read more [here](../../developers/smart-contracts/oracle.md). &#x20;

After selecting a healthy amount of USK to mint, it is then straightforward to follow the 'How to Mint USK' product guide to mint the USK and finish step 2 of the process. Note that when minting USK, 0.1% of that minted USK is kept by BLUE as a mint fee and distributed out to all KUJI stakers.

## Step 3: Managing the health of the CDP over time

The final step in the USK mint process actually occurs after the initial USK mint has finished. For as long as that minted USK remains in circulation, the provided backing collateral acts as a collateral debt position (CDP) for that minted USK and is subject to 1% in yearly interest and possible liquidation assuming the backing collateral price falls too far and the CDP risk ratio rises over 100%. &#x20;

As such, since all USK minted by the same backing collateral with the same wallet is aggregated into the same CDP as mentioned above, new backing collateral can always be added to the position to lower the risk ratio. At the same time, if the collateral is performing very well, and the risk ratio goes low, it may make sense to reevaluate and mint more USK using the same CDP. Minted USK can be utilized across a variety of [use cases](use-cases.md) in the Kujira ecosystem which will only expand over time. At times it may also make sense to burn some minted USK to reduce your CDP risk ratio.

[Sea Shanty](../../governance/capybara-labs.md)'s bot provides real time updates on user mint collateral debt positions. Available on Telegram, it provides an easy way to view USK mint position amount and risk ratio at any time on mobile or desktop. Sea Shanty does not have access to provided wallets, it simply reads public blockchain information based on provided wallet address details.         &#x20;



