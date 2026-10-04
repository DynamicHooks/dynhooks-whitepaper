# How a market is born

A market on Dynamic Hooks is three things created in one transaction:

1. **A token.** Fixed supply, minted once, no mint function, no owner. The default is 1,000,000,000 units.
2. **A pool.** A Uniswap v4 pool between the token and a quote asset (ETH by default; see [Quote in a stock](quote-in-a-stock.md)), opened at a published starting price, with the whole supply placed as a single-sided position and locked in a contract that has no withdraw function.
3. **A program.** The list of rules that govern the market's economics, chosen from a template and filled in by the launcher. See [Programs and rules](programs-and-rules.md).

The launcher pays a small creation fee in ETH and signs once. There is no presale, no allocation to the launcher, and no way to seed the pool with less than the full supply. From the first block the market is tradable, the liquidity is locked, and the program is live.

## What the launcher decides

- The template, and the blanks the template exposes (thresholds, recipients, windows).
- The quote asset, from the allowed list.
- The token's name and symbol.
- Who the market is **about**, if the template has a creator (a handle on a supported platform, or a wallet).

## What the launcher cannot decide

- A fee above the engine's cap.
- A recipient outside the market's declared set.
- Any path that removes liquidity.
- Any path that reaches an escrow without its claim.

Those are properties of the engine, not of the template. They are listed in [What cannot change](what-cannot-change.md).
