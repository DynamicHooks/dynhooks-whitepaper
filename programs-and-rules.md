# Programs and rules

A **program** is an ordered list of **rules**. A rule has the form:

```
when <condition>  then <action>   [once | repeatable]   [after <rule>]
```

The hook reads the market's current **economics** on every swap: the fee rate, the routing table, the liquidity mode, the rewards switch. Rules change those values. Nothing else can.

## Conditions

| Condition | What proves it | Example |
| --- | --- | --- |
| `Verified(event)` | A signature from an allow-listed verifier, bound to this market, with a nonce and a deadline | the creator owns the handle; the team hit a public milestone |
| `State(metric op value)` | Read from the chain at evaluation time | liquidity ≥ 50 ETH; cumulative volume ≥ 1,000 ETH; 30 days since launch; holders ≥ 500 |
| `Agent(key)` | A call from an allow-listed agent address, **and** the rule's own State or Verified check still passing | an agent fires "lower the fee" the block liquidity crosses the line |
| `Vote(threshold)` | On-chain signal from holders of the market token (later release) | the community turns rewards on |

Agents execute; they do not decide. A rule whose only condition is an agent is rejected when the program is created. An agent can make a true rule fire sooner. It cannot make a false rule fire at all.

## Actions

| Action | Limit the engine enforces |
| --- | --- |
| `SetFee(bps)` | 0 to 300. Never above 3%. |
| `SetRouting(recipients, shares)` | Shares sum to the fee; recipients only from the market's declared set |
| `RouteToEscrow` / `RouteToCreator` | The claim switch. The escrow is reachable only by its claim. |
| `ActivateRewards` / `DeactivateRewards` | Turns the holders' share on or off. Accrued balances are never clawed back. |
| `SetLiquidityMode(mode)` | `locked` or `locked_plus_buyback`. Removal is not a mode. |
| `ReleaseIncentive(amount, to)` | From the market's pre-funded incentive vault only, capped per rule at creation |

## Evaluation

Anyone can call `evaluate(market, rule, proof)`. If the condition holds, the action is applied in that transaction and a `RuleFired` event is emitted with the rule, the proof and the new economics. If it does not hold, the call reverts and nothing changes. We run an agent that evaluates every market's State rules every block they could plausibly fire; anyone else can run one too.

## Reading a program

Every market's program is public and readable in the interface: each rule, its condition, whether it has fired, when, and what it changed. A market with a program nobody can read is not a market on Dynamic Hooks.
