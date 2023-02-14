# 🔀 Swap

## [https://blue.kujira.app/swap](swap.md#https-blue.kujira.app-swap)

## Simple Token Swap User Interface

The BLUE 'Swap' tab (much like the BOW 'Swap' tab) is a simple token swap user interface. Token swaps occur by placing [FIN](../fin/) market orders or fixed price limit orders behind the scenes. Swaps are currently limited to [FIN](../fin/) token pairs. To trade between two assets without a direct [FIN](../fin/) pair, you can first trade for [USK](../usk-stablecoin.md) or axlUSDC as necessary, depending on the target asset, using the BLUE swap UI. At most, you may need to make up to 3 trades.

## How to Swap Tokens

A detailed visual guide for swapping tokens on BLUE can be found [here](product-guides/how-to-swap-tokens.md) in the product guides section.&#x20;

### Instant Swap

Instant swaps are simple market swaps that execute immediately for maximum convenience. Instant swap fees are always 0.15% of the traded tokens. (FIN limit order fees are 0.075%)

To perform an instant swap, first choose a token to exchange away and enter that token name on the left side. Second, choose a token to obtain and enter that token on the right side. Third, enter an amount of tokens to exchange away. The right side will display the estimated return in the new token.

The current 'Swap Rate' and corresponding 'Swap Fee' as well as the 'Estimated return after fees' are listed below. If satisfied with the above, click the blue 'Instant Swap' button and pay gas fees to complete the transaction.

#### Advanced Settings

Advanced settings only apply to instant swaps. These settings display additional information and options to work with when initiating swaps.

These settings distinguish between the current market rate and the swap rate. When a swap is sufficiently large, the prices of the token being sold and bought may change partway through the transaction as liquidity leaves the [FIN](https://fin.kujira.app/) orderbook causing the swap and market rates to differ. Thus, the swap rate reflects the average exchange rate between the two assets.&#x20;

The price impact reflects the change in exchange rate between the two assets upon liquidity leaving the FIN orderbook and completing the transaction as explained above.

The slippage limit reflects the maximum allowed change in exchange rate upon performing a swap. Swaps will fail if the order size is too large while the slippage limit is too small. Higher slippage tends to correlate with worse average execution price (swap rate).   &#x20;

### Fixed Price Swap

Fixed price swaps are special limit orders placed at the current market exchange rate between two tokens. Fixed swap orders only get filled at the current market exchange rate, which means that they often take some time to fully execute after initiation. Track orders on [FIN](https://fin.kujira.app/) or get notified when the rest fills via [SeaShanty](../../governance/capybara-labs.md).

To perform a fixed price swap, first choose a token to exchange away and enter that token name on the left side. Second, choose a token to obtain and enter that token on the right side. Third, enter an amount of tokens to exchange away.

Next, click the white text that reads 'Fixed Price Swap' to see an expanded menu. The 'Fixed Swap Rate', 'Return after fees', as well as the 'Estimated return filled instantly' are listed in that dropdown menu. If satisfied with the above, click the blue 'Fixed Price Swap' button and pay gas fees to initiate the fixed price swap.

