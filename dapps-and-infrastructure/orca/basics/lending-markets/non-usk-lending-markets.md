# 🎑 Non-USK Lending Markets

## Overview

At the moment, all lending markets on ORCA use USK. As a result, users must obtain USK in order to be able to bid on liquidated collateral at a discount. However, in the future, non-USK lending markets will be available as well. To bid on them, it is necessary to acquire the relevant asset(s) being used to perform liquidations on that lending market. For example, Acala liquidations are projected to use the aUSD stablecoin.&#x20;

## How to place bids

To understand the ins and outs of the ORCA liquidation process, please refer to the explanations in the [lending markets section](./) as well as the provided ATOM liquidation example. Once the necessary bidding asset has been obtained, for a particular lending market, bids may be placed anywhere in the ORCA liquidation queue by choosing a desired liquidation discount at which to purchase the specific collateral associated with that ORCA lending market. To submit an ORCA bid, select the desired premium (discount), select the amount of \<bidding asset> to place a bid with, leave the 'auto-active my bid with SeaShanty' option selected or manually activate the bid at the end of this process (non-active bids will NOT purchase liquidated collateral at a discount), and then confirm acknowledgment that 'withdrawal of a successful bid will include a 0.5% fee (98% of ORCA fees are distributed to KUJI stakers and 2% go to the community pool). Finally, click place my bid to wrap up the process. Bids take a total of 10 minutes to activate. Sea Shanty which is a product by [Capybara Labs](../../../../governance/capybara-labs.md), a community validator, activates ORCA bids automatically as long as the service is enabled when setting a bid.&#x20;

## ORCA bid strategy&#x20;

Setting discount bids is a strategic process. Sometimes it might make sense to set several bids of different sizes at different premiums--sometimes it may make sense to set a large bid at an unlikely premium to attempt to profit greatly in the case of a black swan, often it may make sense to look at where users are the majority of bid premiums, and pick either the same premium of lower premiums to ensure that the active bids end up being used to purchase discounted collateral even if it is ultimately at a smaller discount. Part of the process of mastering how to set ORCA bids comes down to properly interpreting ORCA liquidation analytics which will be covered in the next section.

## Withdrawing liquidated collateral&#x20;

Once funds have been obtained after a successful liquidation event, simply click the withdraw button to withdraw purchased liquidated collateral minus the 0.5% withdrawal fee which goes to KUJI stakers.&#x20;
