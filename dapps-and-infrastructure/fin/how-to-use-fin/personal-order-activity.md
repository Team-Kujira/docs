# Personal Order Activity

## Overview

Personal order activity tracks current and past FIN order activity associated with any wallet currently connected to the FIN decentralized application. This section contained in the bottom center of the FIN user interface is the second to last important piece of the FIN trading experience. For a connected wallet, each FIN trading pair has a completely separate set of displayed personal order activity. This information is conveniently stored to help users track gains and loss across each FIN trading pair.

Personal order activity can be broken down into 3 main components of the user interface: open orders, filled orders, and history.&#x20;

## Open Orders

Open orders are limit orders (market orders fill instantly so they are never open orders) for a specific FIN trading pair that have been placed and are either unfilled or only partially filled. As open orders are filled over time, the status of how much has already been filled will display on the user interface. When limit orders are entirely filled they are removed from the 'open orders' section of the FIN UI to the 'filled orders' section.

Each open order for a trading pair comes with the following associated information: the date when the order was first placed in local time, the associated trading pair, whether the order is a buy or a sell, the price of the [base asset](./#fin-trading-pair-notation) in terms of the [quote asset](./#fin-trading-pair-notation), the amount of the base asset initially supplied or demanded with the limit order, the amount of the base asset already filled from the limit order, and the remaining amount of the base asset still to be filled from the limit order.

&#x20;                                        ![](<../../../.gitbook/assets/image (35).png>)

Open orders can be sorted by each information type by tapping or clicking on the top of each category. Tapping or clicking it more times will alternate the open orders listed between ascending and descending order.

Furthermore, open orders can be cancelled at any time (although any partial fills are permanent) for a small fee of approximately a few cents.

## Filled Orders

Filled orders are past limit orders for a specific FIN trading pair that have previously been completely filled due to matching demand or supply from the orderbook AND that have not yet been claimed by the user from FIN back into their wallet. To reiterate, all limit orders on FIN must be claimed from the filled orders tabs (of the relevant trading pair) to show up in a user's wallet. Filled orders are exactly those orders that have previously been filled, but not yet claimed by users.   When filled orders are claimed, they automatically are removed from the 'filled orders' section of the FIN UI to the 'history' section.

For the sake of maximum convenience for users, trading pairs with unclaimed filled orders will have a green dot appear next to them--to alert users to claim their purchased assets (whether obtained from buying or selling).

Much like open orders, each filled order for a trading pair comes with the following associated information: the date when the order was first placed in local time, the associated trading pair, whether the order is a buy or a sell, the amount of the base asset initially supplied or demanded by the order, the price of the [base](./#fin-trading-pair-notation)[ asset](./#fin-trading-pair-notation) in terms of the [quote](./#fin-trading-pair-notation)[ asset](./#fin-trading-pair-notation), the percentage of the base asset already filled from the total amount specified by the order, and the amount of the base asset currently filled that is available to claim from FIN into the user's wallet.

&#x20;                                         ![](<../../../.gitbook/assets/image (19).png>)

Filled orders can be sorted by each information type by tapping or clicking on the top of each category. Tapping or clicking it more times will alternate the open orders listed between ascending and descending order.

Furthermore, filled orders can be claimed at any time (although any unfilled parts of the order will need to be claimed separately later) for a small fee of approximately a few cents.

## History

This tab in the FIN personal order activity user interface contains detailed information for all past market orders and claimed limit orders uniquely specific to each FIN trading pair.

&#x20;                                            ![](<../../../.gitbook/assets/image (37).png>)

The history tab contains the order # (out of FIN's total transactions, which # transaction was it), the date using local time, the price the asset was purchased or sold at, the amount of the [base asset](./#fin-trading-pair-notation) and [quote asset](./#fin-trading-pair-notation) exchanged, the specific action taken (submitting an order or claiming an order), and a link to the the associated transaction on [FINDER](../../finder/) to verify all the involved specifics.

The history tab contains the cumulative experience of a particular wallet (or user) for a specific FIN trading pair. This information can be very useful for tracking gains and losses, filing tax information, or simply track of personal order activity over time.&#x20;
