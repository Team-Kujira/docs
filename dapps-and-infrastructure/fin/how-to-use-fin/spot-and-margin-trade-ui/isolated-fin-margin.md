# ⭕ Isolated FIN Margin

## Overview

Isolated FIN Margin is a type of margin product that allows leverage trading of up to 2.5X on certain FIN trading pairs. All compatible FIN pairs have a 2.5X logo:<img src="../../../../.gitbook/assets/image (36).png" alt="" data-size="line">

Margin is allowed on most [USK](../../../usk-stablecoin/) collateral types when paired with USK on FIN. Currently margin is only unavailable for gPAXG (Paxos Gold bridged over to Kujira using [Gravity Bridge](../../../../kujira-ecosystem/how-to-deposit-assets-into-the-ecosystem.md#gravity-bridging)). All margin liquidations are handled by ORCA. Read more specifics about how this process works [here](../../../orca/lending-markets/usk-lending-markets/isolated-fin-margin.md#liquidation-mechanism).

## Margin trade safely

Margin trading in cryptocurrency allows you to earn substantial profits, diversify your position, and learn trading strategies. The profits are better because of the high relative value of trading positions, and you can open multiple positions with little investment. However, crypto margin trading can also result in significant losses because of its extremely volatile nature and greater risks. Therefore, if you are new to margin trading in cryptocurrency, you have to be more cautious.

It is advisable to acquire knowledge about hedging and risk management. Even with adequate knowledge to identify market trends, [entry and exit points](https://medium.com/@ArnieHill/choosing-entrance-and-exit-levels-in-crypto-trading-34530e9c2d12), it is always best to remain cautious with crypto margin trading.

## Placing spot orders&#x20;

To use isolated margin on a suitable FIN trading pair, first navigate to the 'Isolated Margin tab:

&#x20;                                     ![](<../../../../.gitbook/assets/image (3).png>)

To create a FIN margin position, first navigate to a FIN trading pair that has isolated margin trading available. Next, select an amount of USK to leverage and a leverage factor to use to gain exposure to a corresponding amount of the [base asset](../price-chart-and-charting-tools.md#fin-price-charts) equal to the product of the current asset pair exchange rate, the USK amount, and the selected leverage factor for as long as the margin position is open.

&#x20;                                        ![](<../../../../.gitbook/assets/image (21).png>)

A projected daily interest rate, the current base asset oracle price, the projected base asset entry price, as well as the margin position liquidation price are all displayed as part of the trading UI and can be examined in detail before deciding to open the long position.

Isolated margin positions are special cases of margin that correspond to USK collateral positions used to mint USK which have corresponding liquidation thresholds. Positions are liquidated in progressive stages rather than all at once. &#x20;

## Mechanism&#x20;

The FIN isolated margin long contract effectively works by minting USK backwards. For the sake of convenience, let's assume the trading pair of interest is ATOM/USK. Suppose the specified deposit amount is 1000 USK and the leverage factor has been chosen to be 1.4. In that case, the funding amount can be calculated as (the initial USK deposit amount) \* (the chosen leverage factor - 1) amount of USK = 1000\*(1.4-1) or 400 USK. Next, the following 4 step process takes place instantly:

At time 0, 1000 USK is deposited at a chosen leverage factor of 1.4. At time 1, 400 USK is minted (unbacked and in reverse) based on the promise of future ATOM backing. At time 2, the 1000 initial USK deposit + the 400 minted USK are used to purchase 1400 USK worth of ATOM on the market using FIN. Finally, at time 3, 1400 USK worth of ATOM are used to back the 400 minted USK.

The above position allows the user to have exposure to 1400 USK worth of ATOM with debt/borrow obligations of 400 USK by using 1000 USK upfront. The benefit is that the initial 1000 USK is leveraged at a factor of 1.4X and assuming ATOM price increases while the position is open, then the margin will make more money than it would have by simply buying 1000 USK worth of ATOM upfront.&#x20;

The highest possible leverage is 2.5X. In this case, a USK collateral debt position is minted at 60% LTV. Maximum leverage is risky as USK CDP positions start to be liquidated as soon as the LTV  passes the 60% threshold.&#x20;

