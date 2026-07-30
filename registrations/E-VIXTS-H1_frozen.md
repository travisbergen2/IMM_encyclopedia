# E-VIXTS-H1 Protocol — VIXTS-T2 Prospective Holdout (FROZEN)

**ADOPTED AND FROZEN: T₀ = 2026-07-29 (America/Chicago), by Travis Bergen's instruction in Hyperagent thread cmrs7brj51qvb07adbri63nsf.** Canonical text of Hyperagent document cms55eo160prl06ad1e4rzra8 v1 (DESIGN v0.1), unchanged at adoption. Every VIX/VIX3M event after T₀ is holdout data. Post-freeze changes only as dated addenda in the live document.

## 0. Status, Freeze Mechanics, and the Honest Power Statement

Freeze occurred at adoption (above); this file's SHA-256 committed to GitHub provides the third-party timestamp. Because the data is in the future, registration is inherently uncontaminated — the integrity requirements are contemporaneous capture (§2) and no post-freeze edits outside dated addenda.

**The power statement:** the frozen signal fires ≈2.4 non-overlapping events/year. Per-event net returns have historical sd ≈ 4.5% against a +1.9% expected mean. At a 36-month horizon (expected n ≈ 7): SE ≈ 1.7%, so even a fully real premium reaches placement-null significance with only ≈30% probability. **This holdout is a disconfirmation-capable, weak-confirmation instrument** — it can kill the transfer claim decisively, and can usually only corroborate it. TRANSFER-CERTIFIED is reachable but requires either luck or a larger-than-historical effect; stated before event one so a CONSISTENT outcome cannot be spun as certification, nor an absence of certification as failure of the premium.

**Registered expectations (frozen):** modal outcome at 36 months = TRANSFER-CONSISTENT; early disconfirmation is real and priced in — the 2020-cluster dependence of the historical estimate means a calm-regime holdout may show much weaker rebounds. Season directional record 3/7; held loosely.

## 1. Frozen Instrument (all by reference, zero new parameters)

**Signal (verbatim from the lab's frozen Cj-VIXTS-T2 spec):** VIXCLS/VXVCLS ratio; event = upward crossing of the trailing 756-trading-day 90th-percentile threshold; entry at next available TradeLocker SPX500 daily close; exit at the 20th available daily close after entry; no overlapping events (an event during an open window is ignored).

No parameter in this protocol is new. Any change to the signal creates a NEW candidate requiring its own historical work; it cannot be absorbed here.

**Costs:** per event, all-in cost = 2 × observed half-spread at the actual entry/exit timestamps (captured by the read-only gateway) + actual overnight swap/financing for the holding period once the broker rate is known. Until the swap rate is captured, primary accounting uses the frozen 50bp all-in scenario with 0bp/100bp sensitivities reported alongside; capturing the real swap number is what the manual-trade instrument (§3) exists for.

## 2. Data Capture and the Matched Null

**Contemporaneous capture:** at least weekly, an automated read-only job snapshots (a) FRED VIXCLS and VXVCLS, (b) TradeLocker SPX500 daily closes via the gateway, (c) the live spread; each snapshot appends to an immutable manifest with SHA-256 hashes and capture timestamps. Signals are computed from data as captured at the time — retroactive revisions are recorded as discrepancies, and the as-captured value governs.

**Primary endpoint:** mean all-in net 20-day event return across holdout events.

**Null (placement-matched, from the holdout period itself):** at evaluation, 2,000 sets of pseudo-events — same count, same no-overlap spacing constraints, placed uniformly over the SAME holdout calendar — with identical net-return machinery. p = frac(null means ≥ observed mean), one-sided.

**Secondary (descriptive, never gating):** sizing-cage shadow account — each event's P&L at the 7.9% exposure cap, cumulated; positive-fraction vs the null's; per-era comparison to historical partitions.

## 3. Demo-Account Hosting Without Breaking Fail-Closed

**The lab never places orders — that boundary is structural and stays.**

**Layer 1 (the verdict layer): pure paper.** Every signal, entry, exit, and net return computed from captured data. No order anywhere. The §4 verdict is computed from THIS layer only.

**Layer 2 (the cost-capture instrument): manual minimum-lot trades, optional.** On a signal, the lab emits a signal notice (date, instrument, direction, 0.01-lot size, exit date). If Travis chooses, HE manually places that trade on the designated demo account 2104772 and closes it on the exit date. The lab only READS the resulting fills, swaps, and statements via the read-only gateway and reconciles them against the paper prediction. This captures actual fill slippage and the actual overnight swap rate. Missed/skipped trades change nothing in Layer 1; no order-placing code path exists; whether to place any manual trade is Travis's decision alone, on a demo account, at minimum size.

**The minimum-lot coincidence (verified):** 0.01 lot × lot-size 10 × SPX500 ≈ 7,400 → ≈ $740 notional ≈ 7.4% of a $10k account — almost exactly the 7.9% sizing cap the worst historical path implies. Worst observed intrawindow path −12.7% × $740 ≈ −$94 ≈ 0.94% of account, inside the 1% design loss and far inside the 3%/6% rules.

Incidental note, separated from research: Layer-2 trades would also satisfy demo inactivity requirements — an account-hygiene convenience, never a reason to trade.

## 4. Verdict Grammar and Schedule (frozen)

**Checkpoints:** quarterly addenda are DESCRIPTIVE ONLY (events logged, no p-values). Verdict computations occur only at: (i) an early-stop check after each event once n≥4, (ii) the 24-month event-drought check, (iii) the 36-month primary evaluation.

- **TRANSFER-DISCONFIRMED (early stop allowed):** at any n≥4, running all-in mean ≤ −2.0%; or at 36 months, observed mean ≤ 0.
- **INCONCLUSIVE-BY-DESIGN:** fewer than 3 events by month 24; or capture-integrity failure spanning an event.
- **TRANSFER-CONSISTENT (modal):** at 36 months, observed mean > 0 and within the historical predictive band (+1.4% to +2.4% after costs), placement-null p ≥ 0.05. Grade: prospectively corroborated, uncertified.
- **TRANSFER-CERTIFIED:** placement-null p < 0.05 at 36 months (or at any n ≥ 6 if the effect is large enough — same test, no threshold change). Acknowledged ≈30% power even under truth.
- **Extension rule (frozen):** if 36 months ends TRANSFER-CONSISTENT, ONE 24-month extension under identical rules; a second is not permitted.

**What any pass means (binding):** certification of premium TRANSFER at ~+0.3–0.5%/yr account-level under compliant sizing — a structure result and a risk-engine component, not an income line. All events and the final verdict enter the ledger (kind=registered_prospective, protocol E-VIXTS-H1).

## Adoption Record

- T₀: 2026-07-29
- Designated Layer-2 account: 2104772 (Aqua Funded demo)
- Evaluation dates: early-stop checks from n≥4; drought check 2028-07-29; primary evaluation 2029-07-29; single permitted extension to 2031-07-29.
