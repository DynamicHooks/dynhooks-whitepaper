# What cannot change

Three things are not in any template, cannot be added by any program, and are not parameters:

1. **A way to remove liquidity.** The locking contract has no such function.
2. **A way to reach an escrow without its claim.** The escrow moves on a verified claim, or to the holders after the window. Nothing else.
3. **A fee above 3%.** The hook refuses it at the engine level.

If a future version of the protocol changes any of these, it is a different protocol, and this document will say so on its first page.
