# E-TREND-1 Protocol — Few-Shot Registered Test of Slow-Trend / Vol-Targeted Candidates on a Factory-Disjoint Corpus (Pre-Registered)

Canonical frozen text of Hyperagent document cmrs7q3na0qas06ad7t5w8e4f, version 1, created 2026-07-19 in thread cmrs7brj51qvb07adbri63nsf. Author: the Riemann agent for Travis Bergen. Any divergence between this file and the live document's sections 0–10 must favor this file for registration purposes; post-freeze changes are permitted only as dated addenda in the document's Addenda section.

## 0. Status and Registration Discipline

**Status: FROZEN at registration (2026-07-19, thread cmrs7brj51qvb07adbri63nsf), before any data contact.** No real market data has been downloaded, inspected, or summarized for this protocol at freeze time. No availability probe has been made — the basket carries frozen fallback rules instead.

This is an **internal pre-registration**, the same instrument used by every prior E-series protocol (E-EA-OR-1/2/3, E-EA-J6-1, E-FAC-1). Its statistical function — fixing the hypothesis set, N, thresholds, and reporting rules before data — is fully served internally. What internal registration does NOT provide is third-party proof of timestamp; that is recovered (optionally) by committing the SHA-256 hash of this frozen text to a public GitHub repository at freeze time (§10). Any post-freeze edit to sections 1–9 must be a labeled, dated addendum; silent edits void the registration.

**Nothing in this protocol bears on RH or any IMM mathematical claim. No claim of market edge is made or testable here beyond the frozen endpoints. A PASS is historical-backtest evidence only — it would queue the spec for the paper-trade bridge, never for capital.**

## 1. Motivation and Provenance (Declared Priors)

**Why this test exists.** The strategy factory (thread cmr6r2s5j2qec06adbh5d6p4h) holds an append-only ledger of N=7,596 trials with zero G5 survivors. Its positive control (2026-07-19, multi-seed) measured: false-positive rate 0/10 noise worlds; power ≈ 0% against a true net Sharpe 0.63; power ~20–40% against true 1.55. Conclusion: at N≈8,000 the deflation bar (~4.2 SE) is unclearable by realistic edges — breadth of search and power to certify trade off directly. The registered few-shot test is the only instrument in the program that can certify an edge: with the hypothesis set fixed at ~10 before data, the family-max noise bar drops to ~1.6–1.7 SE, and a single pre-designated flagship faces a ~1.65 SE bar.

**Declared priors (everything already seen that could bias this design):**
1. The factory searched tsmom / ma_cross / breakout / reversion / carry / seasonality / dual_mom / xasset_filter families on ~20y daily data for 6 instruments (recoverable identities: BTC, ETH, CL/WTI, an S&P-class index; two not recovered; amptrader symbol groups were crypto/metals/oil/sp500). Best factory OOS artifacts: tsmom_BTC_126 and slow-trend/vol-target G4-passers. **Family-level selection is therefore contaminated** — trend was chosen partly because it survived deepest in the factory — and is handled by (a) corpus disjointness (§4, VG-3) and (b) the secondary DSR sensitivity at inflated N (§6, H2b).
2. E-FAC-1 used ES daily bars 2016–2026 (block-bootstrap seed data).
3. Literature prior: time-series momentum is a documented, published, heavily crowded premium (Moskowitz-Ooi-Pedersen 2012 lineage), with post-publication decay (McLean-Pontiff; Chen-Velikov cost erosion). Published diversified-portfolio net Sharpe estimates post-2010 cluster ≈ 0.3–0.5 — BELOW this test's flagship MDE (§7).
4. No statistic of any kind has been computed on any instrument in the E-TREND-1 basket (§4) within this program.

**Registered default / evidential asymmetry (pre-stated):** the modal expected outcome is **FAIL or POSITIVE-BUT-UNDERPOWERED**. A FAIL is consistent with crowding-decay and leaves the retail-loses prior unrefuted (no damage to the trend literature is claimed). A PASS would be surprising, must survive the placebo gate, and still would NOT establish a live edge — it earns only a paper-trade-bridge slot. The asymmetry: this test can meaningfully KILL the 'our slow-trend implementation is worth paper-trading' hypothesis; it can only weakly support it.

## 2. Hypotheses

**H1 (primary — flagship, N=1).** The pre-designated flagship spec S1 (§3), evaluated on the disjoint corpus (§4) under the frozen cost model (§5), delivers a positive net annualized Sharpe ratio distinguishable from zero and from a signal-timing placebo:
- H1a: one-sided stationary-block-bootstrap 95% CI for the flagship's net annualized Sharpe excludes 0 (p_boot < 0.05), AND
- H1b: the flagship's net Sharpe exceeds the 95th percentile of 200 circular signal-time-shift placebo nulls (shift the whole signal series by a uniform-random offset ≥ 260 trading days, re-run the identical portfolio machinery — destroys signal-return alignment, preserves both marginals and autocorrelation).
Both must hold for H1 PASS.

**H2 (secondary — family, N=10).** At least one of the 10 specs achieves Deflated Sharpe (Bailey–López de Prado, N=10 trials, full higher-moment correction) ≥ 0.95. Reported two ways: H2a at the honest local N=10; H2b sensitivity at N=50 (family-selection contamination penalty per Declared Prior 1). H2 cannot rescue a FAIL of H1 into a PASS; it can upgrade PARTIAL.

**H3 (descriptive only, no threshold).** Vol-targeted variants vs equal-notional twins: sign and size of the Sharpe difference (tests whether the OR-2-surviving EWMA-33 risk layer earns anything here). Explicitly exploratory.

## 3. The Ten Frozen Specs

All specs are **diversified portfolios over the full basket** (§4), not per-instrument bets — portfolio aggregation is one of the three registered power levers. Signals computed on data through close t; positions applied to close-to-close return t+1→t+2 (act-from-next-close, same convention as the factory backtester). Position per instrument ∈ {−1, 0, +1} × weight. No parameter may be changed after freeze; there are no grids.

**Vol-targeting (VT) definition (frozen):** per-instrument ex-ante daily vol = sqrt(EWMA span-33 of squared daily log returns) (the E-EA-OR-2 winning estimator, lagged one day); position scaled to target 10% annualized per-instrument vol, leverage clamped to [0.25, 4.0]; portfolio = mean of instrument P&L streams (equal risk weight). Equal-notional (EN) twin: weight 1/K per instrument, no scaling.

| # | ID | Signal (long if >0, short if <0, flat if undefined) | Sizing |
|---|----|----|----|
| **S1** | **tsmom_252_21_vt (FLAGSHIP)** | sign of total log return over days [t−252, t−21] (12-month momentum, skip-month, the literature-standard theory-motivated spec) | VT |
| S2 | tsmom_252_21_en | same as S1 | EN |
| S3 | tsmom_126_0_vt | sign of log return over [t−126, t] | VT |
| S4 | tsmom_126_0_en | same as S3 | EN |
| S5 | tsmom_63_0_vt | sign of log return over [t−63, t] | VT |
| S6 | tsmom_blend_vt | mean of the three sign signals (63/126/252-21); position = sign of mean, flat if 0 | VT |
| S7 | macross_50_200_vt | sign of (SMA50 − SMA200) | VT |
| S8 | macross_50_200_en | same as S7 | EN |
| S9 | tsmom_252_21_vt_lag5 | S1 signal executed with 5 additional days of lag (execution-robustness twin) | VT |
| S10 | tsmom_126_0_vt_long | S3 signal, long-only (shorts → flat) | VT |

Warm-up: first 273 trading days of each instrument produce no positions. Instruments enter the portfolio only when their signal is defined; portfolio divisor = count of active instruments that day.

## 4. Corpus (Disjoint by Construction)

**Data source (frozen):** Stooq free daily CSV endpoint (https://stooq.com/q/d/l/?s=<symbol>&i=d), daily closes, full available history through 2026-07-17 (last complete trading week before freeze). Downloaded once, hashed, and cached; the cached file is the corpus.

**Basket (8 instruments, frozen with fallbacks):**

| Instrument | Primary symbol | Fallback symbol |
|---|---|---|
| DAX index | ^dax | dax (futures cont.) |
| Nikkei 225 | ^nkx | ^nikkei |
| USD/JPY | usdjpy | jpy=x-equivalent on stooq |
| AUD/USD | audusd | — |
| Copper (HG cont.) | hg.f | — |
| Sugar #11 (SB cont.) | sb.f | — |
| Coffee C (KC cont.) | kc.f | — |
| Wheat (ZW cont.) | zw.f | — |

**Frozen fallback rules:** (i) if a primary symbol is unavailable or fails VG-1, try its listed fallback once; (ii) instruments failing both are DROPPED and named in the report; (iii) if fewer than 6 instruments survive, verdict is INCONCLUSIVE-BY-DESIGN (no endpoint computed); (iv) no symbol not in this table may enter the corpus.

**Disjointness rationale (VG-3):** the basket excludes every recoverable and every plausible member of the factory universe — no crypto, no oil, no gold/silver, no S&P-class index, no EURUSD, and none of the amptrader groups (crypto/metals/oil/sp500) except copper, which is declared as the single judgment call (industrial metal; amptrader's 'metals' traded precious metals). Exclusion clause: if the factory's exact six-list is ever recovered and any basket instrument appears in it, that instrument's contribution is excluded post-hoc and the overlap reported prominently; if the flagship verdict flips under exclusion, the flipped verdict governs.

**Overlap in TIME with factory data is permitted and unavoidable** (both use history ending 2026-07); disjointness is at the instrument level, which is what the multiplicity accounting requires — the 7,596 trials never computed a statistic on these series.

## 5. Cost Model

Frozen, same structure as the factory backtester: per-side proportional cost applied to every position CHANGE (|Δposition| × cost). Indices and FX: 10 bp per side. Commodity futures (hg.f, sb.f, kc.f, zw.f): 20 bp per side. No financing/borrow modeled (declared simplification — biases AGAINST shorts being expensive, i.e., mildly optimistic; noted in report). **Economic gate:** H1 PASS additionally requires the flagship to retain net Sharpe > 0 at 2× costs (reported as part of H1; if it passes at 1× but fails at 2×, verdict is PASS-FRAGILE, treated as PARTIAL).

## 6. Endpoints and Verdict Rules

Primary metric: net annualized Sharpe = mean(daily net portfolio return)/sd × sqrt(252), full post-warm-up sample.

**Bootstrap (frozen):** stationary block bootstrap on the flagship's daily net return series, expected block length 20 days, 10,000 resamples, one-sided p = fraction of resampled Sharpes ≤ 0.

**Placebo (frozen):** 200 circular shifts of the signal matrix by uniform-random offsets in [260, T−260], identical machinery; threshold = 95th percentile of placebo Sharpes.

**DSR (frozen):** Bailey–López de Prado deflated Sharpe with skew/kurtosis correction, benchmark SR₀ = expected max of N i.i.d. null Sharpes at the realized T; H2a N=10, H2b N=50.

**Verdict table (frozen):**
- **PASS** = H1a AND H1b AND 2×-cost gate, all on the flagship.
- **PARTIAL** = flagship fails but ≥1 other spec clears bootstrap p < 0.005 (Bonferroni 0.05/10) AND the placebo gate; or PASS-FRAGILE per §5.
- **FAIL** = neither; the few-shot trend hypothesis is dead on this corpus at this power, and the honest next lever is more T or new instrument classes — NOT more specs.
- **INCONCLUSIVE-BY-DESIGN** = VG failure per §8 or basket < 6.

All ten specs' Sharpes, CIs, and DSRs are reported in full regardless of verdict (no cherry-picking survivors).

## 7. Power / MDE (computed analytically before freeze — no data used)

SE of annualized Sharpe ≈ sqrt((1 + SR²/2)/T_years). Assumed usable T ≈ 20 years (basket median; if realized T differs, recompute and report — the MDE clause binds on realized T):
- SE ≈ 0.23 at SR≈0.
- H1a alone needs realized SR ≥ ~1.65×SE ≈ **0.38**.
- 80% power for H1a requires true SR ≥ (1.645+0.84)×0.23 ≈ **0.57**.
- H2a (DSR≥0.95, N=10) needs realized SR ≈ (1.57+1.645)×0.23 ≈ **0.74** — high; H2 is expected to fail even for genuinely positive premia (stated now so its failure cannot be spun).

**Underpowered clause (frozen):** the published post-2010 diversified-trend net Sharpe prior (≈0.3–0.5) sits BELOW the 80%-power MDE. Therefore: a FAIL with flagship point estimate in (0, 0.38) and bootstrap CI overlapping both 0 and 0.5 is reported as **FAIL-UNDERPOWERED-FOR-LITERATURE-PRIOR** — the test cannot distinguish 'decayed-but-real premium' from zero at this T. Only a flagship point estimate ≤ 0 counts as evidence against the premium itself. If realized T_years < 12 (basket median), the whole test is INCONCLUSIVE-BY-DESIGN regardless of endpoint values.

## 8. Validity Gates (any failure blocks endpoint reporting)

**VG-1 Data hygiene (per instrument):** ≥ 3,000 daily rows; no duplicate dates; ≤ 5% missing-day rate vs its own trading calendar; no |daily log return| > 0.5 (indices/FX) or > 0.8 (commodities); prices strictly positive. Failing instruments → fallback → drop rule (§4).

**VG-2 Basket sufficiency:** ≥ 6 surviving instruments AND median usable history ≥ 12 years, else INCONCLUSIVE-BY-DESIGN.

**VG-3 Disjointness assertion:** automated check that no corpus symbol maps to {BTC, ETH, WTI/CL, ES/SPX/S&P500, GC/gold, silver, EURUSD} or any crypto/oil/precious-metal/sp500 instrument; plus the exclusion clause of §4.

**VG-4 Harness validation on synthetic worlds (BEFORE any real download):** (a) planted-trend world — persistent-drift regime paths (drift levels calibrated as in the factory positive control) where the flagship machinery must recover net Sharpe ≥ 0.5 on 20 synthetic instruments × 5,000 days; (b) pure-noise world — 10 GBM instruments, flagship |Sharpe| must have bootstrap CI covering 0 and placebo gate must NOT fire in ≥ 18/20 seeded runs. Failure → fix harness, re-run VG-4, document every iteration; real data stays untouched until VG-4 passes.

**VG-5 Leak oracle:** shifting all signals FORWARD by +1 day must not increase flagship Sharpe by more than 1 SE (a large improvement under future-shift = lookahead bug); plus code assertion that position at t uses closes ≤ t and earns return t+1→t+2.

**VG-6 Corpus immutability:** SHA-256 of the downloaded corpus file recorded before endpoint code runs; endpoints computed only against that hash.

## 9. Deliverables and Post-Test Path

Definition of done: harness code (etrend1/harness.py + families), unit tests (including VG-4/VG-5 as tests), README (design, parameter table, how to run), results JSON, and the verdict logged here as a dated addendum plus a row in the framework audit ledger.

Post-test paths (frozen now): PASS/PARTIAL → the surviving spec(s) go to the factory's paper-trade bridge (forward-only activation, ≥126 live days, graduation/kill rules already frozen in that module) — never to capital. FAIL → the trend line closes on this corpus; successor tests must change T or instrument class, not spec count. In every case the trials enter a new E-TREND ledger file (10 rows, kind=registered_fewshot) kept separate from the factory ledger to preserve both counts' integrity.

## 10. External Timestamp (optional, post-freeze)

After this document is frozen, its canonical text is exported to a file, SHA-256 hashed, and the hash (plus title and freeze date, not necessarily the full text) is committed to a public GitHub repository under Travis's account. The commit timestamp provides third-party proof that the registration predates the data. This step is mechanical and adds no statistical validity beyond §0; recorded here so its presence or absence is never ambiguous.
