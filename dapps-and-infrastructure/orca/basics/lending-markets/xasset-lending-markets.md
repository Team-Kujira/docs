# xAsset Lending Markets

## Overview

Although many lending markets on ORCA use USK. Since the launch of GHOST, there are ORCA markets with other bid denominations. Users must obtain those assets to bid on liquidated collateral at a discount in those markets. All of these markets have xAsset bid denominations. xAssets such as xUSK, xaxlUSDC, xKUJI, xATOM, etc. can be obtained by lending the corresponding assets (USK, axlUSDC, KUJI, ATOM, etc.) on [GHOST](../../../ghost-money-market/).

xAsset lending markets can be separated into two subgroups: stablecoin lending markets & non-stablecoin lending markets. ORCA stablecoin lending markets operate identically to USK lending markets. The biggest difference is that xAssets accrue yield over time from GHOST borrow interest--so even if these markets stay stagnant in the short-term, you are earning yield from GHOST. However, the real fun begins with non-stablecoin lending markets.

### Sell Yield Bearing Assets up to 43% Above Local Market Tops

Non-stablecoin lending markets operate almost identically to USK lending markets with a major twist. Liquidating stablecoins at a discount by bidding with xAssets is equivalent to selling those yield bearing xAssets for stablecoins at a premium above the current market price.

For example, if you bid on USK with xKUJI at a 10% discount, you are actually attempting to sell yield bearing xKUJI at 11.1% above the market price. Since liquidations occur at local bottoms--in this case--you would effectively be selling (yield bearing) KUJI at 11.1% above a local market top. This unlocks many new possibilities.

Bidding at a 30% discount is equivalent to spending 30% fewer tokens worth of the denomination asset to buy $1 of the liquidated stablecoin. So if Y xATOM is $1, you would spend 0.7Y or $$\frac{7}{10}\text{Y}$$ xATOM to receive that dollar worth of stables. And you could spend Y xATOM to obtain $$ $\frac{10}{7} $$or $1.43 worth of stables. In other words, you're selling that xATOM 43% above the market price when an ATOM short position against USK is liquidated. &#x20;

## How to place bids

To understand the ins and outs of the ORCA liquidation process, please refer to the explanations in the [lending markets section](./) as well as the provided ATOM liquidation example. Once the necessary bidding asset has been obtained, for a particular lending market, bids may be placed anywhere in the ORCA liquidation queue by choosing a desired liquidation discount at which to purchase the specific collateral associated with that ORCA lending market. To submit an ORCA bid, select the desired premium (discount), select the amount of the bidding asset to place a bid with, leave the 'auto-active my bid with SeaShanty' option selected or manually activate the bid at the end of this process (non-active bids will NOT purchase liquidated collateral at a discount), and then confirm acknowledgment that 'withdrawal of a successful bid will include a 0.5% fee (98% of ORCA fees are distributed to KUJI stakers and 2% go to the community pool). Finally, click place my bid to wrap up the process. Bids take a total of 10 minutes to activate. Sea Shanty which is a product by [Capybara Labs](../../../../governance/capybara-labs.md), a community validator, activates ORCA bids automatically as long as the service is enabled when setting a bid.&#x20;

## ORCA bid strategy&#x20;

Setting discount bids is a strategic process. Sometimes it might make sense to set several bids of different sizes at different premiums--sometimes it may make sense to set a large bid at an unlikely premium to attempt to profit greatly in the case of a black swan, often it may make sense to look at where users are the majority of bid premiums, and pick either the same premium of lower premiums to ensure that the active bids end up being used to purchase discounted collateral even if it is ultimately at a smaller discount. Part of the process of mastering how to set ORCA bids comes down to properly interpreting ORCA liquidation analytics which will be covered in the next section.

## Withdrawing liquidated collateral&#x20;

Once funds have been obtained after a successful liquidation event, simply click the withdraw button to withdraw purchased liquidated collateral minus the 0.5% withdrawal fee which goes to KUJI stakers.&#x20;
