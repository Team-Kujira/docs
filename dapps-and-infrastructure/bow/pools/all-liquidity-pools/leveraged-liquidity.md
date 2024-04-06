# Leveraged Liquidity

## Overview

The 'Leveraged Liquidity' tab displays information about your open leveraged LP position.&#x20;

<figure><img src="../../../../.gitbook/assets/image (164).png" alt=""><figcaption><p>Leveraged Liquidity tab overview</p></figcaption></figure>

The information displayed on this tab includes your position size, the amount of each asset borrowed, the current LTV on your loan, etc. You can also model what the LTV (loan-to-value) would be if you were to update your position.

## Updating an open Leveraged LP

<figure><img src="../../../../.gitbook/assets/image (165).png" alt=""><figcaption><p>What happens if I update my leveraged LP position by borrowing 0.5 <a href="../../../../tokenomics/kuji-token/">KUJI</a> and 0.1 ATOM</p></figcaption></figure>

It is possible to slide the LTV bar for both assets manually to attempt to borrow an open that opens your position to a specific desired LTV. Or you can manually enter however much of each asset you would like to borrow.&#x20;

After doing so, you see a little chart below on the left which displays the amount your LP token collateral increases or decreases, the amount of each asset that is being borrowed or repaid in GHOST, and. the net change of each asset in the LP balance.

The little chart below on the right displays the total amount of LP collateral you will now, the total dollar value of this LP collateral, the dollar value of the total debt your hypothetical (of 0.5 KUJI at 0.1 ATOM in this example) position would have, the LTV your leveraged LP would be updated to, and the nt change in LP collateral $ amount, net $ change in overall debt, and net change in overall LTV.

If you're satisfied with the overview, simply click the blue 'Update Position' button on the bottom left to update your LP to these new amounts. &#x20;

<figure><img src="../../../../.gitbook/assets/image (166).png" alt=""><figcaption><p>This is what the LP looks like after updating the leveraged LP position based on the criteria above.</p></figcaption></figure>

## Repay & Close&#x20;

When you are ready to close your leveraged LP position, simply hit the red 'Repay & Close' button on the bottom left and it will automatically fill up the LP page fields with the necessary values to close the position and display what would happen when doing such.

<figure><img src="../../../../.gitbook/assets/image (54).png" alt=""><figcaption><p>What happens after you hit the red 'Repay &#x26; Close' button on the bottom left</p></figcaption></figure>

Finally, hit the blue 'Update Position' button to repay and close your leveraged LP position. At the moment, there is a bug that doesn't allow you to unwind your positions all the way. So in the meantime until this is fixed, what is recommended is to unwind 99.99% of your position (for example to first click 'Repay & Close', then to enter a small amount of each asset to keep open such as 0.0001 KUJI and 0.0002 ATOM, this will unwind the vast majority of your KUJI/ATOM leveraged LP and leave dust.
