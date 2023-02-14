# 📱 Spot and Margin Trade UI

## Overview

The spot and margin trade user interface on the bottom right is the final section of the FIN experience for a specific trading pair. Here users can perform trades to buy or sell assets using market orders, limit orders, or spot margin on available pairs. As part of the UI, users can choose between selling [base assets](../#fin-trading-pair-notation) to acquire [quote assets](../#fin-trading-pair-notation) or buying base assets by 'spending' quote assets.

## Spot Trading

All FIN pairs allow spot trading and use a simple fee structure. FIN charges different types of proportional fees on different types on orders depending on whether they are maker or taker orders. Read more on FIN maker/taker fees and mechanics [here](../orderbook-status-and-recent-trades.md#recent-trading-activity). More details below.&#x20;

FIN pairs without isolated margin trading typically have a UI split between limit and market orders.

&#x20;                                 ![](<../../../../.gitbook/assets/image (36).png>)

### Placing Orders

Placing an order using the FIN spot trading UI is relatively simple once the user understands the basic FIN trading notation being used. FIN pairs are notated [Base asset](../#fin-trading-pair-notation) / [Quote asset](../#fin-trading-pair-notation) (KUJI/USK). On the spot trading UI, the _left half_ of the UI (for both market and limit orders) allows you to spend  the quote asset to _purchase_ an equivalent amount of _the base asset_--and the _right half_ of the UI similarly allows you to _sell the base asset_ to purchase an equivalent amount of the quote asset.

As a point of caution, all transactions on FIN are irreversible and final so when placing orders make sure to double check that numbers, prices, amounts, etc. are entered correctly without missing or adding extra decimal places or zeroes to avoid buying or selling assets at undesired prices.&#x20;

The activity of placing FIN spot orders can be broken down into placing market and limit orders.

#### Market Orders

Upon selecting a FIN trading pair, the FIN trade UI defaults to the spot limit order view. First switch to 'market' near the top left of the FIN trade UI to be able to place market orders using FIN. Next, depending on whether you want to buy or sell the base asset, refer to the prompts at the bottom of the FIN trade UI and fill out the side of the UI (left or right) corresponding to the desired action.

&#x20;As a non-zero amount of [quote asset](../#fin-trading-pair-notation) to spend or [base asset](../#fin-trading-pair-notation) to sell is entered into the UI, corresponding information will be listed below: the total amount of the quote asset or base asset that is available in a user's wallet to spend on a trade, the estimated amount of acquired base asset or quote asset respectively after spending quote assets or selling base assets, the effective average exchange rate between the quote and base asset, total fees that would be spent, and estimated slippage. The UI also has a handy mechanism for automatically selecting 25%, 50%, 75%, or 100% of the relevant quote asset to spend or base asset to sell as part of the trade.&#x20;

&#x20;                                             ![](<../../../../.gitbook/assets/image (21).png>)

When performing a market order to spend quote assets (or sell base assets), corresponding FIN trading fees are always 0.15% taken off from what would have been the total purchased base assets (or received quote assets). This mechanism leverages the fact that FIN is an orderbook and that every trade on the platform needs to be made between two parties. Each party pays fees in terms of the asset they would have received.

For example, suppose user A has already placed a FIN limit order selling 14 KUJI at 5 USK each (which is the closest limit sell to the current KUJI/USK exchange rate) and user B places a market order to spend 10 USK to purchase KUJI. In this case, the FIN orderbook would still contain a limit order selling 12 KUJI at 5 USK each, FIN charges user B (0.15%\*\[10/5] or) 0.003 KUJI in fees B and charges user A (0.075%\*10) or 0.0075 USK in fees, and finally FIN dispenses (5-0.003 or) 4.997 KUJI to user B and (10-0.0075 or) 9.9925 USK to user A. Note that in the above example, since 1 KUJI = 5 USK, the total fee for user B is equal to 0.003 \* (1 KUJI) = 0.003 \* 5 USK = 0.015 USK = 2 \* (0.0075 USK). In other words, as expected user B pays 0.15% in taker fees which is the double fee as user A who pays 0.075% which is the maker fee for orders that add liquidity to the FIN orderbook. This ratio will change in the near future once FIN maker fees become negative.

Alternatively, users can use the [BLUE swap](../../../blue/swap.md) or [BOW](../../../bow/swap.md)[ swap](../../../bow/swap.md) UI's to place FIN market orders. That being said, the FIN UI still provides current [trading pair orderbook status and recent trades](../orderbook-status-and-recent-trades.md), the [price chart](../price-chart-and-charting-tools.md), and [personal order activity](../personal-order-activity.md) which often make FIN a superior option for users willing to spend a bit of extra time to gather information.

#### Limit Orders

Upon selecting a FIN trading pair, the FIN trade UI defaults to the spot limit order view. Depending on whether you want to buy or sell the base asset, refer to the prompts at the bottom of the FIN trade UI and fill out the side of the UI (left or right) corresponding to the desired action.

Unlike the FIN market trading UI, the limit order trading UI requires two separate pieces of information as part of either spending [quote assets](../#fin-trading-pair-notation) or selling [base assets](../#fin-trading-pair-notation) using a limit order. As with market trades, it is necessary to specify a non-zero amount of quote asset to spend or base asset to sell. In addition, it is necessary to specify a desired asset pair exchange rate floor or ceiling with any limit order. A FIN trading pair exchange rate can simply be thought of the ratio of the base asset price to the quote asset price. For example, if 1 KUJI currently costs 3 USK, then the corresponding current KUJI / USK exchange rate would be  3 : 1. The exchange rate floor/ceiling is used as part of a limit order to guarantee that the base asset is only sold above or bought below a certain price--to ensure that a subjectively good trade is being made. These prices correspond directly to the prices listed in the [orderbook status](../orderbook-status-and-recent-trades.md) section--which can serve as a helpful reference to ensure that entered prices are within the correct ballpark.&#x20;

Once the amount of quote asset to spend (or base asset to sell) and desired trading pair exchange rate ceiling/floor are entered into the UI, corresponding information will be listed below: the total amount of the quote asset or base asset that is available in a user's wallet to spend on a trade, total fees that would be spent, and the estimated amount of acquired base asset or quote asset respectively after spending quote assets or selling base assets.

&#x20;                                                  ![](<../../../../.gitbook/assets/image (38).png>)

When performing a limit order to spend quote assets (or sell base assets), depending on whether the limit order is adding or removing liquidity from the orderbook, corresponding FIN trading fees will either be 0.075% or 0.15% taken off from what would have been the total purchased base assets (or received quote assets). This mechanism leverages the fact that FIN is an orderbook and that every trade on the platform needs to be made between two parties. Each party pays fees in terms of the asset they would have received. Refer to the market orders section for an example of how FIN fees work in action.

Aside from relatively limited fixed price swap orders (special limit orders that are automatically assigned to execute at the current asset pair market exchange rate) which may be performed on the [BLUE swap](../../../blue/swap.md) and[ BOW swap](../../../bow/swap.md) UIs, limit orders are exclusive to the FIN decentralized application. The FIN UI also provides current [trading pair orderbook status and recent trades](../orderbook-status-and-recent-trades.md), [the price chart](../price-chart-and-charting-tools.md), and [personal order activity](../personal-order-activity.md) to help users make the best trades.



## Margin Trading

Certain FIN trading pairs allow users the option to use margin to perform FIN trades at anywhere between 1X and 2.5X leverage. Currently isolated FIN margin is available on every USK collateral / USK pair except for gPAXG/USK by using ORCA as a liquidation settlement layer. Currently only spot longs are available; however, with time spot shorts and limit orders using margin will also be possible. Read more [here](isolated-fin-margin.md) about isolated FIN margin.
