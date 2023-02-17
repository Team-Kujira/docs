# 🚛 Lending Markets

### Overview

The ORCA bidding queue is an innovation that takes liquidation profits from the clutches of whales and instead delivers it into the hands of everyday community members. This is possible by having users compete to acquire discounted collateral. The competition to acquire liquidated collateral moves away from bots and speed and instead to bidding wars which allow integrated protocols to be as capital efficient as possible. User bids seeking to purchase liquidated collateral at a smaller discount have higher priority in the ORCA liquidation queue. In this way instead of competing by speed for 30% discount liquidations of assets to dump on the market, users bid in the ORCA liquidation queue and compete to liquidate collateral empirically closer to a 3-8% discount. Integrated protocols do not need to worry about liquidators arbitraging and dumping liquidated collateral onto the market at a heavy discount and liquidation profits are accessible to many more users.&#x20;

## Customization and flexibility for integrated products

Each integrated protocol or application has the ability to customize the ORCA liquidation queue however they would like to maximize its appeal to their target communities. They can choose to allow half percentage discount liquidations, set their own minimum and maximum percentage liquidation discount, and choose their preferred assets to use to bid on liquidated collateral in the ORCA queue.&#x20;

&#x20;                           ![](<../../../../.gitbook/assets/image (47).png>)

Each lending market contains its own unique ORCA liquidation queue with discounts ranging from 0% to the maximum allowed percentage. All USK lending markets have a 30% maximum bid and bid premiums must be whole numbers.

## Hypothetical liquidation example

Let's take a look at a hypothetical ORCA example for the ATOM/USK lending market. Suppose the price of ATOM suddenly falls and that in the ATOM USK lending market, exactly 20000 USK worth of ATOM ends up getting liquidated in one go. Further, also assume that there is 0 USK in the 0%, 1%, and 2% columns; 100 USK in the 3% column; 1000 USK in the 4% column; 10000 USK in the 5% column; and 10000 USK in the 6% column of the ORCA liquidation queue. Finally, let's assume that the 10000 USK in the 6% column has been deposited by 4 separate individuals: person A deposited 2500 USK, person B deposited 3500 USK, person C deposited 3990 USK, and person D deposited 10 USK. In that case, 20000 USK worth of ATOM is being liquidated and purchased at corresponding discounts by currently active bids in the ATOM ORCA liquidation queue. In this case, approximately 103 USK worth of atom is purchased at a 3% discount (i.e. for 100 USK), approximately 1040 USK worth of ATOM is purchased at a 4% discount (i.e. for 1000 USK), approximately 10500 USK worth of ATOM is purchased at a 5% discount, and finally the remaining 8457 USK is purchased at a 6% discount. Within a particular discount percentage, users fill their bids proportionally based on how much they have deposited. For example, of the 8457 USK purchased at a 6% discount, person A deposited 25% of the USK in the 6% column, person B deposited 35%, person C deposited 39.9%, and person D deposited 0.1%. As a result, person A receives 8457 USK \*25/100 worth of ATOM purchased at a 6% discount; person B receives 8457 USK \* 35/100 worth of ATOM purchased at a 6% discount; person C receives 8457 USK \*39.9/100 worth of ATOM purchased at a 6% discount; and person D receives 8457 USK \*0.1/100 i.e. 8.457 USK worth of ATOM purchased at a 6% discount so person D receives 8.457/0.94 worth of ATOM.&#x20;