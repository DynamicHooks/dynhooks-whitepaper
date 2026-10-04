# Who gets paid

Every trade pays a fee on the quote side, taken inside the swap by the hook and distributed in the same transaction. The fee rate and the routing are part of the market's economics and can change by rule, within the limits below.

## The declared set

A market declares its recipients at launch. The engine knows six kinds:

| Recipient | Who |
| --- | --- |
| Creator | The person or team the market is about. Paid directly once verified; held in escrow until then. |
| Launcher | The wallet that created the market. |
| Holders | Everyone holding the market token, by balance and time, through the holders pool. |
| Protocol | Dynamic Hooks. Funds buybacks and operations; pays referral links from its own share. |
| Referral | The wallet whose link brought the trade, paid from the protocol share. |
| Escrow | The creator's share while unverified. |

A program can move shares between these. It cannot add a seventh.

## The default: the Person template

| Recipient | Before the creator verifies | After |
| --- | --- | --- |
| Creator | 2.00% (to escrow) | 1.50% (direct) |
| Launcher | 0 | 0.50% |
| Holders | 0.50% | 0.50% |
| Protocol | 0.50% (of which up to 0.25% to a referral link) | same |

The switch from the left column to the right is one rule: `when Verified(ownership) then RouteToCreator`. Until it fires, the launcher's share goes to the creator, so launching a market for someone is never a way to tax them.

## Escrow

The creator's share accrues in a contract keyed to the creator's identity, not to any wallet. It moves in exactly two cases: the creator proves the identity and claims it, or the claim window passes and it is paid to the holders pool. It is never burned and never reachable by the launcher, by the protocol, or by any rule.

## Referral links

Every wallet has a link for every market. A trade that arrives through a link pays up to a quarter point of that trade to the link's owner, out of the protocol share. The other recipients are untouched.
