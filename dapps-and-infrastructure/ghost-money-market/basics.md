# 🔢 Basics

## What is GHOST?

GHOST is Kujira's premier Money Market. As a decentralized money market, GHOST allows would-be lenders and borrowers to cooperate by providing a convenient supply-demand framework. Furthermore, it generates attractive returns for market participants without relying on artificial incentives.  &#x20;

Since GHOST is a decentralized money market, suppliers are covered even if borrowers fail to repay their loans. Furthermore, since all loans on GHOST are overcollateralized, borrowers don't have to apply for loans or go through credit checks. Opening or closing a loan and supplying or redeeming supplied assets is a near instant process that can be done at nearly anytime. The only exception is when the utilization of an asset reaches 100%. In this case, supplied assets of that type cannot be redeemed until some are returned (or more are supplied) to the platform.&#x20;

Suppliers supply assets to GHOST to earn variable interest on those provided assets based on their overall utilization by borrowers. Borrowers borrow assets supplied on GHOST (by others) in order to participate in financial speculation or take out loans without selling underlying assets. Borrowers are charged variable interest over time dependent on the borrowed assets' overall utilization by borrowers. This interest rate cycles between high and low over time based on inherent market demand and GHOST's framework. [Here's more about how the interest rate works](basics.md#how-interest-works-on-ghost).

When borrowers fail to pay back their loans in time due to decreases in collateral value, increases in funds borrowed, or accrued interest--provided collateral is liquidated via ORCA.  [Here's more about how liquidations work on GHOST](basics.md#how-ghost-has-integrated-orca). &#x20;

## Borrowing on GHOST

All borrowers must put up collateral (in asset "C") in order to take out a loan (in a different asset "L")--this collateral is not supplied to GHOST in the same sense as with "suppliers". The collateral cannot be borrowed by other users and it sits on the platform mainly as a guarantee to ensure the underlying integrity of a corresponding loan. This is necessary in case borrowers exceed max safety on their loans in which case their deposited collateral gets liquidated on ORCA and they get to keep any borrowed funds.

Depending on the perceived risk relationship between the supplied collateral asset (asset C) and borrowed loan asset (asset L), there is an underlying max allowable loan-to-value (LTV) ratio belonging to that loan. Say the value of the provided collateral is $$v_{c}$$and the value of the borrowed loan is $$v_{l},$$then the current LTV of that loan is$$\frac{v_{l}}{v_{c}}$$(any decimal can be converted into a percentage by multiplying it by 100%).

For stablecoins borrowed against provided stablecoins, the loan is considered relatively safe so they have slightly higher max allowable LTVs. For tokens borrowed against liquid staking derivative versions of themselves, they generally have a higher max allowable LTV which depends on each particular case. And in almost every other case, when borrowing one asset against another unrelated asset, the max allowable LTV is 60%. The only exception is when borrowing funds against provided KUJI collateral. The max allowable LTV is slightly lower to create less instability in KUJI price.

### General example

Now, for a more concrete example. Let's say at time $$0$$ user U has provided X units of asset C to borrow Y units of assets L; the prices of asset C and L at time t respectively are $$p_{c}(t)$$and $$p_{l}(t);$$ the max allowable loan-to-value (LTV) of asset C as collateral to asset L as a loan is K; and $$I(t)$$is a function representing the instantaneous variable interest rate of asset Y over time. Then, the borrowed funds (the Y units of L), will be liquidated at any future time $$t$$ if&#x20;

$$K < \frac{ \text{value of borrowed loan}}{ \text{value of provided collateral}}+\text{accrued interest until time } t=\frac{yp_{l}(t)}{xp_{c}(t)}+\frac{yp_{l}(t)}{xp_{c}(t)}\int\limits_{0}{t}I(s)ds$$



An easier way to think about the maximum allowable LTV is to understand that the interest rate reflects the amount of extra funds you will need to pay back (if you keep your loan open for a sustained period of time). Any extra funds you need to pay back increase your position's LTV and get you closer to liquidation. LTV can also change in other ways. If the price of the asset you provided as collateral goes down, then the LTV will increase. Similarly, if the price of the asset you borrowed goes up, then the LTV will increase. Of course, the reverse can also happen, and push the LTV lower--this is why, it is generally recommended to borrow stablecoins and use relatively stable or high quality assets you are bullish on as collateral (unless you are experienced).

The simple mental calculation with APR is that when your current loan amount is $$v_{l}$$ and your yearly interest rate is i, then assuming a constant interest rate, in two months, your accrued interest will be $$v_{l}*\frac{i}{6}$$since only 1/6th of a year would have passed (assuming no changes in the loan value).&#x20;

More advanced examples of how to understand and work with borrowing can be found under advanced tutorials.

## Lending on GHOST

All lenders on GHOST provide liquidity by lending assets to the platform and get paid a variable interest rate as compensation. When users deposit N units of an asset called “TOKEN” into the platform, they will receive N liquid units of an asset called “xTOKEN” in their wallet.&#x20;

xTOKEN is similar to a receipt token that represents a claim to lent TOKEN on GHOST. xTOKEN can be traded on FIN, sent to other wallets, or used with ORCA to bid on liquidations. This is especially attractive as units of xTOKEN automatically accrue interest that is collected from TOKEN borrowers’ open loan positions on GHOST. When the lender eventually redeems their xTOKEN, they will receive back all their TOKEN and some extra TOKEN corresponding to that accrued interest.

For example, if you lend 10 ATOM on GHOST, you will receive 10 xATOM in your wallet. Say you leave those ATOM lent to GHOST for a few months and redeem your ATOM at that time. Depending on utilization levels and how much interest was accrued during that period of time from other ATOM borrowers, you may receive back 10 ATOM, 10.1 ATOM, 11 ATOM, etc.&#x20;

Using xAssets to liquidate collateral on ORCA is particularly exciting because doing so is equivalent to selling the underlying xAsset at a local market top (i.e. when it is most expensive) at up to $$\frac{1}{1-30\%}=\frac{1}{0.7}=42.8\%$$ above the maximum possible market price at that time.

## How interest works on GHOST

All interest rates on GHOST are represented as yearly APR's, as this is generally more convenient for users who often think on longer time scales.

Variable interest rates increase with higher utilization and decrease with lower utilization. This serves two purposes: 1. encourage new suppliers and incentivize borrowers to unwind their loans and return borrowed assets in hot markets; 2. discourage new suppliers and make it more attractive for borrowers to open loans in slow markets.

Asset utilization refers to the ratio of borrowed assets to supplied assets for an asset on GHOST. For example, suppose 1000 users collectively provide 1 million ATOM to GHOST, and 300 users collectively borrow 572,138 ATOM on GHOST. In that case, ATOM's utilization on GHOST is $$\frac{572,138}{1,000,000}=0.572138=57.2138 \%$$. Based on  1. and 2. asset utilization rates will often cycle between high and low over time.&#x20;

GHOST uses an exponential algorithm that spikes the interest rate sharply once utilization hits around 60% to encourage asset borrow to supply ratios to stay within certain boundaries. Generally, the borrow interest rate for an asset is a few percent higher than its supply interest rate. This accounts for the inherent risk premium that accompanies borrowing. &#x20;

## How GHOST has integrated ORCA

ORCA has been overhauled in order to smoothly integrate GHOST. In this framework, each GHOST collateral and borrowable asset pair has its own corresponding liquidation queue on ORCA. In general, demand exists to liquidate outstanding GHOST loans on ORCA, because it’s possible to acquire the liquidated collateral at a discount and achieve a tidy profit.&#x20;

For example, if GHOST users are able to borrow ATOM (lent by suppliers) against their own provided USK collateral, then an axlUSDC-xATOM liquidation queue will exist on ORCA–where users can bid on liquidated axlUSDC using xATOM at a discount of up to 30%. Note 1. the maximum allowed LTV and maximum allowed discount on ORCA take each other into account and 2. when a user bids with their xATOM on ORCA to purchase discounted axlUSDC, they are forfeiting their receipt/claim to the corresponding supplied ATOM on GHOST. .

That is to say, after a liquidator purchases liquidated axlUSDC at a 30% discount, since the position is liquidated when the LTV of the borrowed ATOM loan position reaches 60%--this ensures that the loan is approximately 160% overcollateralized at the time of liquidation–and even after a 30% discount is applied, the position is still 112% overcollateralized.

Therefore, say the liquidator puts down $70 worth of xATOM on ORCA to purchase the $100 of liquidated axlUSDC at a 30% discount. The liquidator receives $100 of axlUSDC, and ORCA receives $70 worth of xATOM which go back to GHOST to replenish the original lender’s supplied ATOM.&#x20;

Assuming the loan was liquidated immediately once it reached 60% LTV, then only $60 worth of xATOM was actually borrowed from the platform. In this way, GHOST ends up with an extra $10 of xATOM that can be further used to redeem borrowers. Most of the time, the loan will be liquidated for a significantly smaller discount due to user competition, so GHOST pockets more profit in general.  &#x20;

In the case of assets with higher maximum allowable LTVs, the maximum possible discount on an ORCA queue will be smaller such as with the axlUSDC-USK queue where the maximum possible discount is only 10%. This ensures the integrity of the underlying loan.&#x20;

### Liquidation Alerts

As an aside, since there are many different liquidation queues in the new ORCA/GHOST framework, ORCA alerts have been conveniently added to the top right of most of our 1st party ecosystem dApps.  Kujira ecosystem users can conveniently see when GHOST (or USK mint) positions are at risk via alerts that detail which assets are closest to getting liquidated (including how much is at risk of being liquidated and how close they are to liquidation). This allows users to anticipate future liquidations and move corresponding funds in advance.&#x20;

\


