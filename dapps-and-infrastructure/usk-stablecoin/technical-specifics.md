---
cover: ../../.gitbook/assets/usk docs test.png
coverY: 0
---

# Technical Specifics

## Overview

This entry is meant to provide a detailed technical explanation for all of USK's underlying mechanics including the collateral debt position mechanism, backing composition, minting process,  liquidation process, price stability, and payment aspects.&#x20;

As explained in the main USK header entry as well as the basics section, USK is Kujira's native decentralized stablecoin that is _softpegged_ to the US dollar. Holding USK opens up the opportunity to use and make the most of financial services exclusive to Kujira and affiliated products and services. USK can be acquired by minting it on [BLUE](../blue/) or purchasing it on [FIN](../fin/). [SONAR](../kujira-wallet/) will soon be the best USK experience (holding, buying, selling, paying, sending, and new Kujira specific financial functionalities).

On a basic level users can provide collateral to mint USK for a 0.1% fee and can burn USK at any time with no penalty to redeem their collateral. Provided collateral acts as a guarantee ensuring that minted USK is fully overcollateralized at a minimum of 166% total collateralization. When the value of backing collateral falls below 66% overcollateralization, the backing collateral is liquidated in [ORCA](../orca/) via USK bids, 99% of which get burnt at the time. The remaining 1% of filled ORCA USK bids is distributed to KUJI stakers along with the accumulated 1% borrow interest which is also distributed to stakers in the liquidated collateral asset.&#x20;

## Collateralized Debt Position Mechanism&#x20;

USK is backed by valuable compatible crypto assets sitting on BLUE smart contracts that are essentially available to redeem (or burn) USK. Like a blockchain version of the gold standard and unlike modern banking, USK is not printed out of thin air and is backed at over 166% capacity.

As part of USK's crypto-collateralized model, it is minted by locking crypto collateral on smart contracts. The smart contracts are called collateralized debt positions (CDP) and is the only way new USK can enter the supply.

Essentially, in this process loans are made with the smart contracts to mint USK. USK is "borrowed" by locking up collateral in the smart contracts. Ownership of the collateral is retained, but the collateral is temporarily locked behind debt and can only be retrieved by paying back the debt. This is not so different from a mortgage which uses a house as collateral from a bank to take out a loan. Ownership of the house is retained, but the bank has a lien on it.&#x20;

One measure of how collateralized a debt position is the loan-to-value (LTV) ratio which measures the amount of USK borrowed versus the total amount of collateral supplied. The ratio between the two i.e. $$\frac{\text{amount of USK borrowed i.e. minted}}{\text{amount of backing collateral provided}}$$is known as the collateral debt positions' LTV. As the value of the backing collateral decreases due to volatility in the underlying asset, the LTV increases showing the deteriorating health of that debt position. Beyond a certain point, a position is said to be too risky and gets automatically liquidated via ORCA.&#x20;

The risk ratio is another concept often used to illustrate the health of a collateralized debt position. Risk ratio can be instead thought of as $$\frac{\text{amount of USK borrowed i.e. minted}}{\text{amount of backing collateral provided}}\times\frac{1}{\text{Max allowed LTV}}$$. This is a more useful measure because while different assets may hypothetically have their own maximum allowed loan-to-value ratio based on that assets' specific characteristics, risk ratio is a unified concept that doesn't need to be aware of that maximum LTV to be useful.

For example, suppose that the maximum allowed LTV is 60% for wBNB supplied to mint USK. In that case, the risk ratio is the current LTV divided by the maximum possible allowable LTV before liquidation occurs and is always a number between 0% and 100%. The risk ratio shows that a collateral debt position reaches the point of liquidation at a risk ratio of 100%, no matter the maximum allowed LTV--therefore it is a convenient generalized measurement of CDP health.  &#x20;

## Backing Composition&#x20;

USK collateral composition is decided by Kujira community governance. At the moment, the community has been ensuring diverse USK mint caps uniquely tailored to each backing collateral type to ensure proper diversification of USK backing funds in case of a black swan. The strategy has been working well so far as USK experienced essentially zero volatility throughout the FTX crisis.

The specific backing composition breakdown can be analyzed in real time via either the [dashboard](../bow/dashboard.md) on [blue.kujira.app](https://blue.kujira.app/) or directly via [blue.kujira.app/mint](https://blue.kujira.app/mint). At the moment, USK is backed by various collateral types including ATOM, wrapped ETH, wrapped DOT, wrapped BNB, LUNA, MNTA, and bridged PAXG that are sitting in smart contracts on Kujira which can essentially be used to redeem USK at any time. Mint cap sizes correspond to the perceived stability of backing collateral. As the supply of USK grows, mint caps will be grown accordingly. Nomic Bridge Bitcoin, nBTC, is planned to be a supported collateral option once it releases later this month.

## Mint Process

The user mint process using BLUE is explained in substantial detail in the '[How to Mint USK](how-to-mint-usk.md)' entry. This is meant to be a more technical explanation of the mint process and what each step entails.&#x20;

The actual USK mint process occurs by providing valuable (compatible) crypto assets as backing collateral and selecting an amount of USK to mint. This opens a new USK mint position which charges 1% yearly APR in stability fee interest while it remains open. This interest slowly increases the mint position risk ratio over time although the increase is capped yearly by the maximum yearly change. Interest is paid in full at the time of either winding down a USK collateral debt position or having the backing collateral liquidated due to market volatility and insufficient risk management. Furthermore, there is a 0.1% mint fee that is taken off the amount of minted USK and dispersed as another revenue stream to KUJI stakers.&#x20;

All USK positions by the same wallet that use the same backing collateral type are treated as one aggregate position. USK debt positions generated by different backing collaterals are always treated as separate (rather than combined) positions no matter whether they were performed by the same wallet address. &#x20;

## Liquidation Process

The USK liquidation process leverages ORCA, Kujira's original proven flagship product. As explained above, USK is minted or borrowed by depositing collateral that is temporarily locked up in smart contracts on Kujira until that minted USK is eventually redeemed by that wallet address. All USK collateral debt positions currently have a maximum allowable LTV of 60%. This means that when the ratio of minted USK to backing collateral exceeds 60%, some of the collateral will be liquidated via ORCA leading to some USK being burnt which preserves full USK overcollateralization. The current risk ratio of aggregate active USK debt positions for each collateral type can be observed in corresponding ORCA markets under the [analytics](../orca/basics/lending-markets/analytics.md) section. Furthermore, ORCA alerts have been added to 1st party Kujira applications to inform users of USK collateral that is currently at over 95% risk ratio and possibly at risk of near immediate liquidation.&#x20;

To understand the process of bidding on USK collateral using USK, the simplest method is to read through the [lending markets](../orca/basics/lending-markets/) and [USK lending markets](../orca/basics/lending-markets/usk-lending-markets/) entries in the ORCA subsection of Kujira's docs to get a basic understanding of how ORCA liquidations work. Specifically, for USK collateral markets, when the collateral is liquidated, bids to liquidate that collateral (i.e.. to purchase it at a discount or at a specific premium) are made using USK. A majority of the USK from filled ORCA bids is burnt and 1% of the liquidated collateral is sent to KUJI stakers along with the accumulated collateral debt position borrow interest. This accumulated 1% yearly borrow interest is distributed to stakers in the form of the provided collateral rather than as USK.&#x20;

## Price Stability

In an effort to be decentralized, USK avoids using a centralized price stability module. Rather, price stability is achieved via a variety of mechanisms.&#x20;

Hard pegged stablecoins are directly exchangeable for a specified quantity of the asset they are pegged to and maintain a permanent, fixed ratio. On the other hand, USK is softpegged to the US Dollar which means that USK will deviate in value within a range around 1 USD over time. Price stability is achieved by guiding human behavior using well-designed psychological incentives for performing certain actions.

One part of what makes the USK price stable is the possible arbitrage between the USK price on FIN and the USK CDP contract which consistently values USK as if it were exactly worth $1. This prevents borrow positions from seeing increased risk ratios as the price of USK goes up.

When the price of USK is over $1, it is possible to deposit collateral into the CDP, mint USK, and arbitrage it using FIN pairs to buy other assets (or stablecoins) at a discount. Eventually, once USK price drops back to the dollar peg from accumulated USK mint sell pressure, depositors can then buy back USK on FIN to profit.

At the same time, if USK falls below $1, since collateral providers need to redeem USK to recover their locked collateral (and as it is fully backed), they have an incentive to scoop up USK at a premium, but others also have an incentive to front run them as minters would eventually need the USK to exit their mint positions. This aggregate USK buying pressure combined with decreased incentives to mint USK because of reduced borrow against the CDP returns the price of USK back to $1 over time. &#x20;

On ORCA, the value of 1 USK is always treated as if it were equal to 1 USD. This not only keeps the liquidation settlement mechanism running smoothly in all situations, but also serves to further decrease USK demand when it is worth more than a dollar and increase USK demand when it is valued at less than a dollar. Furthermore, as the CDP USK price is fixed at $1, this also means that when USK falls in price, the backing collateralization ratio strictly increases.

There are other inbuilt mechanisms that help stabilize and influence the USK price as well. For example, the mint fee can be increased or decreased to disincentive or incentivize minting as needed to contract or expand the USK supply. The stability fee or borrow interest APR can also be changed to control corresponding USK demand. Finally, the percentage of USK burnt upon liquidation can also be lowered and the percentage of USK disbursed to stakers increased.

As is, as CDP liquidated collateral is purchased at a 30% premium at maximum, over time USK should actually be more than 160% backed, as more USK is burnt than then the amount of backing collateral liquidated from the CDP that would be need to be present to mint that much USK.

In the near future, there will be even more mechanics that help keep the USK price stable and accurate to the 1 USD soft peg.&#x20;

Recently, a new experimental Kujira BOW algorithm launched which requires far less liquidity to keep USK price significantly more stable.

## Payment Aspects

By being Kujira blockchain native, USK has a great amount of flexibility available in underlying various payment services. By being soft-pegged to the US Dollar and maintaining relative price stability over time, USK makes for an effective medium for making payments that can be settled on the Kujira blockchain. Decentralized commerce follows from the integration of real-world payments with functionality already enabled through an initial WooCommerce integration that allows USK payments in online shopping. More details will be added once new features are live.
