# ⛽ Orderbook status and Recent Trades

## Overview

When a trading pair is selected, the upper right section of the FIN user interface contains real time orderbook activity including a list of most recent trades and a list of all buy and sell limit orders sufficiently close to the current FIN market rate for that pair.

## Limit Order Activity

BOW helps create liquidity for FIN and is responsible for placing some of these limit orders, both buys and sells to help minimize the spread on FIN pairs. Spread can be understood as a changing numerical value that refers to the gap between the lowest price a user (or market maker) is willing to sell the [base asset](./#fin-trading-pair-notation) in terms of the [quote asset](./#fin-trading-pair-notation) and the highest price a user (or market maker) is willing to buy the base asset in terms of the quote asset. It can also be understood as the smallest gap between supply and demand for the base asset of a trading pair.

For heightened experience, FIN only displays limit orders sufficiently close to the current FIN market price to most closely reflect short-term trading pair demand or supply.

&#x20;                                           ![](<../../../.gitbook/assets/image (23).png>)

There are 3 different orderbook views: the default buy and sell limit order views, with limit sells in red and limit buys in green; the second limit sell view, only showing red limit sells (showing more of the sell side of the orderbook); and the third limit buy view, only showing green limit buys (showing more of the buy side of the orderbook). The 3 different views have different uses to understand more extreme order predictions for short or long-term price changes, especially for large limit orders.

Market orders placed on FIN fill based on existing limit order liquidity in the orderbook. When multiple limit orders exist at the same price, they are aggregated together into the book view simply increasing the total amount shown demanded or supplied at a certain price. Following this principle, when market orders are placed using FIN, they will partially fill based on existing aggregate limit orders created at the closest prices to the current midpoint of the bid-ask spread. Once filling all the limit orders at a specific price, they will then continue on to the next lowest (when market buying) or next highest (when market selling) set of aggregate limit orders and so on until they completely fill.

The buy and sell side orderbook activity contains 3 important pieces of information for each row: limit order price in terms of the quote asset, total amount of the base asset supplied or demanded by all aggregate limit orders in the orderbook at that price level, and the aggregate value of all limit orders at a specific price i.e. the product of the first two numbers.

## Recent Trading Activity

Recent FIN trading activity for a specific pair is also captured on the top right of the screen in the user interface. Before the UI is explained in detail it is important to explain the concept of maker/taker.

&#x20;Maker and taker FIN transactions have different fees. Maker orders refer to actions that supply liquidity to the FIN orderbook i.e. placing a limit order (whether a buy or sell) where as taker orders refer to actions that remove liquidity from the FIN orderbook i.e. placing a market order. In some cases, limit orders can also be taker orders. Suppose there is an order to sell 10 KUJI in the orderbook at X price and a user enters a limit order to buy 10 KUJI in the orderbook at X price--since the result of that order is the overall reduction of FIN orderbook liquidity for that trading pair, the limit order is still treated as a taker order. Currently maker orders and taker orders respectively have 0.075% and 0.15% fees. In the near future, FIN will transition to a model where maker orders have _negative_ fees and taker orders will have slightly higher fees to sustainably earn revenue and encourage more orderbook liquidity.&#x20;

Building on this understanding of maker/taker orders, it is easier to explain the details of the FIN recent trading activity UI. This UI only displays taker orders i.e. (market and limit) buys and sells that removed liquidity from the FIN orderbook. Buys are displayed in green text whereas sells are displayed in red text. Three additional pieces of data are stored for each recent taker order: the price of the base asset in terms of the quote asset; the amount of the base asset purchased or sold; and the _local_ time in hours, minutes, and seconds when the order was placed.&#x20;

&#x20;                                             ![](<../../../.gitbook/assets/image (40).png>)

The recent trading activity shows the latest 25 FIN transactions, more transactions can be seen on external third parties such as Coinhall. Transaction history can give traders a better idea of orderbook flow over a period of time--especially in conjunction with recently released announcements or news.&#x20;

&#x20;

