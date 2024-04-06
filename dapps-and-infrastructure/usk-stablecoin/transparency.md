---
cover: ../../.gitbook/assets/usk docs test.png
coverY: 0
---

# Transparency

## Overview

We aim to turn USK into a premier high quality decentralized stablecoin that is suited for real world decentralized commerce. That is why transparency is essential as a part of reassuring our partners and users alike. We have compiled helpful explanations below.

## How to check USK price

USK price can easily be tracked on [FIN](../fin/) and on [CoinGecko](https://www.coingecko.com/en/coins/usk). Remember that USK is _softpegged_ to the US dollar. On FIN, USK price can be tracked by looking at the relative token prices of pairs on FIN. How much USK does it cost to buy each asset? Even though some assets may be more expensive on FIN, other assets may be cheaper which effectively averages out the USK price as traded assets can always be IBC'ed or bridged away via the [BLUE IBC / Bridge interface](../blue/ibc-bridge.md).

## How to review all active USK backing collateral

The BLUE [dashboard](https://blue.kujira.app) and [Mint ](https://blue.kujira.app/mint)tabs contain a breakdown of all USK backing collateral (and will soon contain information displaying the total of collateral actually backing minted USK).

In the meantime, [ORCA](../orca/) contains information about each USK liquidation market including the total amount of locked collateral for each USK collateral type as well as the current asset price. The corresponding Analytics tabs neatly summarize this data at the top. Using this data, a USK collateral backing ratio can be calculated for each collateral type. This calculation can be performed by taking the amount of USK minted by a specific collateral type (found on BLUE) and dividing it by the product of the total amount of locked collateral for that specific collateral type and and the current asset price i.e. $$\text{USK collateral type backing ratio = } \frac{\text{total amount of USK minted by that collateral type}} {\text{total amount of locked collateral for that type } \times \text{ the collateral's current price} }$$

## How to track USK liquidation backstop health

By navigating to [ORCA](../orca/), each USK liquidation market can be analyzed in-depth for all collateral types. At any point in time, there is only some proportion of backing collateral (if any) actually at risk of liquidation to preserve USK's status of being 166% collaterized. The analytics tab shows two charts, 'The Cumulative Collateral by Risk Ratio' chart and the 'Collateral by Risk Ratio' chart which measure the amount of USK actually at risk of liquidation. The concept behind 'risk ratio' as well as other basic ORCA concepts are explained [here](../orca/basics/).&#x20;

The 'Ratio of Pools to Locked Collateral value' gives us an idea of the ratio of funds locked in ORCA to liquidate USK backing collateral, but generally is healthy even at low numbers as long as a corresponding amount of backing collateral is at risk.&#x20;

## How to verify and track all USK minting and burning

1. Go to any USK market page, $ATOM in this example: [https://blue.kujira.network/mint/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf](https://blue.kujira.network/mint/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf)
2. Get the address in the URL. In this case it's `kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf`
3. Look up that address in the Kujira Finder: [https://finder.kujira.network/kaiyo-1/contract/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf](https://finder.kujira.network/kaiyo-1/contract/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf)
4. Here is a sample TX where you can see a **`burn`** event: [https://finder.kujira.network/kaiyo-1/tx/624CFE48D905F91647FA0698400C4C2D52C1558D28BC650F4FE21924915D206F](https://finder.kujira.network/kaiyo-1/tx/624CFE48D905F91647FA0698400C4C2D52C1558D28BC650F4FE21924915D206F)\
   \
   which corresponds with the burn events emitted by the core module [https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L89-L95](https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L89-L95)
5. The same goes for the **`mint`** event: [https://finder.kujira.network/kaiyo-1/tx/8F39BC56D32602EBD76C4BCAC20075431AEEB2ECC245849699D7E12286F9A6AD](https://finder.kujira.network/kaiyo-1/tx/8F39BC56D32602EBD76C4BCAC20075431AEEB2ECC245849699D7E12286F9A6AD)\
   \
   which corresponds with the mint events emitted by the core module [https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L61-L67](https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L61-L67)
