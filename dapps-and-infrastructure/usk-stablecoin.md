---
description: >-
  An over-collateralized Cosmos stablecoin soft-pegged to the USD and initially
  backed by $ATOM, $DOT, $wBNB, & $wETH
---

# 🐎 USK Stablecoin

Kujira's USK stablecoin is a decentralized stablecoin that is soft-pegged to the US dollar and initially backed by ATOM, DOT, wETH, and wBNB (with nBTC to be added soon). It is an overcollateralized stablecoin, meaning that it is backed at a minimum of 166%. This helps to ensure the stability of the stablecoin and reduce the risk of liquidation.

* Mint USK by depositing collateral on the Kujira platform
* Manage USK through the platform's dashboard
* Maintain a low loan-to-value (LTV) ratio to avoid the risk of liquidation
* In the event of a liquidation, collateral is put up for auction on [ORCA](orca.md)
* Users can bid on the collateral to help protect the stablecoin and obtain the collateral at a discount

USK is designed to be sustainable, robust, and usable for payments and commerce. Its codebase is written in Rust, which is a more robust and expressive language than Solidity or JavaScript. Rust is also inherently built to be safer (bug-resistant) and is increasingly used for financial applications due to its level of safety guarantees. As a native Cosmos stablecoin, USK has the potential to drive value accrual for ATOM and can be used for other purposes in the future. It is integrated into the ORCA platform to allow for seamless and publicly accessible liquidations. The USK mechanism is intended to be sovereign, uncensorable, and revenue-generating, and it is intended to provide a secure and reliable foundation for decentralized finance.

* Greater focus on payments and real-world applications for decentralized commerce
* USK synergizes with Kujira's wallet, Sonar as well as all Kujira products
* Integration with Woo Commerce, one of the largest online merchant providers
* Initially set a cap of 1 million USK per collateral type to ensure proper diversification

ORCA is a public marketplace that allows anyone to bid on liquidated collateral from the Kujira platform, effectively participating in a Dutch auction to obtain the collateral at a discount. ORCA has processed a significant amount of liquidity since its launch, with a maximum total value locked (TVL) of $160 million. ORCA operates using a queue-based and anti-bot approach, filling bids from the smallest discount to the biggest, helping to find an optimal discount rate and prevent immediate selling and damage to the market by bot operators. ORCA offers several benefits for partner money markets and users, including a user-friendly interface, transparent bidding process, nearly instant settlement of liquidations, robust yet capital efficient approach, and strong community. Universally accessible, ORCA allows every user to participate in the marketplace and take advantage of its benefits.

Here's a more detailed breakdown describing USK mechanics:

1. [USK overview and mechanism design](https://medium.com/team-kujira/kujira-usk-stablecoin-launch-kickstarting-grown-up-defi-26b4372d7aef)
2. [USK minting and ORCA liquidation guide](https://medium.com/team-kujira/testnet-usk-minting-orca-liquidation-bids-4f1215e9677b)
3. [Minting USK and managing your position](https://medium.com/team-kujira/team-kujira-minting-usk-and-managing-your-position-6ba405bf1301)

### How to verify and track all USK minting and burning

1. Go to any USK market page, $ATOM in this example: [https://blue.kujira.app/mint/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf](https://blue.kujira.app/mint/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf)
2. Get the address in the URL. In this case it's `kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf`
3. Look up that address in the Kujira Finder: [https://finder.kujira.app/kaiyo-1/contract/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf](https://finder.kujira.app/kaiyo-1/contract/kujira1ecgazyd0waaj3g7l9cmy5gulhxkps2gmxu9ghducvuypjq68mq2smfdslf)
4. Here is a sample TX where you can see a **`burn`** event: [https://finder.kujira.app/kaiyo-1/tx/624CFE48D905F91647FA0698400C4C2D52C1558D28BC650F4FE21924915D206F](https://finder.kujira.app/kaiyo-1/tx/624CFE48D905F91647FA0698400C4C2D52C1558D28BC650F4FE21924915D206F)\
   \
   which corresponds with the burn events emitted by the core module [https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L89-L95](https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L89-L95)
5. The same goes for the **`mint`** event: [https://finder.kujira.app/kaiyo-1/tx/8F39BC56D32602EBD76C4BCAC20075431AEEB2ECC245849699D7E12286F9A6AD](https://finder.kujira.app/kaiyo-1/tx/8F39BC56D32602EBD76C4BCAC20075431AEEB2ECC245849699D7E12286F9A6AD)\
   \
   which corresponds with the mint events emitted by the core module [https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L61-L67](https://github.com/Team-Kujira/core/blob/master/x/denom/keeper/msg\_server.go#L61-L67)\
   \
