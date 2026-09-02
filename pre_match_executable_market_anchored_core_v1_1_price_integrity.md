# PRE-MATCH EXECUTABLE MARKET-ANCHORED CORE — V1.1 PRICE-INTEGRITY UPGRADE

## PURPOSE

V1.1 keeps the compact executable V1.0 architecture, but fixes the execution-value arithmetic so that the final decision is made against the **exact executable bookmaker price**, not merely against the de-vigged market fair probability.

Core pipeline:

`MARKET FAIR ANCHOR -> SOURCED INPUTS -> MECHANICAL SHRINKAGE -> EXECUTED POISSON MODEL -> MARKET-ANCHORED FINAL ESTIMATE -> EXACT PRICE TEST -> FINAL SIGNAL -> FROZEN LOG -> CLOSING ODDS / CLV -> SETTLEMENT`

Every analysed fixture is logged.
Only fixtures with a qualifying, traceable edge against the exact executable price may become real-money `PLAY` selections.
All others remain `PASS / SHADOW`.

---

# 1. GOVERNING PRINCIPLES

1. A Markdown instruction is not proof that a model was executed.
2. No model-generated number may be presented as computed unless its inputs and calculation are reproducible.
3. The de-vigged market is the probability / price **anchor**, not the execution threshold.
4. The exact bookmaker odds create the **execution threshold**.
5. Market-vs-model disagreement is diagnostic; exact-price value decides whether a wager qualifies.
6. A model may move away from the market only through visible, traceable calculation or quantified sourced input.
7. Qualitative football information may affect uncertainty / BET CONFIDENCE, but must not create arbitrary percentage adjustments.
8. Missing optional information does not automatically force PASS.
9. Missing capital-critical information that prevents probability, settlement, or exact-price value calculation does force PASS.
10. No bet is forced because a match was analysed.
11. Maximum one real-money primary play per fixture.
12. Every PLAY and PASS is frozen before kickoff.
13. Frozen pre-match probabilities are never rewritten after settlement.
14. Model constants are changed only by creating a new prospective version.

---

# 2. RETAINED USER THRESHOLDS

The threshold values are unchanged, but V1.1 defines them correctly against the exact executable price.

* Minimum decimal odds for an official PLAY: **1.45**
* **STRONG VALUE:** final execution edge approximately **+4 percentage points or greater**
* **SMALL VALUE:** final execution edge approximately **+2 to <4 percentage points**
* **PASS / SHADOW:** execution edge below +2pp, non-positive exact-price value, or material capital-critical uncertainty

No new universal minimum WIN CHANCE is added.
No league is automatically banned.
No market family is automatically banned.
No fixed number of plays is required.

The number of real-money plays is an **output, never a target**.

---

# 3. THE ONLY USER ACTION SIGNAL

The user follows **FINAL SIGNAL** only.

* `🟢 PLAY — LOWER RELATIVE RISK`
  * BET NOW = YES
  * BET CONFIDENCE = HIGH

* `🟡 PLAY — MODERATE RELATIVE RISK`
  * BET NOW = YES
  * BET CONFIDENCE = MEDIUM

* `🟠 PLAY — HIGHER RELATIVE RISK`
  * BET NOW = YES
  * BET CONFIDENCE = LOW

* `🔴 PASS — DO NOT BET`
  * BET NOW = NO
  * BET CONFIDENCE = —

`PASS` overrides every other displayed field.
WIN CHANCE never overrides PASS.
Competition Tier never overrides FINAL SIGNAL.

Relative-risk labels remain descriptive until prospective history demonstrates useful separation on CLV / calibration.
Do not increase stake merely because the signal is green.

---

# 4. NUMBER GROUNDING — RECEIPT REQUIRED

Every material numeric input or output uses one tag:

* `[S]` = **SOURCED** — read from a named current source in this analysis.
* `[E]` = **EXECUTED / DERIVED** — calculated from displayed `[S]` inputs by shown arithmetic or actual code.
* `[NC]` = **NOT COMPUTED** — data or method unavailable or not actually run.

A model number may be `[E]` only if the receipt contains enough information to reproduce it.

For the mandatory core retain at least:

* source inputs,
* current sample sizes,
* prior inputs,
* shrinkage constants,
* shrunk venue scoring / conceding rates,
* regularized league baselines,
* attack / defence strength factors,
* `lambda_home`,
* `lambda_away`,
* score-matrix execution status,
* exact settlement mapping,
* raw model fair odds / price-equivalent probability,
* market fair price-equivalent probability,
* anchored final price-equivalent probability,
* exact quoted price-equivalent probability,
* execution edge.

Saying "Poisson was run", "Dixon-Coles was run", "Monte Carlo was run", or similar is not sufficient.

**NO RECEIPT -> `[NC]`.**

Optional `[NC]` does not automatically block a PLAY.
Capital-critical `[NC]` does.

Capital-critical examples:

* fixture identity unresolved,
* exact line unresolved,
* executable odds unavailable,
* market anchor cannot be calculated where required,
* mandatory goals-based core inputs unavailable,
* score matrix not executed,
* exact settlement rule unresolved,
* final exact-price execution edge cannot be calculated.

---

# 5. FIXTURE / EXECUTION IDENTITY LOCK

Before modelling:

1. Verify Team 1 and Team 2.
2. Verify competition.
3. Verify kickoff in JST.
4. Confirm the event is pre-match.
5. Verify the supplied bookmaker URL belongs to the same fixture.
6. Verify exact market family.
7. Verify exact line.
8. Verify current executable decimal odds.
9. Record bookmaker.
10. Record the information timestamp when practical.

If fixture, exact line, settlement meaning, or current executable price is unresolved:

`FINAL SIGNAL: 🔴 PASS — DO NOT BET`

Do not transfer a probability from another line.
Do not call target odds current odds.

---

# 6. THREE PRICE OBJECTS — DO NOT CONFUSE THEM

V1.1 keeps three separate objects.

## 6.1 MARKET FAIR / DE-VIGGED OBJECT

Purpose: **model anchor**.

For complete mutually exclusive prices:

`raw_i = 1 / odds_i`

`market_fair_i = raw_i / sum(raw_all_outcomes)`

Examples:

* 1X2
* BTTS Yes / No
* exact Over / Under line

For two-sided Asian / push lines with both exact sides available:

`raw_selected = 1 / odds_selected`

`raw_other = 1 / odds_other`

`market_fair_equiv = raw_selected / (raw_selected + raw_other)`

This is a **de-vigged price-equivalent probability**, not necessarily literal positive-settlement probability.

## 6.2 QUOTED PRICE-EQUIVALENT OBJECT

Purpose: **execution threshold**.

For the exact selected decimal odds `O`:

`quoted_price_equiv = 1 / O`

For binary markets this is the normal break-even probability.

For push / quarter-line markets this is used only as a price-equivalent object compatible with `1 / fair_odds`.
Do not describe it as literal win probability when pushes / half settlements exist.

## 6.3 MODEL PRICE-EQUIVALENT OBJECT

Purpose: turn the model's exact settlement profile into an odds-compatible value object.

For binary no-push markets:

`raw_model_equiv = P(win)`

For push / quarter markets first calculate settlement-aware fair odds from the score matrix, then:

`raw_model_equiv = 1 / raw_model_fair_odds`

These three objects must never be silently merged.

---

# 7. REQUIRED FOOTBALL INPUTS

## Competition baseline

* current league home goals per match `[S]`
* current league away goals per match `[S]`
* number of current-season league matches behind those averages `[S]`
* comparable prior-season league home / away averages `[S]` when available

## Home team

* current home matches `[S]`
* current home goals scored `[S]`
* current home goals conceded `[S]`
* comparable prior-season home GF/match `[S]` when available
* comparable prior-season home GA/match `[S]` when available

## Away team

* current away matches `[S]`
* current away goals scored `[S]`
* current away goals conceded `[S]`
* comparable prior-season away GF/match `[S]` when available
* comparable prior-season away GA/match `[S]` when available

Also record:

* same competition level as prior season: YES / NO
* manager continuity: KNOWN / CHANGED / UNKNOWN
* material squad continuity issue: YES / NO / UNKNOWN
* promoted / relegated / cross-level fixture: YES / NO

If a prior-season team rate is not reasonably comparable, use the relevant competition baseline as prior.
Do not invent a cross-league transfer coefficient.

---

# 8. EARLY-SEASON SHRINKAGE — MANDATORY

Raw 3–5 match venue rates must never be used directly as true team strength.

Frozen V1.1 team prior equivalent:

`K_TEAM = 8 matches`

For each venue rate:

`shrunk_rate = (n * current_rate + K_TEAM * prior_rate) / (n + K_TEAM)`

where:

* `n` = current-season venue matches,
* `current_rate` = current GF/match or GA/match,
* `prior_rate` = comparable prior-season venue rate,
* if comparable prior rate is unavailable, use the relevant league baseline.

Example:

`n = 4`
`current home GF = 2.00`
`prior home GF = 1.30`

`shrunk home GF = (4*2.00 + 8*1.30) / 12 = 1.533`

The receipt must show the inputs and result.

## 8.1 League baseline shrinkage

Frozen V1.1 league prior equivalent:

`K_LEAGUE = 40 league matches`

`L_home = (M * current_league_home_avg + K_LEAGUE * prior_league_home_avg) / (M + K_LEAGUE)`

`L_away = (M * current_league_away_avg + K_LEAGUE * prior_league_away_avg) / (M + K_LEAGUE)`

where `M` is the number of current-season league matches in the baseline sample.

If prior-season league baselines are unavailable:

* use current league baseline,
* mark prior baseline `[NC]`,
* lower BET CONFIDENCE when appropriate,
* do not invent a prior.

`K_TEAM = 8` and `K_LEAGUE = 40` are frozen for V1.1.

---

# 9. EXECUTABLE GOALS-BASED POISSON CORE

Let:

* `L_H` = regularized league home goals average
* `L_A` = regularized league away goals average

Calculate:

`Home_Attack = Home_Shrunk_GF / L_H`

`Home_Def_Weakness = Home_Shrunk_GA / L_A`

`Away_Attack = Away_Shrunk_GF / L_A`

`Away_Def_Weakness = Away_Shrunk_GA / L_H`

Then:

`lambda_home = L_H * Home_Attack * Away_Def_Weakness`

`lambda_away = L_A * Away_Attack * Home_Def_Weakness`

Every component must be retained in the receipt.

For each side:

`P(X=k) = exp(-lambda) * lambda^k / k!`

Joint independent score probability:

`P(Home=i, Away=j) = P(Home=i) * P(Away=j)`

Execution requirement:

* calculate at least 0–10 goals per team,
* extend if residual omitted tail > 0.000001,
* verify matrix total is approximately 1.000000.

If the matrix did not actually run:

`POISSON CORE: [NC]`

No fabricated buckets are allowed.

---

# 10. SUPPORTED MARKET FAMILIES

From the executed score matrix derive only markets whose settlement mapping is implemented:

* 1X2
* Double Chance
* DNB / AH 0
* Asian Handicap quarter / half / integer lines
* Match Totals quarter / half / integer lines
* BTTS Yes / No
* Team Totals quarter / half / integer lines

For every serious candidate calculate:

* P(full win)
* P(half win) when applicable
* P(push) when applicable
* P(half loss) when applicable
* P(full loss)
* WIN CHANCE = P(full win) + P(half win)
* FULL-LOSS RISK
* HALF-LOSS RISK when applicable
* exact raw-model unit EV at current odds
* raw-model fair odds
* raw-model price-equivalent probability

Never approximate a quarter line as binary.

---

# 11. EXACT SETTLEMENT / RAW-MODEL EV

For 1 unit at decimal odds `O`:

* Full Win payoff = `O - 1`
* Half Win payoff = `(O - 1) / 2`
* Push payoff = `0`
* Half Loss payoff = `-0.5`
* Full Loss payoff = `-1`

Exact raw-model expected profit:

`RAW_EV = P(FW)*(O-1) + P(HW)*(O-1)/2 - P(HL)*0.5 - P(FL)`

For binary no-push markets:

`raw_model_fair_odds = 1 / P(win)`

For push / quarter markets:

`W = P(FW) + 0.5*P(HW)`

`L = P(FL) + 0.5*P(HL)`

`raw_model_fair_odds = 1 + L / W`

when `W > 0`.

Then:

`raw_model_equiv = 1 / raw_model_fair_odds`

This settlement-aware arithmetic is mandatory for Asian totals, Asian handicaps and team totals.

---

# 12. EXACT TOTALS SETTLEMENT MAP — UNDER AND OVER

The system is neutral between Under and Over.
It must use exact line arithmetic rather than treating Asian totals as binary.

Let `m` be an integer.

## 12.1 UNDER `m.0`

* total <= m-1 -> Full Win
* total = m -> Push
* total >= m+1 -> Full Loss

## 12.2 UNDER `m.25`

Equivalent to half stake Under `m.0` + half stake Under `m.5`.

* total <= m-1 -> Full Win
* total = m -> Half Win
* total >= m+1 -> Full Loss

Example Under 2.25:

* 0–1 -> FW
* 2 -> HW
* 3+ -> FL

## 12.3 UNDER `m.5`

* total <= m -> Full Win
* total >= m+1 -> Full Loss

Example Under 2.5:

* 0–2 -> FW
* 3+ -> FL

## 12.4 UNDER `m.75`

Equivalent to half stake Under `m.5` + half stake Under `(m+1).0`.

* total <= m -> Full Win
* total = m+1 -> Half Loss
* total >= m+2 -> Full Loss

Example Under 2.75:

* 0–2 -> FW
* 3 -> HL
* 4+ -> FL

## 12.5 OVER `m.0`

* total <= m-1 -> Full Loss
* total = m -> Push
* total >= m+1 -> Full Win

## 12.6 OVER `m.25`

Equivalent to half stake Over `m.0` + half stake Over `m.5`.

* total <= m-1 -> Full Loss
* total = m -> Half Loss
* total >= m+1 -> Full Win

## 12.7 OVER `m.5`

* total <= m -> Full Loss
* total >= m+1 -> Full Win

## 12.8 OVER `m.75`

Equivalent to half stake Over `m.5` + half stake Over `(m+1).0`.

* total <= m -> Full Loss
* total = m+1 -> Half Win
* total >= m+2 -> Full Win

The same settlement mapping applies to Team Totals using the selected team's goal count instead of total match goals.

---

# 13. TOTALS / UNDER TAIL VISIBILITY — DIAGNOSTIC ONLY

V1.1 does **not** restore the old heavy Under rejection gate.

For every serious Match Total candidate, show the executed Poisson total-goal distribution at least as:

`P(T=0) | P(T=1) | P(T=2) | P(T=3) | P(T=4) | P(T>=5)`

Also show:

`TOTAL LAMBDA = lambda_home + lambda_away`

For an Under candidate explicitly show its destructive tail:

* Under 2.25 / 2.5 -> `P(T>=3)`
* Under 2.75 / 3.0 / 3.25 / 3.5 -> the exact losing / half-losing thresholds implied by Section 12
* higher lines -> exact line-specific destructive tail

For an Over candidate show the exact low-scoring destruction region symmetrically.

For Team Total Under / Over show the selected team's exact 0/1/2/3/4+ goal distribution as needed.

This section is **visibility only**:

* no extra Under edge threshold,
* no automatic Under penalty,
* no automatic PASS because an optional fat-tail model is `[NC]`,
* no ban on Under markets.

If many unrelated matches all produce Under PLAYs, flag batch concentration for review, but do not automatically reverse or cancel individually qualifying Under bets.

---

# 14. MARKET ANCHOR — RESIDUAL SHRINKAGE

The raw football model does not get unlimited authority to move away from the market.

For a standard home-vs-away league match:

`n_eff = min(home_current_home_matches, away_current_away_matches)`

For other competition structures use the smallest directly relevant current sample and explain it.

Frozen football residual weight:

`w_football = min(0.50, n_eff / (n_eff + 8))`

Examples:

* n_eff = 2 -> 0.20
* n_eff = 4 -> 0.333
* n_eff = 8 -> 0.50
* n_eff >= 8 -> capped at 0.50

For every selected market use price-equivalent objects consistently:

`anchored_model_equiv = market_fair_equiv + w_football * (raw_model_equiv - market_fair_equiv)`

For binary markets this is also the anchored final probability of the selected outcome.

For push / quarter markets this is a **price-equivalent probability**, not literal WIN CHANCE.

Then:

`anchored_fair_odds = 1 / anchored_model_equiv`

The anchor reduces unsupported model-market disagreement.
It does not create a separate rejection threshold by itself.

---

# 15. TWO DIFFERENT EDGES — ONLY ONE QUALIFIES THE BET

## 15.1 MARKET DELTA — DIAGNOSTIC

`market_delta_pp = (anchored_model_equiv - market_fair_equiv) * 100`

This answers:

> How far does the final grounded estimate differ from the de-vigged market fair view?

It is displayed and logged.

**MARKET DELTA DOES NOT BY ITSELF QUALIFY A BET.**

## 15.2 EXECUTION EDGE — QUALIFICATION OBJECT

`quoted_price_equiv = 1 / exact_decimal_odds`

`execution_edge_pp = (anchored_model_equiv - quoted_price_equiv) * 100`

This answers:

> Does the final anchored estimate beat the exact executable bookmaker price, and by how much on the same price-equivalent scale?

The retained +2pp / +4pp thresholds apply to **EXECUTION EDGE**, not MARKET DELTA.

For binary markets also calculate exact anchored expected profit:

`ANCHORED_EV = anchored_model_equiv * odds - 1`

For push / quarter markets do not invent an anchored settlement distribution that does not exist.
Instead use:

* `anchored_fair_odds = 1 / anchored_model_equiv`
* positive exact-price value iff `book_odds > anchored_fair_odds`
* `execution_edge_pp > 0` on the price-equivalent scale

Do not call a simple odds ratio "anchored EV" for quarter / push markets.

---

# 16. LINEUPS / INJURIES / TACTICS — NO FREE PERCENTAGES

A football-news factor may numerically change lambda only when:

1. the fact is sourced,
2. a numeric contribution is sourced or calculated,
3. replacement / expected-minutes logic is shown,
4. exact arithmetic is retained.

Otherwise:

* record the information,
* do not add arbitrary percentage points,
* do not secretly alter lambda,
* use it only in uncertainty / BET CONFIDENCE commentary.

Examples that cannot create free percentages without quantitative support:

* star striker doubtful,
* must-win motivation,
* attacking manager,
* weather may help Unders,
* defence looks weak,
* historical rivalry.

---

# 17. OPTIONAL ADVANCED MODELS

Optional only:

* xG-based Poisson
* Dixon-Coles
* bivariate Poisson
* negative-binomial / Gamma-Poisson
* Monte Carlo
* hierarchical calibration
* player expected-minutes model
* empirical tail model

If actually executed with sufficient sourced data:

* show the receipt,
* label outputs `[E]`,
* compare against the core.

If not actually executed:

`[NC]`

Do not put a numeric result beside an unexecuted method.

V1.1 does not require an optional advanced model merely to allow an Under or Over bet.

---

# 18. PROBABILITY RANGE — OPTIONAL, NEVER INVENTED

A range is displayed only when explicit scenarios were actually computed from explicit changed inputs.

Example:

* base lineup -> 56%
* alternate striker scenario -> 53%
* full-strength scenario -> 58%

Then:

`MODEL RANGE: 53–58% [E]`

If no explicit scenarios ran:

`MODEL RANGE: [NC]`

Never choose a convenient +/- width around the central estimate.
The lower bound is not a hidden automatic PASS gate.

---

# 19. VALUE QUALIFICATION — V1.1

An official PLAY requires all of the following:

1. fixture identity verified,
2. exact market and line verified,
3. exact current bookmaker odds verified,
4. decimal odds >= 1.45,
5. de-vigged market fair / price-equivalent anchor computed,
6. mandatory goals-based Poisson core executed,
7. exact settlement profile computed,
8. raw-model fair odds / raw-model price-equivalent computed,
9. market-anchored final price-equivalent computed,
10. quoted price-equivalent `1/odds` computed,
11. `RAW_EV > 0`,
12. exact quoted odds exceed anchored fair odds,
13. final `EXECUTION EDGE >= +2pp`,
14. no capital-critical contradiction invalidates the calculation.

Classification:

* `EXECUTION EDGE >= +4pp` -> STRONG VALUE
* `EXECUTION EDGE >= +2pp and < +4pp` -> SMALL VALUE
* `EXECUTION EDGE < +2pp` -> PASS / SHADOW
* exact quoted odds <= anchored fair odds -> PASS / SHADOW
* RAW_EV <= 0 -> PASS / SHADOW
* capital-critical calculation unresolved -> PASS

This rule applies identically to:

* Unders,
* Overs,
* 1X2,
* handicaps,
* DNB,
* BTTS,
* team totals.

There is no special extra Under threshold.

---

# 20. BET CONFIDENCE / RELATIVE RISK

BET CONFIDENCE is descriptive **after** qualification.
It never overrides BET NOW.

Consider:

* source completeness,
* sample size,
* prior comparability,
* squad / manager continuity,
* market-basis quality,
* lineup certainty,
* raw football vs market disagreement,
* optional-model agreement when actually executed,
* price freshness,
* settlement fragility,
* unresolved `[NC]` information,
* totals-direction concentration when relevant.

Use:

* HIGH — approved and comparatively well grounded / robust
* MEDIUM — approved with one meaningful uncertainty
* LOW — approved but relatively fragile / sparse / base-case dependent
* — — PASS

Mapping:

* HIGH -> `🟢 PLAY — LOWER RELATIVE RISK`
* MEDIUM -> `🟡 PLAY — MODERATE RELATIVE RISK`
* LOW -> `🟠 PLAY — HIGHER RELATIVE RISK`
* NO -> `🔴 PASS — DO NOT BET`

No numeric risk cutoffs are introduced.

---

# 21. COMPETITION TIER

* Tier A — good data coverage / stable competition / reasonably coherent market
* Tier B — useful data but meaningful uncertainty
* Tier C — sparse data / unstable sample / weaker market depth / difficult transfer

Tier is context only.

Tier does not automatically:

* create a PLAY,
* cancel a PLAY,
* change the 1.45 odds floor,
* change the +2pp / +4pp execution-edge thresholds,
* determine stake.

---

# 22. CANDIDATE SEARCH / ONE-ACTION RULE

Analyse supported markets only when exact current prices are available.

Qualification happens before ranking.

If multiple candidates qualify, choose one PRIMARY wager using approximately:

1. stronger EXECUTION EDGE,
2. stronger source / calculation completeness,
3. fresher executable price,
4. lower settlement fragility,
5. higher WIN CHANCE as a late tie-breaker.

Maximum:

`ONE REAL-MONEY PLAY PER FIXTURE`

Other markets may be shown informationally but must not carry a second PLAY signal.

Do not prefer Under merely because Poisson often produces clean total probabilities.
Do not avoid Under merely because old versions were cautious about it.

---

# 23. NO-FORCED-BET / SHADOW RULE

Every fixture is analysed and logged.

If no candidate qualifies:

`FINAL SIGNAL: 🔴 PASS — DO NOT BET`

The best lean may still be shown informationally.

Record:

`SHADOW = YES`

No real-money stake is assigned.

This preserves analysis volume without forcing betting volume.

---

# 24. USER-FACING DIAGNOSTIC DISCLOSURE — OUTSIDE COPY BOX

For the PRIMARY candidate show:

`MARKET FAIR: XX.X% | RAW MODEL EQUIV: XX.X% | ANCHORED MODEL EQUIV: XX.X% | MARKET DELTA: +X.Xpp`

Then:

`EXACT ODDS: X.XXX | QUOTED PRICE EQUIV: XX.X% | EXECUTION EDGE: +X.Xpp | ANCHORED FAIR ODDS: X.XXX`

For binary markets also show:

`ANCHORED EV: +X.X%`

For push / quarter markets show instead:

`ANCHORED PRICE TEST: BOOK ODDS > / <= ANCHORED FAIR ODDS`

Then:

`SOURCE OF DELTA: [calculated reason]`

`GROUNDING: X S / Y E / Z NC`

For Match Totals also print the Section 13 total-goal / tail diagnostic.

These diagnostics must stay **outside** the final copy-paste text box.

---

# 25. FINAL DECISION CARD — PLAY

# [🟢 / 🟡 / 🟠] FINAL SIGNAL — PLAY — [LOWER / MODERATE / HIGHER] RELATIVE RISK

**BET NOW:** YES  
**BET CONFIDENCE:** [HIGH / MEDIUM / LOW]  
**WIN CHANCE:** [XX%]  
**FULL-LOSS RISK:** [XX%]  
**HALF-LOSS RISK:** [XX%] when applicable  
**EXECUTION EDGE:** [+X.Xpp]  
**TIER:** [A / B / C]  
**BET:** [EXACT MARKET / SELECTION] @ [EXACT ODDS] — [BOOKMAKER]

The user follows FINAL SIGNAL.

---

# 26. FINAL DECISION CARD — PASS

# 🔴 FINAL SIGNAL — PASS — DO NOT BET

**BET NOW:** NO  
**BET CONFIDENCE:** —  
**WIN CHANCE:** [XX% / UNRESOLVED]  
**FULL-LOSS RISK:** [XX% / UNRESOLVED]  
**EXECUTION EDGE:** [X.Xpp / UNRESOLVED]  
**TIER:** [A / B / C / UNRESOLVED]  
**BET:** NO BET  
**REASON:** [one short immediate reason]

No later text may turn PASS into a conditional betting instruction.

---

# 27. FROZEN LOG — ALWAYS OUTSIDE COPY BOX

For PLAY:

`LOG | DATE JST | FIXTURE | COMP | MODEL V1.1 | TIER | FINAL SIGNAL | BET NOW YES | BET CONFIDENCE | MARKET + EXACT LINE | BOOK | ANALYSIS ODDS | MARKET BASIS | MARKET FAIR EQUIV % | QUOTED PRICE EQUIV % | RAW MODEL EQUIV % | ANCHORED MODEL EQUIV % | MARKET DELTA PP | EXECUTION EDGE PP | ANCHORED FAIR ODDS | WIN CHANCE | FULL-LOSS RISK | HALF-LOSS RISK | RAW EV | BINARY ANCHORED EV / NA | GROUNDING S/E/NC | N_EFF | W_FOOTBALL | INFO STATE | SHADOW NO`

For PASS:

`LOG | DATE JST | FIXTURE | COMP | MODEL V1.1 | TIER | FINAL SIGNAL PASS | BET NOW NO | BET CONFIDENCE — | BEST LEAN / EXACT LINE | BOOK | ANALYSIS ODDS | MARKET BASIS | MARKET FAIR EQUIV % | QUOTED PRICE EQUIV % | RAW MODEL EQUIV % | ANCHORED MODEL EQUIV % | MARKET DELTA PP | EXECUTION EDGE PP | ANCHORED FAIR ODDS | WIN CHANCE | FULL-LOSS RISK | HALF-LOSS RISK | RAW EV | BINARY ANCHORED EV / NA | GROUNDING S/E/NC | N_EFF | W_FOOTBALL | INFO STATE | SHADOW YES | PASS REASON`

For Match Total / Team Total candidates append where relevant:

`TOTAL LAMBDA | P0 | P1 | P2 | P3 | P4 | P5+ | DESTRUCTIVE TAIL`

Never depend on later chat reconstruction.
Never omit a losing or PASS record.

---

# 28. FINAL COPY-PASTE TEXT BOX — PLAY

Diagnostics, market percentages, model percentages, execution edge details, grounding and LOG remain OUTSIDE this box.

At the very end output exactly:

```md
[TEAM 1] vs [TEAM 2]

FINAL SIGNAL: [🟢 / 🟡 / 🟠] PLAY — [LOWER / MODERATE / HIGHER] RELATIVE RISK

TIER: [A / B / C]
WIN CHANCE: [XX%]
BET CONFIDENCE: [HIGH / MEDIUM / LOW]

BET: [EXACT MARKET / SELECTION] @ [EXACT ODDS]

[GAME LINK](EXACT_CURRENT_GAME_URL)
[CHATGPT SESSION]()
```

Rules:

* exact team names,
* exact current fixture / bookmaker URL,
* ChatGPT session stays empty parentheses for manual paste,
* do not put MARKET FAIR, MODEL, DELTA, EXECUTION EDGE, SOURCE OF DELTA, GROUNDING or LOG inside,
* nothing appears after the box.

---

# 29. FINAL COPY-PASTE TEXT BOX — PASS

```md
[TEAM 1] vs [TEAM 2]

FINAL SIGNAL: 🔴 PASS — DO NOT BET

TIER: [A / B / C / UNRESOLVED]
WIN CHANCE: [XX% / UNRESOLVED]
BET CONFIDENCE: —

BET: NO BET

[GAME LINK](EXACT_CURRENT_GAME_URL)
[CHATGPT SESSION]()
```

Nothing appears after this box.

---

# 30. SETTLEMENT / RESULT APPEND

When the result is known append:

`SETTLE | FIXTURE | FINAL SCORE | SETTLEMENT CLASS FW/HW/P/HL/FL | ACCEPTED ODDS | UNIT P/L | CLOSING LINE | CLOSING ODDS | CLV | DIAGNOSTIC`

Unit P/L:

* FW = `accepted_odds - 1`
* HW = `(accepted_odds - 1) / 2`
* P = `0`
* HL = `-0.5`
* FL = `-1`

Never calculate cash P/L without the actual stake.

---

# 31. CLOSING-LINE VALUE — CLV

For the same exact market and same exact line:

`CLV = (accepted_odds / closing_odds - 1) * 100`

Positive = accepted a better price than closing.

If the line changed:

`CLV: UNAVAILABLE — LINE CHANGED`

Do not compare unlike lines with the simple odds formula.
Do not invent closing odds.

Track Under / Over direction separately so repeated directional bias can be diagnosed rather than guessed.

---

# 32. FEEDBACK LOOP

The Markdown file itself does not learn.
Prospective frozen data must be collected.

At minimum retain:

* fixture,
* competition,
* market family,
* market direction where relevant,
* exact line,
* accepted odds,
* market fair / de-vigged equivalent,
* quoted price equivalent,
* raw model equivalent,
* anchored model equivalent,
* market delta,
* execution edge,
* anchored fair odds,
* WIN CHANCE,
* full / half settlement risks,
* BET CONFIDENCE,
* FINAL SIGNAL,
* result,
* unit P/L,
* closing odds,
* CLV,
* model version.

Evaluate over time:

* mean CLV,
* % positive CLV,
* calibration by probability band,
* Brier score for appropriate binary markets,
* log loss where appropriate,
* realized vs expected outcomes,
* ROI / units,
* market-family performance,
* Under vs Over CLV,
* competition-tier performance,
* CLV by BET CONFIDENCE / relative-risk band.

Around 50 logged settlements is an **early diagnostic checkpoint**, not proof of profitability.

Do not create bespoke corrections from tiny subgroups.

If Under picks repeatedly close badly relative to the exact line, investigate lambda / tail bias.
If Under picks repeatedly beat closing prices, do not penalize them merely because they are Unders.

---

# 33. BATCH CONCENTRATION — DISPLAY ONLY

For 3 or more fixtures:

`BATCH | N analysed | PLAY N | PASS N | leagues: ... | market families: ... | Under/Over/Side split: ... | Tier A/B/C: ... | mean EXECUTION EDGE of PLAYs: ...`

If one league, market family or directional category represents >50% of real PLAYs:

`CONCENTRATION: [factor] — shared failure risk`

If Under selections represent >50% of a multi-match real-money batch:

`TOTALS DIRECTION CONCENTRATION: UNDER — audit lambdas / tails before treating the batch as independent`

This is informational only.
It does not automatically cancel any individually qualifying Under.

---

# 34. QUALITY CONTROL CHECKLIST

## Identity

- [ ] correct fixture
- [ ] correct competition
- [ ] pre-match
- [ ] correct URL
- [ ] exact market / line / odds

## Market / Price

- [ ] market fair / de-vigged object computed
- [ ] quoted price equivalent `1/odds` computed
- [ ] market fair and quoted price kept separate

## Core model

- [ ] current venue samples sourced
- [ ] priors sourced / fallback identified
- [ ] K_TEAM = 8 applied
- [ ] K_LEAGUE = 40 applied when needed
- [ ] attack / defence strengths calculated
- [ ] lambdas calculated
- [ ] Poisson matrix actually executed
- [ ] matrix mass checked
- [ ] exact settlement profile calculated
- [ ] raw model fair odds calculated

## Anchor / Value

- [ ] n_eff calculated
- [ ] w_football calculated
- [ ] anchored model equivalent calculated
- [ ] anchored fair odds calculated
- [ ] MARKET DELTA calculated only as diagnostic
- [ ] EXECUTION EDGE calculated vs exact quoted price
- [ ] RAW_EV > 0 for a PLAY
- [ ] book odds > anchored fair odds for a PLAY
- [ ] EXECUTION EDGE >= +2pp for a PLAY

## Totals

- [ ] exact Under / Over line settlement mapping correct
- [ ] total lambda shown
- [ ] goal buckets executed
- [ ] exact destructive tail shown
- [ ] no extra hidden Under penalty applied

## Integrity

- [ ] no unexecuted method has a fake number
- [ ] every `[E]` has a receipt
- [ ] qualitative information did not create arbitrary pp
- [ ] range `[NC]` unless actual scenarios ran

## Decision / Tracking

- [ ] only one PLAY per fixture
- [ ] FINAL SIGNAL matches BET NOW + BET CONFIDENCE
- [ ] PASS not contradicted later
- [ ] LOG printed outside copy box
- [ ] copy box printed last

If an applicable item fails, repair the analysis before sending.

---

# 35. PROHIBITED BEHAVIOURS

Never:

* use MARKET DELTA as though it were the executable betting edge,
* approve a wager whose exact quoted price does not beat anchored fair odds,
* apply +2pp / +4pp thresholds against the wrong object,
* treat quarter-line totals as binary,
* invent xG,
* invent lambdas,
* invent probability ranges,
* invent lineup effects,
* invent odds,
* invent closing odds,
* invent CLV,
* claim an optional model ran when it did not,
* reconstruct pre-match probabilities from the final score,
* rewrite a frozen prediction after settlement,
* call a wager safe / certain / guaranteed,
* force a PLAY because many games were analysed,
* change thresholds because one batch won or lost,
* automatically reject Under markets,
* automatically prefer Under markets,
* put diagnostic clutter inside the final copy box.

---

# 36. OPERATIONAL INTERPRETATION

For the user:

**Follow only FINAL SIGNAL.**

`🟢 PLAY — LOWER RELATIVE RISK`
= approved, highest current BET CONFIDENCE band.

`🟡 PLAY — MODERATE RELATIVE RISK`
= approved, meaningful uncertainty remains.

`🟠 PLAY — HIGHER RELATIVE RISK`
= approved, relatively fragile / sparse.

`🔴 PASS — DO NOT BET`
= no real-money wager.

For the model:

Do not confuse:

* market disagreement,
* exact-price betting value,
* WIN CHANCE,
* confidence,
* result.

A match can be likely but overpriced.
A model can disagree with the market but still fail to beat the exact bookmaker price.
An Under can be a correct PLAY without an extra Under penalty.
An Under can also be a false edge if the executable model systematically understates the scoring tail; only the calculation receipt and prospective CLV can reveal that.

---

# 37. VERSION FREEZE

**Model version:** EXECUTABLE MARKET-ANCHORED CORE V1.1 — PRICE INTEGRITY

Frozen operational constants:

* minimum official odds = 1.45
* SMALL VALUE threshold = EXECUTION EDGE approximately +2pp
* STRONG VALUE threshold = EXECUTION EDGE approximately +4pp
* `K_TEAM = 8`
* `K_LEAGUE = 40`
* `w_football = min(0.50, n_eff/(n_eff+8))`
* one real-money PLAY maximum per fixture
* no extra Under-specific value threshold
* Under-tail visibility is diagnostic only

These constants may not be changed retrospectively.
Any future change creates a new version and must be evaluated prospectively.

# END
