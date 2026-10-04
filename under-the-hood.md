# Under the hood

| Contract | Role |
| --- | --- |
| MarketFactory | Creates token, pool, locked position and program in one call. Pausable for new launches only. |
| MarketToken | Fixed-supply ERC-20. Notifies the holders pool on transfer. |
| DynamicHook | The Uniswap v4 hook. Takes the fee inside the swap, routes it, enforces liquidity guards, holds each market's economics, exposes `evaluate`. One instance serves every market. |
| ProgramRegistry | Templates, rule encoding and validation, per-market programs. Rejects anything outside the engine's limits at creation. |
| Verifier | Typed-signature attestations, the verifier allow-list, nonces and deadlines. |
| CreatorEscrow | Holds the creator's share by identity until claimed or swept. |
| HoldersPool | Reward-per-token distribution to holders of a market. |
| IncentiveVault | Pre-funded per-market vault for `ReleaseIncentive`. |
| LiquidityLock | Holds the position. No removal function. |
| MarketRouter | Exact-input swaps with the referral payload. Holds nothing. |
| QuoteRegistry | Allowed quote assets, price feeds, staleness and sequencer checks. |

All contracts are verified on the explorer at deployment. Addresses are on the [Addresses](addresses.md) page.

## Trust

- Sells, claims, withdrawals, sweeps and `evaluate` cannot be paused.
- New launches can be paused by the multisig. Existing markets are unaffected.
- Parameter changes apply only within the bounds in [The numbers](the-numbers.md), are announced before they take effect, and never apply to a past trade.
- No contract holds a key to any market's liquidity or escrow.
