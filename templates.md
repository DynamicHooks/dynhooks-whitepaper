# Templates

A template is a saved program with blanks. Launching from a template fills the blanks and installs the rules in one transaction. The first templates:

## Person

A market about a person with a handle. Fee 3%. Routing as in [Who gets paid](who-gets-paid.md).

- `when Verified(ownership) then RouteToCreator` — once
- `when State(days_since_launch ≥ 90) and not claimed then SweepEscrowToHolders` — once

## Creator

A market launched by its own creator, verified at launch.

- `when State(liquidity ≥ L) then SetFee(150)` — once
- `when State(volume ≥ V) then ActivateRewards` — once

## Milestone

A team market with rewards off until something real happens.

- `when Verified(milestone) then ActivateRewards` — once
- `when Verified(milestone) then ReleaseIncentive(A, holders)` — once, after the rule above

## Stock-quoted

Any of the above with a Robinhood Stock Token as the quote asset. See [Quote in a stock](quote-in-a-stock.md).

Templates are added by the protocol and, later, by $DHOOKS governance. Every template is published with its rules in full before any market can use it.
