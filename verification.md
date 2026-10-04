# Verification

`Verified(event)` rules depend on someone attesting that something happened. Dynamic Hooks keeps that role small, auditable and replaceable.

## Verifiers

A verifier is a signing key on the engine's allow-list. It signs a typed message: the market, the event, the subject, a nonce and a deadline. The hook checks the signature, the nonce and the deadline, then evaluates the rule. A signature for one market cannot be replayed on another.

At launch the protocol runs the first verifier. The allow-list is public, additions and removals are announced before they take effect, and a market can require signatures from more than one verifier.

## Events

| Event | How it is established |
| --- | --- |
| `ownership(platform, handle)` | A code placed in the handle's public profile, or an OAuth login, checked by the verifier |
| `ownership(wallet)` | A signed message from the wallet |
| `milestone(id)` | A public, dated, verifiable statement defined in the program at launch (a URL, a contract address, a number on-chain) |

A `Verified` rule names the event it needs at creation. The verifier cannot invent events a program did not ask for.

## Agents

An agent is any address allowed to call `evaluate` on rules marked for agents. The agent pays gas. The rule still has to be true: an agent cannot sign for a verifier, cannot read state that is not there, and cannot fire a rule twice if it is `once`.

## What a verifier can and cannot do

It can delay a true claim by refusing to sign. It cannot move funds, change economics directly, or sign for an event the program did not define. If a verifier goes dark, the allow-list is updated and the claim proceeds with another.
