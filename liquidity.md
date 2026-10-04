# Liquidity

At launch the entire token supply is placed as one single-sided position in the market's Uniswap v4 pool, from the starting price upward. The position is held by a contract with no function that removes liquidity. Not paused, not time-locked, not governed: absent.

Fees earned by that position accrue to the position and stay in the pool.

## Modes

A program can set the market's liquidity mode:

- `locked` — the default. Nothing moves.
- `locked_plus_buyback` — a share of the protocol's fee from this market buys the market token on the open market and adds it to the locked position.

Both modes keep the position locked. There is no mode in which liquidity leaves.

## Why single-sided

Because it means the launcher puts in nothing but the creation fee, holds nothing at launch, and cannot have pre-bought. The first buyer pays the starting price. There is nothing to dump.
