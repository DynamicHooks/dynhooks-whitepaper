# Quote in a stock

Robinhood Chain carries Robinhood Stock Tokens: ERC-20 tokens tracking listed equities. A market on Dynamic Hooks can use one of them as its quote asset instead of ETH.

That changes what a market *is*. A market about a company's founder, quoted in the company's stock token, pays its creator, its holders and its launcher in that stock on every trade. Supporting the person and holding the business become the same position.

## Rules

- The quote asset must be on the engine's allowed list. The list starts with ETH and adds Stock Tokens one at a time, each with a published price feed and a staleness limit.
- A market's quote asset is fixed at launch. A program cannot change it.
- Stock Tokens carry their issuer's own transfer restrictions. The interface shows them before launch and before every trade. The engine does not override them.
- Markets quoted in a Stock Token start at a price expressed in that token, from the feed at launch.

This is the part of Dynamic Hooks that exists only on Robinhood Chain. It ships after ETH-quoted markets, as a step in [What comes next](what-comes-next.md).
