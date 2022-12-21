---
description: >-
  An over-collateralized Cosmos stablecoin soft-pegged to the USD and initially
  backed by $ATOM, $DOT & $wETH
---

# 🐎 USK Stablecoin

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
