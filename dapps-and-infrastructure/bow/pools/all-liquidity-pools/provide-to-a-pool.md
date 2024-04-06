---
cover: ../../../../.gitbook/assets/Kujira BOW (1).png
coverY: 0
---

# Provide to a Pool

## Overview

The 'provide' tab for each liquidity pool contains a user interface for providing and withdrawing liquidity and data on total personal provided liquidity in addition to the basic header contained in the 'Overview', 'Provide', and 'Stake' pages).&#x20;

## My LP Balance

This section of the 'Provide' tab contains a connected wallet's LP token balance for that particular liquidity pool as well as its current dollar value and breakdown into component provided assets. LP tokens are acquired by providing liquidity and converting each asset from the token pair into some amount of LP tokens. Remember to stake any unstaked LP tokens on the '[Stake](stake-lp-with-a-pool.md)' page to obtain incentives and maximize rewards!

<figure><img src="../../../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Your LP balance info</p></figcaption></figure>

## Deposit Liquidity

Use the deposit UI to provide liquidity to a specific BOW liquidity pool. Adding liquidity is immediate. To add liquidity to a particular pool, the amounts of each pool asset must be balanced in value based on their current prices. The UI is user-friendly so simply enter an amount of tokens to deposit for either pool token  (on top or on bottom) and the UI will automatically balance the other asset's provision amount to match.&#x20;

The number of LP tokens to be minted by depositing said liquidity are displayed further down in the deposit UI. Lower slippage reduces fees, but may take longer (or be impossible) to execute depending on circumstance.   &#x20;

<figure><img src="../../../../.gitbook/assets/image (52).png" alt=""><figcaption><p>Depositing liquidity to the KUJI/ATOM pool based on the pair ratio between each token's price</p></figcaption></figure>

### Leverage your deposit

If you choose to leverage your deposit by selecting the slider near the 'Leverage my deposit' text, then you will see the following menu pop up for whatever specific pair you are dealing with.

<figure><img src="../../../../.gitbook/assets/image (53).png" alt=""><figcaption><p>Leveraged KUJI / ATOM liquidity pool deposit</p></figcaption></figure>

When you enter an amount to deposit on the LP for one of the tokens, the amount of the other token will automatically increase to match your selected liquidity deposit. In other words, based on the current exchange rate between KUJI and ATOM on FIN, if you try to deposit 5 KUJI, you'll be prompted to deposit 1.018797 ATOM along with it.

However, with a leveraged LP, you have the flexibility to choose to deposit more ATOM or KUJI (without changing the amount of the other correspond asset KUJI or ATOM) and borrow the remaining amount needed to balance the LP from GHOST at a rate depending on the current asset ratio between the two and a specific asset's current borrow rate in ghost. Some assets will have a high rate and others low.

The total borrowed shows the amount of the other asset you need to borrow from GHOST to keep the relative amount of assets you are depositing into the pool equal, the opening LTV of the position open depositing the liquidity, the current borrow interest rate on the open position, the LP tokens minted by opening this position, and the desired slippage you would like to select.

After accepting the terms and conditions, you just need to click the 'Borrow Funds & Deposit Liquidity' button on the user interface and pay gas fees to open a leveraged LP position.&#x20;

For any wallet, you can only have one leveraged LP position open at a time for a specific liquidity pair.

## Withdraw Liquidity

Use the withdraw UI to remove liquidity from a specific BOW liquidity pool. Withdrawing liquidity is immediate with no lock up. To withdraw LP tokens from a particular pool, simply enter an amount of LP tokens to withdraw. The estimated return upon converting those LP tokens back to their component assets is displayed further down in the UI.

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Withdrawing liquidity from the KUJI/ATOM pool based on the pair ratio between each token's price</p></figcaption></figure>

To unwind or manage an open leveraged LP position hit the blue 'Manage open position' button which replaces the 'Borrow Funds & Deposit Liquidity' button when you have an open leveraged LP position.

This will bring you to the '[Leveraged liquidity](leveraged-liquidity.md)' tab.
