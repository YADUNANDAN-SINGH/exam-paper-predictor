# CBSE Class XII Mathematics 2026: prediction test report

Retrospective test of the exam-paper-predictor skill. The prediction was built only from the 2021–2025 papers (11 board papers of 2022–2025 plus CBSE's sample papers up to 2025-26), frozen with SHA-256 hashes, sent to the user, and only then compared with the real paper of 9 March 2026. Every number below comes from `scripts/score_2026.py`.

**Read this first.**

- The model that ran this test was trained on data up to June 2026, after the exam. It may have seen the 2026 paper in training, so treat every score as **likely optimistic**. A clean test needs an exam after the model's cutoff.
- Before the freeze, a search result and a site listing showed about 31 question titles that turned out to be from set **65/1/1**. The 65/1 series (65/1/1, 65/1/2) is therefore reported separately as contaminated. The headline uses series 2, 3, 4 and 5 only.
- Mock 1's question **types** came from code with no hand edits. The wording was written by hand, and one Mock 1 question (Q32) turned out to be the same question, same matrices and equations, as a 2026 question (65/2/1 Q32a). It is an older, widely circulated question; scoring is by type, so it adds nothing to the numbers.
- The 2026 questions were labelled by an independent sub-agent that never saw the prediction (it had only the frozen taxonomy, the labelled 2022–25 bank and the 2026 texts). The matching itself is code.

## Headline (clean sets: 65/2/1, 65/3/1, 65/4/1, 65/5/1)

| Measure | Mock 1 | All mocks (1 + 2 as built) | All mocks (1 + 2 mechanical) |
|---|---|---|---|
| Type hit, by marks | **32.5%** | 59.0% | 57.7% |
| Type hit, by count | 34.9% | | |
| Topic (chapter) coverage, by marks | **51.3%** | 77.2% | 77.6% |
| Topic coverage, by count | 57.8% | | |
| Same type anywhere in the paper (lenient, not headline) | 66.4% | | |

Share of the real papers' marks in Tier 1 + Tier 2 question types (from the frozen Important-Topics PDF): **90.8%** (Tier 1 alone 52.1%).

Sensitivity, not headline: if every item the grader marked 'doubtful' took whichever of its two candidate types scored better, Mock 1's type hit would be 32.9%.

For comparison, the blind backtest on the July 2025 compartment paper gave 46.7% type hit and 85.0% topic coverage.

## Every set

| Set | Items | Printed marks | Mock 1 type hit (marks) | by count | Topic coverage | All mocks (as built) | All mocks (mechanical) | Tier 1+2 share | Note |
|---|---|---|---|---|---|---|---|---|---|
| 65/1/1 | 54 | 109 | 22.9% | 31.5% | 47.7% | 67.0% | 56.0% | 85.3% | contaminated |
| 65/1/2 | 55 | 111 | 22.5% | 30.9% | 46.8% | 65.8% | 55.0% | 79.3% | contaminated |
| 65/2/1 | 54 | 109 | 26.6% | 27.8% | 35.8% | 48.6% | 46.8% | 83.5% | clean |
| 65/3/1 | 54 | 109 | 31.2% | 38.9% | 43.1% | 64.2% | 60.6% | 91.7% | clean |
| 65/4/1 | 52 | 107 | 42.1% | 36.5% | 72.0% | 59.8% | 57.0% | 96.3% | clean |
| 65/5/1 | 52 | 107 | 29.9% | 36.5% | 54.2% | 63.6% | 66.4% | 91.6% | clean |

Contaminated series mean (65/1/1, 65/1/2): Mock 1 type hit 22.7%, topic coverage 47.2%.

## Why it scored lower than the backtests

Baselines scored with the same strict code on the same labels (these are diagnostics, not predictions):

| Blueprint | Clean sets: type hit | topic coverage | same type anywhere | Contaminated sets: type hit |
|---|---|---|---|---|
| Mock 1 (final method: SQP-anchored, weight 0.6) | 32.5% | 51.3% | 66.4% | 22.7% |
| CBSE SQP 2025-26 used as-is | 32.5% | 51.3% | 66.4% | 22.7% |
| Frequency-only blueprint (v0, no SQP weight) | 43.3% | 60.6% | 76.4% | 50.9% |
| Mock 2 as built (v0 + 12 hand edits) | 40.0% | 61.5% | 70.8% | 57.3% |

1. **Mock 1 reproduced the 2025-26 sample paper.** Its 52 slots are exactly the SQP's question types, section for section and mark for mark (checked in code), because the final method gave the latest SQP 60% of the weight in every section. So in the strict layout score the skill added nothing over the SQP. The 2026 setters did not follow the SQP's layout: they moved chapters between sections (inverse-trig domain as a 5-mark Section D question in 65/2/1, functions in Sections B and C, area, rates and matrices as case studies). About two-thirds of the marks (66.4%) are question types that Mock 1 contains somewhere, but only about half of those (32.5 points) sit in the same section.
2. **The simpler method was better this year.** The frequency-only blueprint would have scored 43.3% instead of 32.5%. The backtest had already shown this on the July 2025 paper (51.4% vs 46.7%), and the SQP weighting was kept anyway on the strength of the March 2025 results, which were not fully out-of-sample.
3. **The Mock 2 hand edits only helped on the contaminated series.** Mock 2 as built beat its own mechanical list on 65/1 (57.3% vs 50.9%) but not on the clean sets (40.0% vs 43.3%). That is what contamination from the pre-freeze 65/1/1 titles would look like, so the 'as built' combined numbers are not used in the shareable line.
4. **Chapter-level advice held up.** The Tier 1 + Tier 2 types of the frozen Important-Topics PDF carried 90.8% of the clean papers' marks.

Robustness: pooled over all clean marks instead of averaging sets, Mock 1's type hit is 32.4% and topic coverage 51.2%; dropping the one 65/3/1 question the grader had to infer (Q33, missing from the source) gives 32.8% and 51.8%.

## Exact-question overlaps (reported, not counted)

- Mock 1 Q32 (show AB = 6I, then solve x − y = 3, 2x + 3y + 4z = 17, y + 2z = 7) is the same question as 65/2/1 Q32(a). It is an older, widely circulated question.
- Mock 2 Q34(a) uses the same pair of lines, r = (î+2ĵ+k̂) + λ(î−ĵ+k̂) and r = (2î−ĵ−k̂) + μ(2î+ĵ+2k̂), as 65/5/1 Q35(b), which asks for p given the shortest distance 3/√2. The pair is a standard NCERT exercise.
- Both were written before the 2026 paper was opened, but the model's training data runs past March 2026, so independence cannot be proven. Scoring is by question type, so neither changes any number.

## Source notes from the grader

- 65/3/1: one page of the Scribd copy is missing; Q33 (5 marks) is absent and was inferred as graphical LPP from the unit weightage (scored as a miss either way, since Mock 1 has no LPP in Section D).
- 65/1/2: Q23 on shaalaa appears to be a copy of 65/1/1 Q25, so that set's inverse-trig count may be inflated; it is a contaminated set and not in the headline.
- Several sets have three case studies with an internal choice (54 items / 109 printed marks instead of 52 / 107). Every printed option is counted, as the rules require.
- 65/3/1 and 65/4/1 do not print case-study sub-part marks; the standard 1 + 1 + 2 split was used.

## Section breakdown (Mock 1, mean of clean sets)

| Section | Type hit | Topic coverage |
|---|---|---|
| A | 46.2% | 78.8% |
| B | 21.4% | 46.4% |
| C | 27.8% | 36.1% |
| D | 29.2% | 45.8% |
| E | 38.2% | 57.0% |

## Biggest misses (clean sets, marks not matched by type, summed over the four papers)

| Question type | Marks missed | Where | Why |
|---|---|---|---|
| AOI-AREA — Area of a region bounded by curve(s)/lines using integration | 26 | 65/2/1 A; 65/2/1 E; 65/3/1 A; 65/3/1 E; 65/4/1 A; 65/4/1 D; 65/5/1 A; 65/5/1 D | in Mock 1 but in other sections or too few slots: B:Q23b, C:Q28a, C:Q28b |
| MAT-ALGEBRA — Matrix products/powers/equations: A^2=kA, find X from XA=B,  | 17 | 65/2/1 A; 65/3/1 A; 65/3/1 D; 65/4/1 A; 65/4/1 C; 65/4/1 E; 65/5/1 A | not in Mock 1 (in Mock 2: A:Q2) |
| FUN-INJ-SURJ — Show/check a given function is one-one / onto / bijective | 16 | 65/2/1 B; 65/3/1 D; 65/4/1 A; 65/4/1 C; 65/5/1 E | not in Mock 1 (in Mock 2: D:Q35b) |
| MAT-INV-SOLVE — Find A^-1 (3x3, adjoint) and solve a linear system, incl. wo | 13 | 65/3/1 D; 65/4/1 E; 65/5/1 D | not in Mock 1 (in Mock 2: D:Q32) |
| 3D-SD — Shortest distance between skew or parallel lines | 13 | 65/3/1 D; 65/4/1 C; 65/5/1 D | not in Mock 1 (in Mock 2: D:Q34a) |
| AOD-MONOTONIC — Increasing/decreasing intervals; prove monotonic; condition  | 11 | 65/2/1 D; 65/3/1 B; 65/4/1 B; 65/5/1 B | in Mock 1 but in other sections or too few slots: A:Q9 |
| INT-PARTS — Integration by parts, incl. e^x[f(x)+f'(x)] forms | 11 | 65/3/1 C; 65/4/1 D; 65/5/1 C | in Mock 1 but in other sections or too few slots: B:Q23a |
| AOD-RATE — Rate of change / related rates | 10 | 65/2/1 B; 65/3/1 A; 65/4/1 A; 65/4/1 E | in Mock 1 but in other sections or too few slots: C:Q27 |
| INT-SPECIAL — Special standard integrals: dx/(ax^2+bx+c), (px+q)/sqrt(ax^2 | 10 | 65/2/1 C; 65/3/1 C; 65/4/1 A; 65/5/1 C | not in Mock 1 (in Mock 2: C:Q27a) |
| VEC-BASICS — Magnitude, unit vector, position vectors, section formula, c | 9 | 65/2/1 B; 65/4/1 B; 65/5/1 C | in Mock 1 but in other sections or too few slots: A:Q14, A:Q15 |
| INT-DEF-PROP — Definite integral by properties: f(a+b-x), even/odd, modulus | 9 | 65/2/1 C; 65/3/1 C | in Mock 1 but in other sections or too few slots: A:Q11, D:Q33a |
| PROB-BAYES — Total probability and Bayes' theorem (incl. two-stage experi | 9 | 65/2/1 E; 65/3/1 E; 65/4/1 C; 65/5/1 E | in Mock 1 but in other sections or too few slots: E:Q38(i), E:Q38(ii) |

## Per-question tables

Hit = `type` (same method as a Mock 1 question in the same section), `topic` (same chapter, different method) or `miss`. Each Mock 1 question can be used once. Labels are the independent grader's; '?' marks items it flagged as doubtful.

### 65/1/1 (contaminated)

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | 2 cos^-1 x = y: interval in which y lies | ITF-DOMAIN-RANGE | Q1: graph of cos⁻¹(x/2) | topic | same chapter as Mock 1 Q1 (ITF-GRAPH), different method |
| 2 | 1 | Which order cannot be that of a row matrix | MAT-TYPES | Q2: order of B when A′B, BA′ defined | type | same method as Mock 1 Q2 |
| 3 | 1 | Which transpose rules hold: (A+B)', (A-B)', (AB)', (kAB)' | MAT-SYM-SKEW ? | Q3: skew-symmetric entries | type | same method as Mock 1 Q3 |
| 4 | 1 | Relation between two given 3x3 determinants Delta1 and Delta2 | DET-EVAL | Q6: 2×2 trig determinant | type | same method as Mock 1 Q6 |
| 5 | 1 | Value of x making |cos x sin x; -cos x sin x| = 1 | DET-EVAL | Q4: |adj 2A| | topic | same chapter as Mock 1 Q4 (DET-PROPS), different method |
| 6 | 1 | A, B skew-symmetric: which combination is also skew-symmetric | MAT-SYM-SKEW | Q5: inverse of 2×2 | topic | same chapter as Mock 1 Q5 (MAT-INV-SMALL), different method |
| 7 | 1 | Least value of x^3 - 12x on [0,3] | AOD-EXTREMA | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 8 | 1 | int 3ax/(b^2 + c^2 x^2) dx = A log|...| + K: find A | INT-SUB | Q12: ∫x²e^{x³}dx | type | same method as Mock 1 Q12 |
| 9 | 1 | int_{-1}^{1} x^3/(x^2 + 2|x| + 1) dx via odd function | INT-DEF-PROP | Q11: odd-function definite integral | type | same method as Mock 1 Q11 |
| 10 | 1 | Area between y = x|x|, x-axis, x = -1 and x = 1 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 11 | 1 | Integrating factor of R dx/dy + Px = Q with P, Q, R in y | DE-LINEAR | Q10: x dy − y dx = 0 | topic | same chapter as Mock 1 Q10 (DE-VARSEP), different method |
| 12 | 1 | Order and degree of d/dx(e^y) = 0 | DE-ORDER-DEGREE | — | miss | not in Mock 1; in Mock 2 (A:Q6) |
| 13 | 1 | p making i+2j+3k and 2i-pj+k perpendicular | VEC-DOT | Q13: scalar projection | type | same method as Mock 1 Q13 |
| 14 | 1 | m making three given position vectors collinear | VEC-BASICS | Q14: distance from x-axis | type | same method as Mock 1 Q14 |
| 15 | 1 | |a|=8, |b|=3, |a x b|=12: find |a.b| | VEC-CROSS ? | Q20: A-R cross product | type | same method as Mock 1 Q20 |
| 16 | 1 | Perpendicular length from (2,5,7) to line x/1=y/0=z/0 (x-axis) | 3D-FOOT-IMAGE ? | — | miss | not in Mock 1; in Mock 2 (D:Q34b) |
| 17 | 1 | Feasible-region figure, Z = 5x + 7y: maximum minus minimum | LPP-CORNER | Q17: max Z at corners | type | same method as Mock 1 Q17 |
| 18 | 1 | Degree of an LPP objective function | LPP-CONCEPT | Q16: point outside a half-plane | type | same method as Mock 1 Q16 |
| 19 | 1 | A-R: P(prime | odd) for a die; P(A|B) = P(A u B)/P(B)? | PROB-COND | Q18: dice, conditional | type | same method as Mock 1 Q18 |
| 20 | 1 | A-R: lines x=py+q, z=ry+s perpendicular iff pp'+rr'=1? | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 21a | 2 | Continuity at x=3 of piecewise |x-3|/(2(x-3)) and (x-6)/6 | CD-CONT | Q22: d/dx log(sec x+tan x) | topic | same chapter as Mock 1 Q22 (CD-CHAIN), different method |
| 21b | 2 | sqrt3 (x^2+y^2) = 4xy: dy/dx at (1/2, sqrt3/2) | CD-IMPLICIT | Q24: d(e^{tan x})/d(sin x) | topic | same chapter as Mock 1 Q24 (CD-CHAIN), different method |
| 22 | 2 | Inverted conical bottle loses 1 mm^3/min: rate level drops at 10 mm | AOD-RATE | — | miss | predicted only in another section (C:Q27) |
| 23 | 2 | Vector of magnitude 14 along QP for given P and Q | VEC-BASICS | Q25: triangle area by cross product | topic | same chapter as Mock 1 Q25 (VEC-CROSS), different method |
| 24 | 2 | Parallelogram with adjacent sides a, b: diagonal vectors and lengths | VEC-BASICS | — | miss | predicted only in another section (A:Q14, A:Q15) |
| 25a | 2 | Simplify tan^-1((cos2x - sin2x)/(cos2x + sin2x)), 0<x<pi/4 | ITF-SIMPLIFY | Q21b: domain of sin⁻¹(2x−3) | topic | same chapter as Mock 1 Q21b (ITF-DOMAIN-RANGE), different method |
| 25b | 2 | Evaluate tan(sin^-1 1 - cos^-1(-1/2)) | ITF-VALUE | Q21a: tan⁻¹√3 − sec⁻¹(−2) | type | same method as Mock 1 Q21a |
| 26 | 3 | Evaluate int_0^1 x tan^-1 x dx | INT-PARTS | — | miss | predicted only in another section (B:Q23a) |
| 27a | 3 | Find int sqrt((x+2)/(x-2)) dx | INT-SPECIAL | — | miss | not in Mock 1; in Mock 2 (C:Q27a) |
| 27b | 3 | Find int x^2/((x^2+9)(x^2+16)) dx | INT-PF | — | miss | predicted only in another section (D:Q33b) |
| 28 | 3 | Show I1 - 4 I2 = 0 for int dx/(1+cos2x) and int |x| dx | INT-DEF-PROP ? | — | miss | predicted only in another section (A:Q11, D:Q33a) |
| 29a | 3 | General solution of x^2 dy/dx = x^2 + xy + y^2 | DE-HOMOG | — | miss | predicted only in another section (D:Q34b) |
| 29b | 3 | Particular solution of xy dy/dx = (x+2)(y+2), y(1) = -1 | DE-VARSEP | — | miss | predicted only in another section (A:Q10) |
| 30 | 3 | Minimise Z = 13x - 15y graphically under two constraints | LPP-GRAPH | Q30: graphical LPP | type | same method as Mock 1 Q30 |
| 31a | 3 | Die decides bag I or bag II: total probability of red ball | PROB-BAYES | Q31: independent events | topic | same chapter as Mock 1 Q31 (PROB-INDEP), different method |
| 31b | 3 | P(at least one) = a, P(exactly one) = b: prove P(X')+P(Y') = 2-2a+b | PROB-COND | — | miss | predicted only in another section (A:Q18) |
| 32a | 5 | R on Z with |x-y| divisible by prime p: equivalence relation? | REL-EQUIV | — | miss | not in Mock 1; in Mock 2 (D:Q35a) |
| 32b | 5 | f(x) = (3x+2)/(5x-3) on R-{3/5}: show one-one and onto | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 33a | 5 | Find A^-1 of a 3x3 matrix and solve a related linear system | MAT-INV-SOLVE | Q32: AB = 6I, solve system | topic | same chapter as Mock 1 Q32 (MAT-PRODUCT-SOLVE), different method |
| 33b | 5 | 3x3 matrix with sin3x and cos2x singular: x in [0, pi/2] | DET-EVAL | — | miss | predicted only in another section (A:Q6) |
| 34 | 5 | x = cos t, y = cos mt: prove (1-x^2)y''-xy'+m^2y = 0 | CD-SECOND-ORDER ? | — | miss | type not in either mock |
| 35 | 5 | Two Cartesian lines: parallel? distance if so, else point of intersection | 3D-INTERSECT | Q35: lines intersect + ⟂ line | type | same method as Mock 1 Q35 |
| 36(i) | 1 | Fee raised by Rs x, 10 leave per rupee: subscribers lost | AOD-OPTIMISE | Q37(ii): can case (ii) | type | same method as Mock 1 Q37(ii) |
| 36(ii) | 1 | Write revenue R(x) as a function of x | AOD-OPTIMISE | Q37(iii)a: can case (iii)a | type | same method as Mock 1 Q37(iii)a |
| 36(iii)a | 2 | Find x maximising revenue R(x) | AOD-OPTIMISE | Q37(i): can case (i) | type | same method as Mock 1 Q37(i) |
| 36(iii)b | 2 | Sub-intervals where R(x) is increasing and decreasing | AOD-MONOTONIC | Q37(iii)b: can case (iii)b | topic | same chapter as Mock 1 Q37(iii)b (AOD-OPTIMISE), different method |
| 37(i) | 1 | Jackpot with three prize tiers: possible amounts one ticket can win | PROB-RV | — | miss | type not in either mock |
| 37(ii)a | 2 | Probability one ticket wins at least Rs 2,00,000 | PROB-RV ? | Q38(i): Bayes case (i) | topic | same chapter as Mock 1 Q38(i) (PROB-BAYES), different method |
| 37(ii)b | 2 | Probability one ticket wins no amount | PROB-RV ? | Q38(ii): Bayes case (ii) | topic | same chapter as Mock 1 Q38(ii) (PROB-BAYES), different method |
| 37(iii) | 1 | Tickets in two jackpots: probability exactly one wins | PROB-INDEP | — | miss | predicted only in another section (C:Q31) |
| 38(i) | 1 | Draw roundabout x^2+y^2=64 and pond x^2+y^2=4 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(ii) | 1 | Express y as a function of x for both circles | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(iii)a | 2 | Area covered by roundabout using integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(iii)b | 2 | Area of circular pond using integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |

### 65/1/2 (contaminated)

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | int 3ax/(b^2 + c^2 x^2) dx = A log|...| + K: find A | INT-SUB | Q12: ∫x²e^{x³}dx | type | same method as Mock 1 Q12 |
| 2 | 1 | int_{-1}^{1} x^3/(x^2 + 2|x| + 1) dx via odd function | INT-DEF-PROP | Q11: odd-function definite integral | type | same method as Mock 1 Q11 |
| 3 | 1 | Area between y = x|x|, x-axis, x = -1 and x = 1 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 4 | 1 | Integrating factor of R dx/dy + Px = Q with P, Q, R in y | DE-LINEAR | Q10: x dy − y dx = 0 | topic | same chapter as Mock 1 Q10 (DE-VARSEP), different method |
| 5 | 1 | Order and degree of d/dx(sin y) = y^2 | DE-ORDER-DEGREE | — | miss | not in Mock 1; in Mock 2 (A:Q6) |
| 6 | 1 | p making i+2j+3k and 2i-pj+k perpendicular | VEC-DOT | Q13: scalar projection | type | same method as Mock 1 Q13 |
| 7 | 1 | m making three given position vectors collinear | VEC-BASICS | Q14: distance from x-axis | type | same method as Mock 1 Q14 |
| 8 | 1 | |a|=8, |b|=3, |a x b|=12: find |a.b| | VEC-CROSS ? | Q20: A-R cross product | type | same method as Mock 1 Q20 |
| 9 | 1 | Perpendicular length from (1,2,3) to line x/0=y/1=z/0 (y-axis) | 3D-FOOT-IMAGE ? | — | miss | not in Mock 1; in Mock 2 (D:Q34b) |
| 10 | 1 | Feasible-region figure, Z = 5x + 7y: maximum minus minimum | LPP-CORNER | Q17: max Z at corners | type | same method as Mock 1 Q17 |
| 11 | 1 | Degree of an LPP objective function | LPP-CONCEPT | Q16: point outside a half-plane | type | same method as Mock 1 Q16 |
| 12 | 1 | tan^-1 x = 3y: interval in which y lies | ITF-DOMAIN-RANGE | Q1: graph of cos⁻¹(x/2) | topic | same chapter as Mock 1 Q1 (ITF-GRAPH), different method |
| 13 | 1 | Which order cannot be that of a column matrix | MAT-TYPES | Q2: order of B when A′B, BA′ defined | type | same method as Mock 1 Q2 |
| 14 | 1 | Which transpose rules hold: (A+B)', (A-B)', (AB)', (kAB)' | MAT-SYM-SKEW ? | Q3: skew-symmetric entries | type | same method as Mock 1 Q3 |
| 15 | 1 | Relation between two given 3x3 determinants Delta1 and Delta2 | DET-EVAL | Q6: 2×2 trig determinant | type | same method as Mock 1 Q6 |
| 16 | 1 | Value of x making |cos x sin x; -cos x sin x| = 1 | DET-EVAL | Q4: |adj 2A| | topic | same chapter as Mock 1 Q4 (DET-PROPS), different method |
| 17 | 1 | A, B symmetric: which combination is skew-symmetric | MAT-SYM-SKEW | Q5: inverse of 2×2 | topic | same chapter as Mock 1 Q5 (MAT-INV-SMALL), different method |
| 18 | 1 | Absolute maximum of x^2 + 1 on [-5, 2] | AOD-EXTREMA | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 19 | 1 | A-R: lines x=py+q, z=ry+s perpendicular iff pp'+rr'=1? | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 20 | 1 | A-R: P(prime | odd) for a die; P(A|B) = P(A u B)/P(B)? | PROB-COND | Q18: dice, conditional | type | same method as Mock 1 Q18 |
| 21 | 2 | Vector of magnitude 14, direction ratios 2,3,-6: projection on i | VEC-BASICS ? | Q25: triangle area by cross product | topic | same chapter as Mock 1 Q25 (VEC-CROSS), different method |
| 22 | 2 | Parallelogram with adjacent sides a, b: diagonal vectors and lengths | VEC-BASICS | — | miss | predicted only in another section (A:Q14, A:Q15) |
| 23a | 2 | Simplify tan^-1((cos2x-sin2x)/(cos2x+sin2x)); suspect copy of 65-1-1 Q25a | ITF-SIMPLIFY | Q21b: domain of sin⁻¹(2x−3) | topic | same chapter as Mock 1 Q21b (ITF-DOMAIN-RANGE), different method |
| 23b | 2 | Evaluate tan(sin^-1 1 - cos^-1(-1/2)); suspect copy of 65-1-1 Q25b | ITF-VALUE | Q21a: tan⁻¹√3 − sec⁻¹(−2) | type | same method as Mock 1 Q21a |
| 24a | 2 | Continuity at x=3 of piecewise |x-3|/(2(x-3)) and (x-6)/6 | CD-CONT | Q22: d/dx log(sec x+tan x) | topic | same chapter as Mock 1 Q22 (CD-CHAIN), different method |
| 24b | 2 | sqrt3 (x^2+y^2) = 4xy: dy/dx at (1/2, sqrt3/2) | CD-IMPLICIT | Q24: d(e^{tan x})/d(sin x) | topic | same chapter as Mock 1 Q24 (CD-CHAIN), different method |
| 25a | 2 | Simplify cot^-1 sqrt((1+cos2x)/(1-cos2x)), x in (0, pi/2) | ITF-SIMPLIFY | — | miss | not in Mock 1; in Mock 2 (B:Q21b) |
| 25b | 2 | Evaluate sin(tan^-1(-sqrt3) - sec^-1 2) | ITF-VALUE | — | miss | Mock 1's B slot(s) of this type already used (Q21a) |
| 26 | 3 | Show I1 - 4 I2 = 0 for int dx/(1+cos2x) and int |x| dx | INT-DEF-PROP ? | — | miss | predicted only in another section (A:Q11, D:Q33a) |
| 27a | 3 | General solution of y^2 dx + (x^2 - xy + y^2) dy = 0 | DE-HOMOG | — | miss | predicted only in another section (D:Q34b) |
| 27b | 3 | Particular solution of dy/dx = y tan x, y(0) = 2 | DE-VARSEP | — | miss | predicted only in another section (A:Q10) |
| 28 | 3 | Minimise Z = 13x - 15y graphically under two constraints | LPP-GRAPH | Q30: graphical LPP | type | same method as Mock 1 Q30 |
| 29a | 3 | Die decides bag I or bag II: total probability of red ball | PROB-BAYES | Q31: independent events | topic | same chapter as Mock 1 Q31 (PROB-INDEP), different method |
| 29b | 3 | P(at least one) = a, P(exactly one) = b: prove P(X')+P(Y') = 2-2a+b | PROB-COND | — | miss | predicted only in another section (A:Q18) |
| 30 | 3 | Evaluate int_0^1 x sin^-1 x dx | INT-PARTS | — | miss | predicted only in another section (B:Q23a) |
| 31a | 3 | Find int sqrt((x+2)/(x-2)) dx | INT-SPECIAL | — | miss | not in Mock 1; in Mock 2 (C:Q27a) |
| 31b | 3 | Find int x^2/((x^2+9)(x^2+16)) dx | INT-PF | — | miss | predicted only in another section (D:Q33b) |
| 32 | 5 | x = 3sin t - sin3t, y = 3cos t - cos3t: dy/dx, prove d2y/dx2 | CD-PARAM | — | miss | predicted only in another section (C:Q26b) |
| 33 | 5 | Line AB meets line CD: show it; line through intersection and origin | 3D-INTERSECT | Q35: lines intersect + ⟂ line | type | same method as Mock 1 Q35 |
| 34a | 5 | R on Z with |x-y| divisible by prime p: equivalence relation? | REL-EQUIV | — | miss | not in Mock 1; in Mock 2 (D:Q35a) |
| 34b | 5 | f(x) = (3x+2)/(5x-3) on R-{3/5}: show one-one and onto | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 35a | 5 | Find A^-1 of a 3x3 matrix and solve a related linear system | MAT-INV-SOLVE | Q32: AB = 6I, solve system | topic | same chapter as Mock 1 Q32 (MAT-PRODUCT-SOLVE), different method |
| 35b | 5 | 3x3 matrix with sin3x and cos2x singular: x in [0, pi/2] | DET-EVAL | — | miss | predicted only in another section (A:Q6) |
| 36(i) | 1 | Jackpot with three prize tiers: possible amounts one ticket can win | PROB-RV | — | miss | type not in either mock |
| 36(ii)a | 2 | Probability one ticket wins at least Rs 2,00,000 | PROB-RV ? | Q38(i): Bayes case (i) | topic | same chapter as Mock 1 Q38(i) (PROB-BAYES), different method |
| 36(ii)b | 2 | Probability one ticket wins no amount | PROB-RV ? | Q38(ii): Bayes case (ii) | topic | same chapter as Mock 1 Q38(ii) (PROB-BAYES), different method |
| 36(iii) | 1 | Tickets in two jackpots: probability exactly one wins | PROB-INDEP | — | miss | predicted only in another section (C:Q31) |
| 37(i) | 1 | Draw roundabout x^2+y^2=64 and pond x^2+y^2=4 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(ii) | 1 | Express y as a function of x for both circles | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(iii)a | 2 | Area covered by roundabout using integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(iii)b | 2 | Area of circular pond using integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(i) | 1 | Fee raised by Rs x: subscribers lost (source tags Q38 as [5]) | AOD-OPTIMISE | Q37(ii): can case (ii) | type | same method as Mock 1 Q37(ii) |
| 38(ii) | 1 | Write revenue R(x) as a function of x | AOD-OPTIMISE | Q37(iii)a: can case (iii)a | type | same method as Mock 1 Q37(iii)a |
| 38(iii)a | 2 | Find x maximising revenue R(x) | AOD-OPTIMISE | Q37(i): can case (i) | type | same method as Mock 1 Q37(i) |
| 38(iii)b | 2 | Sub-intervals where R(x) is increasing and decreasing | AOD-MONOTONIC | Q37(iii)b: can case (iii)b | topic | same chapter as Mock 1 Q37(iii)b (AOD-OPTIMISE), different method |

### 65/2/1

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | Properties of R = {(1,1),(2,2),(1,2)} on {1,2,3} | REL-LISTED | — | miss | predicted only in another section (E:Q36(i), E:Q36(ii), E:Q36(iii)a, E:Q36(iii)b) |
| 2 | 1 | Which matrix identities always hold for square A, B | MAT-ALGEBRA | Q2: order of B when A′B, BA′ defined | topic | same chapter as Mock 1 Q2 (MAT-TYPES), different method |
| 3 | 1 | Symmetric 3x3 matrix with entries a, b, c: find 3a + b + c | MAT-SYM-SKEW | Q3: skew-symmetric entries | type | same method as Mock 1 Q3 |
| 4 | 1 | Rotation matrix A with A + A' = I: find x in [0, pi/2] | MAT-ALGEBRA ? | Q5: inverse of 2×2 | topic | same chapter as Mock 1 Q5 (MAT-INV-SMALL), different method |
| 5 | 1 | (3A)^-1 in terms of A^-1 | DET-PROPS | Q4: |adj 2A| | type | same method as Mock 1 Q4 |
| 6 | 1 | 3x3 determinant in a equals -86: sum of possible a | DET-EVAL | Q6: 2×2 trig determinant | type | same method as Mock 1 Q6 |
| 7 | 1 | e^-x + e^-y = 2: dy/dx | CD-IMPLICIT | Q7: continuity, find k | topic | same chapter as Mock 1 Q7 (CD-CONT), different method |
| 8 | 1 | Local maximum and minimum values of x + 1/x | AOD-EXTREMA | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 9 | 1 | int_0^{2a} dx/(1+4x^2) = pi/6: find a | INT-DEF-EVAL | Q11: odd-function definite integral | topic | same chapter as Mock 1 Q11 (INT-DEF-PROP), different method |
| 10 | 1 | Integral giving area between y = x^2 and y = 16 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 11 | 1 | General solution of dy/dx = sqrt y / sqrt x | DE-VARSEP | Q10: x dy − y dx = 0 | type | same method as Mock 1 Q10 |
| 12 | 1 | Integrating factor of 2x dy/dx - y = 3 | DE-LINEAR | — | miss | predicted only in another section (D:Q34a) |
| 13 | 1 | |a| = 5, -2 <= lambda <= 1: max plus min of |lambda a| | VEC-BASICS | Q14: distance from x-axis | type | same method as Mock 1 Q14 |
| 14 | 1 | Magnitude-3 vector, equal angles with x, y, perpendicular to z-axis | VEC-BASICS | Q15: section formula | type | same method as Mock 1 Q15 |
| 15 | 1 | Direction cosines of line (2x-1)/4 = (1-y)/3 = -z/6 | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 16 | 1 | Name of the function optimised in an LPP | LPP-CONCEPT | Q16: point outside a half-plane | type | same method as Mock 1 Q16 |
| 17 | 1 | Non-trivial constraints read from a feasible-region figure | LPP-CONCEPT | Q17: max Z at corners | topic | same chapter as Mock 1 Q17 (LPP-CORNER), different method |
| 18 | 1 | Expression for P(A'|B') | PROB-COND | Q18: dice, conditional | type | same method as Mock 1 Q18 |
| 19 | 1 | A-R: Lagrange identity for |a x b|^2 + (a.b)^2; reason via tan theta | VEC-CROSS | Q20: A-R cross product | type | same method as Mock 1 Q20 |
| 20 | 1 | A-R: can a line have direction cosines 1, 1, 1? | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 21a | 2 | f(x) = (x-2)/(x-3) from R-{3} to R: onto? | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 21b | 2 | f(x,y) = (2y, 3x) on Z x Z: injective? | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 22 | 2 | x = a sin^3 t, y = b cos^3 t: dy/dx at t = pi/4 | CD-PARAM | Q22: d/dx log(sec x+tan x) | topic | same chapter as Mock 1 Q22 (CD-CHAIN), different method |
| 23a | 2 | Absolute maximum of cos x + sin^2 x on [0, pi] | AOD-EXTREMA | — | miss | not in Mock 1; in Mock 2 (A:Q11, E:Q36(i), E:Q36(iii)a, E:Q36(iii)b) |
| 23b | 2 | Hemisphere volume grows uniformly: surface area varies inversely as radius | AOD-RATE | — | miss | predicted only in another section (C:Q27) |
| 24 | 2 | AB, AC sides of triangle: median AD = (AB+AC)/2 and its length | VEC-BASICS | Q25: triangle area by cross product | topic | same chapter as Mock 1 Q25 (VEC-CROSS), different method |
| 25 | 2 | Point on a vector line whose coordinates sum to 3 | 3D-LINE-EQ | — | miss | predicted only in another section (C:Q29a) |
| 26 | 3 | Find int (x+2)/sqrt(9x - x^2) dx | INT-SPECIAL | — | miss | not in Mock 1; in Mock 2 (C:Q27a) |
| 27a | 3 | Evaluate int_{pi/12}^{5pi/12} dx/(1 + sqrt(cot x)) | INT-DEF-PROP | — | miss | predicted only in another section (A:Q11, D:Q33a) |
| 27b | 3 | Evaluate int_{-pi/6}^{pi/2} (sin|x| + cos|x|) dx | INT-DEF-PROP | — | miss | predicted only in another section (A:Q11, D:Q33a) |
| 28 | 3 | F'(x) = 1/(e^x + 1) with F(0) given: find F(x) | INT-SUB ? | — | miss | predicted only in another section (A:Q12) |
| 29a | 3 | Solve x dy/dx = y - x sin^2(y/x), y(1) = pi/6 | DE-HOMOG | — | miss | predicted only in another section (D:Q34b) |
| 29b | 3 | General solution of y log y dx/dy + x = 2y (linear in x) | DE-LINEAR | — | miss | predicted only in another section (D:Q34a) |
| 30 | 3 | Maximise Z = 10500x + 9000y graphically under two constraints | LPP-GRAPH | Q30: graphical LPP | type | same method as Mock 1 Q30 |
| 31a | 3 | Sniper hit chance 3/4, two shots: P(target hit), P(at least one miss) | PROB-INDEP | Q31: independent events | type | same method as Mock 1 Q31 |
| 31b | 3 | Family line-up: P(son at an end | father in middle) | PROB-COND | — | miss | predicted only in another section (A:Q18) |
| 32a | 5 | Compute QP for given 3x3 P, Q; hence solve the linear system | MAT-PRODUCT-SOLVE | Q32: AB = 6I, solve system | type | same method as Mock 1 Q32 |
| 32b | 5 | Evaluate determinant with 1+x, 1+y, 1+z diagonal; zero implies reciprocal sum -1 | DET-EVAL | — | miss | predicted only in another section (A:Q6) |
| 33a | 5 | Intervals where cot^-1(sin x + cos x) increases or decreases on (0, pi) | AOD-MONOTONIC | — | miss | predicted only in another section (A:Q9) |
| 33b | 5 | Rectangle of perimeter 36 revolved into cylinder: dimensions for maximum volume | AOD-OPTIMISE | — | miss | predicted only in another section (E:Q37(i), E:Q37(ii), E:Q37(iii)a, E:Q37(iii)b) |
| 34 | 5 | Domain of cos^-1(x^2 - 1); solve g(x) = pi/3; non-principal range of cos^-1 | ITF-DOMAIN-RANGE | — | miss | predicted only in another section (B:Q21b) |
| 35 | 5 | Line AB meets a vector line: intersection; line perpendicular to both | 3D-INTERSECT | Q35: lines intersect + ⟂ line | type | same method as Mock 1 Q35 |
| 36(i) | 1 | 50 smokers, 30 male: probability selected person is female | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 36(ii) | 1 | Male selected: probability of no lung problems | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 36(iii)a | 2 | Has lung complications: probability person is female | PROB-BAYES | Q38(i): Bayes case (i) | type | same method as Mock 1 Q38(i) |
| 36(iii)b | 2 | No lung problems: probability person is male | PROB-BAYES | Q38(ii): Bayes case (ii) | type | same method as Mock 1 Q38(ii) |
| 37(i) | 1 | Ellipse 9x^2 + 16y^2 = 144: y as a function of x | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(ii) | 1 | Integrate the function from (i), i.e. (3/4) sqrt(16 - x^2), w.r.t. x | AOI-AREA ? | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(iii)a | 2 | Area enclosed by the ellipse excluding the track, by integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 37(iii)b | 2 | Outer track meets axes at P, Q: area of triangle POQ by integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(i) | 1 | Piecewise track function: f'(x) for 0 < x < 3 | CD-DIFF ? | — | miss | not in Mock 1; in Mock 2 (A:Q7) |
| 38(ii) | 1 | Find f'(4) from the second piece | CD-DIFF ? | — | miss | not in Mock 1; in Mock 2 (A:Q7) |
| 38(iii)a | 2 | Test continuity of the piecewise function at x = 3 | CD-CONT | — | miss | predicted only in another section (A:Q7) |
| 38(iii)b | 2 | Test differentiability of the piecewise function at x = 3 | CD-DIFF | — | miss | not in Mock 1; in Mock 2 (A:Q7) |

### 65/3/1

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | Domain of cos^-1(2x - 5) | ITF-DOMAIN-RANGE | Q1: graph of cos⁻¹(x/2) | topic | same chapter as Mock 1 Q1 (ITF-GRAPH), different method |
| 2 | 1 | Quadratic identity in A gives A^-1 = xA + yI: combine x, y | MAT-INV-SMALL | Q5: inverse of 2×2 | type | same method as Mock 1 Q5 |
| 3 | 1 | A, B skew-symmetric: nature of AB + BA | MAT-SYM-SKEW | Q3: skew-symmetric entries | type | same method as Mock 1 Q3 |
| 4 | 1 | Column matrix times A gives a 3x3 matrix: order of A | MAT-TYPES | Q2: order of B when A′B, BA′ defined | type | same method as Mock 1 Q2 |
| 5 | 1 | A^2 = A and a cubic identity in (I - A): find x | MAT-ALGEBRA | — | miss | not in Mock 1; in Mock 2 (A:Q2) |
| 6 | 1 | B(adj B) = 3I: value involving det(B^-1) | DET-PROPS | Q4: |adj 2A| | type | same method as Mock 1 Q4 |
| 7 | 1 | x^2 sin(1/x) for x != 0: k for continuity at 0 | CD-CONT | Q7: continuity, find k | type | same method as Mock 1 Q7 |
| 8 | 1 | sin^-1 x = y: dy/dx in terms of y | CD-CHAIN | Q8: f′(1) of x²tan⁻¹x | type | same method as Mock 1 Q8 |
| 9 | 1 | Rate of change of sphere volume w.r.t. diameter at radius 5 | AOD-RATE | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 10 | 1 | int dx/(2^x + 2^-x) | INT-SUB ? | Q12: ∫x²e^{x³}dx | type | same method as Mock 1 Q12 |
| 11 | 1 | int_{-1}^{1} (1 - |x|) dx rewritten via even-function property | INT-DEF-PROP | Q11: odd-function definite integral | type | same method as Mock 1 Q11 |
| 12 | 1 | Shaded part of circle x^2 + y^2 = 9 as an integral | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 13 | 1 | Which F(x,y) make dy/dx = F(x,y) homogeneous | DE-HOMOG | — | miss | predicted only in another section (D:Q34b) |
| 14 | 1 | Which relation always holds for two vectors: |a.b| <= |a||b| | VEC-DOT | Q13: scalar projection | type | same method as Mock 1 Q13 |
| 15 | 1 | (a+b).(a-b) = 198 and |a| = 10|b|: find |b| | VEC-DOT | Q15: section formula | topic | same chapter as Mock 1 Q15 (VEC-BASICS), different method |
| 16 | 1 | Cosine of acute angle between lines from direction cosines | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 17 | 1 | Parallel lines from direction ratios: find p and q | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 18 | 1 | Independent E, F with P(E), P(E u F) given: P(E|F) - P(F|E) | PROB-INDEP | Q18: dice, conditional | topic | same chapter as Mock 1 Q18 (PROB-COND), different method |
| 19 | 1 | A-R: e^x + e^-y = -2 a particular solution of dy/dx = e^(x+y)? | DE-VARSEP | Q10: x dy − y dx = 0 | type | same method as Mock 1 Q10 |
| 20 | 1 | A-R: a and -2a collinear; reason claims a.(-2a) = 0 | VEC-BASICS ? | Q14: distance from x-axis | type | same method as Mock 1 Q14 |
| 21 | 2 | x = t + 1/t, y = t - 1/t: dy/dx at t = 2 | CD-PARAM | Q22: d/dx log(sec x+tan x) | topic | same chapter as Mock 1 Q22 (CD-CHAIN), different method |
| 22 | 2 | Sub-interval of (0, pi/2) where tan x - 4x increases | AOD-MONOTONIC | — | miss | predicted only in another section (A:Q9) |
| 23a | 2 | Evaluate nested sin, cot^-1, cos, tan^-1 expression | ITF-VALUE | Q21a: tan⁻¹√3 − sec⁻¹(−2) | type | same method as Mock 1 Q21a |
| 23b | 2 | R = {(1,1),(3,3),(1,2)}: symmetric? smallest R1 making R u R1 equivalence | REL-LISTED | — | miss | predicted only in another section (E:Q36(i), E:Q36(ii), E:Q36(iii)a, E:Q36(iii)b) |
| 24 | 2 | Unit vectors with equal magnitudes of two combinations: angle between them | VEC-DOT | Q25: triangle area by cross product | topic | same chapter as Mock 1 Q25 (VEC-CROSS), different method |
| 25a | 2 | Value(s) of p making two Cartesian lines perpendicular | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 25b | 2 | Line through origin perpendicular to two vector lines | 3D-LINE-EQ | — | miss | predicted only in another section (C:Q29a) |
| 26a | 3 | Find int dx/(x^(1/2) + x^(1/3)) | INT-SUB | — | miss | predicted only in another section (A:Q12) |
| 26b | 3 | Find int tan^-1((1-x)/(1+x)) dx | INT-PARTS | — | miss | predicted only in another section (B:Q23a) |
| 27 | 3 | Evaluate int sin^2026 x/(sin^2026 x + cos^2026 x) over symmetric limits | INT-DEF-PROP | — | miss | predicted only in another section (A:Q11, D:Q33a) |
| 28a | 3 | Find int cos x/((2 + sin x)(4 + sin x)) dx | INT-PF | — | miss | predicted only in another section (D:Q33b) |
| 28b | 3 | Find int (x - 3)/(x^2 - 4x + 5) dx | INT-SPECIAL | — | miss | not in Mock 1; in Mock 2 (C:Q27a) |
| 29a | 3 | General solution of a homogeneous DE via y = vx | DE-HOMOG | — | miss | predicted only in another section (D:Q34b) |
| 29b | 3 | Particular solution (x+1) dy/dx = 2e^-y - 1, y(0) = 0 | DE-VARSEP | — | miss | predicted only in another section (A:Q10) |
| 30 | 3 | (sin x)^y = y^(cos x): find dy/dx | CD-LOG | Q26a: (cos x)^y=(sin y)^x | type | same method as Mock 1 Q26a |
| 31 | 3 | Three independent surgeries, 90% success: exactly one, at most two succeed | PROB-INDEP | Q31: independent events | type | same method as Mock 1 Q31 |
| 32 | 5 | f(x) = x/sqrt(1+x^2) on R: one-one but not onto | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 33 | 5 | NOT IN SOURCE (page missing); inferred from unit weightage: graphical LPP | LPP-GRAPH ? | — | miss | predicted only in another section (C:Q30) |
| 34a | 5 | Vouchers word problem: two-variable system solved by matrix method | MAT-INV-SOLVE | Q32: AB = 6I, solve system | topic | same chapter as Mock 1 Q32 (MAT-PRODUCT-SOLVE), different method |
| 34b | 5 | Given 2x2 P, Q, R: find S with PQ - RS = O | MAT-ALGEBRA | — | miss | not in Mock 1; in Mock 2 (A:Q2) |
| 35a | 5 | Write two Cartesian lines in vector form; do they intersect? | 3D-INTERSECT | Q35: lines intersect + ⟂ line | type | same method as Mock 1 Q35 |
| 35b | 5 | Square sides on parallel lines: area via distance; p for perpendicular sides | 3D-SD | — | miss | not in Mock 1; in Mock 2 (D:Q34a) |
| 36(i) | 1 | Poles 22 m, 16 m across 20 m road: p(x) = l1 + l2 | AOD-OPTIMISE | Q37(iii)a: can case (iii)a | type | same method as Mock 1 Q37(iii)a |
| 36(ii) | 1 | Find p'(x) | AOD-OPTIMISE ? | Q37(iii)b: can case (iii)b | type | same method as Mock 1 Q37(iii)b |
| 36(iii)a | 2 | x minimising l1^2 + l2^2 | AOD-OPTIMISE | Q37(i): can case (i) | type | same method as Mock 1 Q37(i) |
| 36(iii)b | 2 | Both poles 16 m: position minimising sum of squared ladder lengths | AOD-OPTIMISE | Q37(ii): can case (ii) | type | same method as Mock 1 Q37(ii) |
| 37(i) | 1 | 40% dropouts, 60% regular: probability a student is regular | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 37(ii) | 1 | Dropout chosen: probability of not qualifying | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 37(iii)a | 2 | Student qualified: probability not a dropout | PROB-BAYES | Q38(i): Bayes case (i) | type | same method as Mock 1 Q38(i) |
| 37(iii)b | 2 | Student did not qualify: probability regular | PROB-BAYES | Q38(ii): Bayes case (ii) | type | same method as Mock 1 Q38(ii) |
| 38(i) | 1 | Park A(0,4), B(-2,0), C(3,0): equation of boundary AB | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(ii) | 1 | Equation of boundary AC | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(iii)a | 2 | Area of region OAC by integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 38(iii)b | 2 | Area of region AOB by integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |

### 65/4/1

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | Identify the inverse-trig function shown in a graph | ITF-GRAPH | Q1: graph of cos⁻¹(x/2) | type | same method as Mock 1 Q1 |
| 2 | 1 | Construct a 2x2 matrix from a given a_ij formula | MAT-TYPES | Q2: order of B when A′B, BA′ defined | type | same method as Mock 1 Q2 |
| 3 | 1 | Principal value of a sec^-1 and cosec^-1 combination | ITF-VALUE | Q19: A-R principal value | type | same method as Mock 1 Q19 |
| 4 | 1 | Points (2,3), (0,4), (p,2) collinear: find p | DET-AREA | Q4: |adj 2A| | topic | same chapter as Mock 1 Q4 (DET-PROPS), different method |
| 5 | 1 | Derivative of e^(e^x) with respect to x | CD-CHAIN | Q8: f′(1) of x²tan⁻¹x | type | same method as Mock 1 Q8 |
| 6 | 1 | Sphere volume changes at same rate as radius: surface area | AOD-RATE | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 7 | 1 | sin x/x + cos x for x != 0: k for continuity at 0 | CD-CONT | Q7: continuity, find k | type | same method as Mock 1 Q7 |
| 8 | 1 | Points in 0 < x < 3 where [x] is not differentiable | CD-DIFF | — | miss | not in Mock 1; in Mock 2 (A:Q7) |
| 9 | 1 | int dx/sqrt(25 - 16x^2) | INT-SPECIAL | Q11: odd-function definite integral | topic | same chapter as Mock 1 Q11 (INT-DEF-PROP), different method |
| 10 | 1 | int_0^1 dx/(e^x + e^-x) = tan^-1 e - k: find k | INT-DEF-EVAL | Q12: ∫x²e^{x³}dx | topic | same chapter as Mock 1 Q12 (INT-SUB), different method |
| 11 | 1 | Area bounded by y = x, x-axis, x = 0 and x = 2 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 12 | 1 | Product of order and degree of a given differential equation | DE-ORDER-DEGREE | Q10: x dy − y dx = 0 | topic | same chapter as Mock 1 Q10 (DE-VARSEP), different method |
| 13 | 1 | Which of four differential equations is not linear | DE-LINEAR | — | miss | predicted only in another section (D:Q34a) |
| 14 | 1 | Region of a system of inequations: bounded or unbounded, which quadrant | LPP-CONCEPT | Q16: point outside a half-plane | type | same method as Mock 1 Q16 |
| 15 | 1 | Max of Z = px + qy along whole segment AB: relation of p, q | LPP-CORNER | Q17: max Z at corners | type | same method as Mock 1 Q17 |
| 16 | 1 | (3i+2j+5k) x (4i+pj+qk) = 0: find p, q | VEC-CROSS | Q20: A-R cross product | type | same method as Mock 1 Q20 |
| 17 | 1 | Area of triangle A(0,1,1), B(2,0,-1), C(1,0,3) | VEC-CROSS | Q13: scalar projection | topic | same chapter as Mock 1 Q13 (VEC-DOT), different method |
| 18 | 1 | Marble drawn with replacement three times: P(at least one red) | PROB-INDEP | Q18: dice, conditional | topic | same chapter as Mock 1 Q18 (PROB-COND), different method |
| 19 | 1 | A-R: AB need not equal BA; diagonal matrices commute | MAT-ALGEBRA | Q3: skew-symmetric entries | topic | same chapter as Mock 1 Q3 (MAT-SYM-SKEW), different method |
| 20 | 1 | A-R: f(x) = x^3 + 2 on N is one-one but not onto | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 21 | 2 | Evaluate a sum of inverse-trig principal values | ITF-VALUE | Q21a: tan⁻¹√3 − sec⁻¹(−2) | type | same method as Mock 1 Q21a |
| 22a | 2 | Show piecewise cos x/(pi/2 - x) is continuous at x = pi/2 | CD-CONT | Q22: d/dx log(sec x+tan x) | topic | same chapter as Mock 1 Q22 (CD-CHAIN), different method |
| 22b | 2 | Piecewise x - 1 and 2x - 3: differentiable at x = 2? | CD-DIFF | Q24: d(e^{tan x})/d(sin x) | topic | same chapter as Mock 1 Q24 (CD-CHAIN), different method |
| 23 | 2 | Values of x for which x^x (x > 0) is increasing | AOD-MONOTONIC | — | miss | predicted only in another section (A:Q9) |
| 24 | 2 | Position vectors of A, B, C: show an isosceles triangle | VEC-BASICS | — | miss | predicted only in another section (A:Q14, A:Q15) |
| 25a | 2 | Vector of magnitude 5 perpendicular to two rod vectors | VEC-CROSS | Q25: triangle area by cross product | type | same method as Mock 1 Q25 |
| 25b | 2 | Unit vector at pi/4, pi/3 to x, y axes: angle with z, components | VEC-BASICS | — | miss | predicted only in another section (A:Q14, A:Q15) |
| 26a | 3 | f(x) = (x-2)/(x-3) from R-{3} to R-{1}: one-one and onto? | FUN-INJ-SURJ | — | miss | not in Mock 1; in Mock 2 (D:Q35b) |
| 26b | 3 | R on Z: x - y divisible by n; equivalence relation? | REL-EQUIV | — | miss | not in Mock 1; in Mock 2 (D:Q35a) |
| 27 | 3 | Given 3x3 block-diagonal A: compute A^2 - 7A + 10I | MAT-ALGEBRA | — | miss | not in Mock 1; in Mock 2 (A:Q2) |
| 28a | 3 | xy = e^(x - y): find dy/dx | CD-LOG ? | Q26a: (cos x)^y=(sin y)^x | type | same method as Mock 1 Q26a |
| 28b | 3 | Differentiate tan^-1 of sqrt(1+x^2), sqrt(1-x^2) ratio w.r.t. cos^-1 x^2 | CD-CHAIN | Q26b: parametric d²y/dx² | topic | same chapter as Mock 1 Q26b (CD-PARAM), different method |
| 29 | 3 | Maximise Z = 200x + 120y graphically under three constraints | LPP-GRAPH | Q30: graphical LPP | type | same method as Mock 1 Q30 |
| 30a | 3 | Point on a Cartesian line at a given distance from (1,2,3) | 3D-LINE-EQ | Q29a: line ⟂ to two lines | type | same method as Mock 1 Q29a |
| 30b | 3 | Shortest distance between two lines in vector form | 3D-SD | Q29b: intersection of two lines | topic | same chapter as Mock 1 Q29b (3D-INTERSECT), different method |
| 31 | 3 | Debate or quiz picks the team: P(one girl and one boy chosen) | PROB-BAYES | Q31: independent events | topic | same chapter as Mock 1 Q31 (PROB-INDEP), different method |
| 32a | 5 | Find int x^2/((x - 1)(x^2 + 4)) dx | INT-PF | Q33b: partial fractions | type | same method as Mock 1 Q33b |
| 32b | 5 | Evaluate int_0^1 x tan^-1 x/(1 + x^2)^(3/2) dx | INT-PARTS | Q33a: ∫x sin x/(1+cos²x) | topic | same chapter as Mock 1 Q33a (INT-DEF-PROP), different method |
| 33 | 5 | Area enclosed by y = |x-6|, x-axis, between x = 4 and 8 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 34a | 5 | Solve y e^y dx = (y^3 + 2x e^y) dy, y(0) = 1 | DE-LINEAR | Q34a: linear DE | type | same method as Mock 1 Q34a |
| 34b | 5 | General solution of (x^3 - 3xy^2) dx = (y^3 - 3x^2 y) dy | DE-HOMOG | Q34b: homogeneous DE | type | same method as Mock 1 Q34b |
| 35 | 5 | Line through intersection of two Cartesian lines, parallel to a given vector | 3D-INTERSECT | Q35: lines intersect + ⟂ line | type | same method as Mock 1 Q35 |
| 36(i) | 1 | Conical cup 15 cm deep, radius 5 cm: relation between h and r | AOD-RATE | Q37(iii)a: can case (iii)a | topic | same chapter as Mock 1 Q37(iii)a (AOD-OPTIMISE), different method |
| 36(ii) | 1 | Rate juice level rises when 6 cm deep | AOD-RATE | Q37(iii)b: can case (iii)b | topic | same chapter as Mock 1 Q37(iii)b (AOD-OPTIMISE), different method |
| 36(iii)a | 2 | Rate upper surface area increases at depth 6 cm | AOD-RATE | Q37(i): can case (i) | topic | same chapter as Mock 1 Q37(i) (AOD-OPTIMISE), different method |
| 36(iii)b | 2 | Rate wetted surface area increases at depth 6 cm | AOD-RATE | Q37(ii): can case (ii) | topic | same chapter as Mock 1 Q37(ii) (AOD-OPTIMISE), different method |
| 37(i) | 1 | Box dimensions: form three equations as AX = B | MAT-INV-SOLVE | — | miss | not in Mock 1; in Mock 2 (D:Q32) |
| 37(ii) | 1 | Does A^-1 exist? Justify using |A| | DET-EVAL ? | — | miss | predicted only in another section (A:Q6) |
| 37(iii)a | 2 | Find A^-1 | MAT-INV-SOLVE | — | miss | not in Mock 1; in Mock 2 (D:Q32) |
| 37(iii)b | 2 | Find A^2 - 7I | MAT-ALGEBRA | — | miss | not in Mock 1; in Mock 2 (A:Q2) |
| 38(i) | 2 | Three cap boxes chosen with probability i/6: P(red cap) | PROB-BAYES | Q38(i): Bayes case (i) | type | same method as Mock 1 Q38(i) |
| 38(ii) | 2 | Green cap selected: probability it came from Box II | PROB-BAYES | Q38(ii): Bayes case (ii) | type | same method as Mock 1 Q38(ii) |

### 65/5/1

| Q | Marks | Real question (grader's summary) | Type (grader) | Best Mock 1 match | Hit | Reason |
|---|---|---|---|---|---|---|
| 1 | 1 | 2x2 matrix in p, q, r with A^2 = I: condition on p, q, r | MAT-ALGEBRA | Q2: order of B when A′B, BA′ defined | topic | same chapter as Mock 1 Q2 (MAT-TYPES), different method |
| 2 | 1 | A^2 = A: simplify (A - I)^3 - A | MAT-ALGEBRA | Q3: skew-symmetric entries | topic | same chapter as Mock 1 Q3 (MAT-SYM-SKEW), different method |
| 3 | 1 | Which inverse-trig principal value branch is wrongly stated | ITF-DOMAIN-RANGE | Q1: graph of cos⁻¹(x/2) | topic | same chapter as Mock 1 Q1 (ITF-GRAPH), different method |
| 4 | 1 | 2x3 matrices with A + B + C = O: find C | MAT-ALGEBRA | Q5: inverse of 2×2 | topic | same chapter as Mock 1 Q5 (MAT-INV-SMALL), different method |
| 5 | 1 | A non-singular: which statement on adj A, A^-1, |A| is false | DET-PROPS | Q4: |adj 2A| | type | same method as Mock 1 Q4 |
| 6 | 1 | (x^2 - 4x - 5)/(x + 1), k at x = -1: k for continuity | CD-CONT | Q7: continuity, find k | type | same method as Mock 1 Q7 |
| 7 | 1 | Triangle (3,1), (-2,1), (0,k) has area 5: values of k | DET-AREA | Q6: 2×2 trig determinant | topic | same chapter as Mock 1 Q6 (DET-EVAL), different method |
| 8 | 1 | Derivative of cos^-1((sin x + cos x)/sqrt2) on (-pi/4, pi/4) | CD-CHAIN | Q8: f′(1) of x²tan⁻¹x | type | same method as Mock 1 Q8 |
| 9 | 1 | Absolute minimum of (x-2)^2 + 5 on [-3, 2] | AOD-EXTREMA | Q9: decreasing interval of a cubic | topic | same chapter as Mock 1 Q9 (AOD-MONOTONIC), different method |
| 10 | 1 | int dx/sqrt(1 + cos 2x) | INT-SUB | Q12: ∫x²e^{x³}dx | type | same method as Mock 1 Q12 |
| 11 | 1 | int_{-5}^{-1} dx/x | INT-DEF-EVAL | Q11: odd-function definite integral | topic | same chapter as Mock 1 Q11 (INT-DEF-PROP), different method |
| 12 | 1 | Area bounded by y = 2x - 4, both axes and x = 1 | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 13 | 1 | Order and degree of 1 + (y''')^3 = lambda y'' | DE-ORDER-DEGREE | — | miss | not in Mock 1; in Mock 2 (A:Q6) |
| 14 | 1 | General solution of dy/dx = e^(3x - y) | DE-VARSEP | Q10: x dy − y dx = 0 | type | same method as Mock 1 Q10 |
| 15 | 1 | Five corner points given, Z = 4x + 3y: maximum | LPP-CORNER | Q17: max Z at corners | type | same method as Mock 1 Q17 |
| 16 | 1 | Position vector of (24, n) has magnitude 25: find n | VEC-BASICS | Q14: distance from x-axis | type | same method as Mock 1 Q14 |
| 17 | 1 | Red Cross strips perpendicular: lambda for 3i+2j+lambda k and 2i-4j+5k | VEC-DOT | Q13: scalar projection | type | same method as Mock 1 Q13 |
| 18 | 1 | 3P(A) = P(B) = 3/5, P(A|B) = 2/3: find P(A u B) | PROB-COND | Q18: dice, conditional | type | same method as Mock 1 Q18 |
| 19 | 1 | A-R: listed relation on {1,2,3} is an equivalence relation | REL-LISTED | — | miss | predicted only in another section (E:Q36(i), E:Q36(ii), E:Q36(iii)a, E:Q36(iii)b) |
| 20 | 1 | A-R: min of x + 2y at infinitely many points; corners (0,3), (6,0) | LPP-CORNER ? | Q16: point outside a half-plane | topic | same chapter as Mock 1 Q16 (LPP-CONCEPT), different method |
| 21 | 2 | Evaluate sin[tan^-1(tan(3pi/4))] | ITF-VALUE | Q21a: tan⁻¹√3 − sec⁻¹(−2) | type | same method as Mock 1 Q21a |
| 22a | 2 | Differentiate x^x with respect to x log x | CD-CHAIN ? | Q22: d/dx log(sec x+tan x) | type | same method as Mock 1 Q22 |
| 22b | 2 | y = P cos ux + Q sin ux: show y''+u^2y = 0 | CD-SECOND-ORDER | Q24: d(e^{tan x})/d(sin x) | topic | same chapter as Mock 1 Q24 (CD-CHAIN), different method |
| 23 | 2 | Values of x where (x-3)/(x+1) is increasing | AOD-MONOTONIC | — | miss | predicted only in another section (A:Q9) |
| 24a | 2 | Bee paths a, b, c: lambda making a + lambda b perpendicular to c | VEC-DOT | — | miss | predicted only in another section (A:Q13) |
| 24b | 2 | AB = i+2j-k, AC = 2i-3j: area of triangle ABC | VEC-CROSS | Q25: triangle area by cross product | type | same method as Mock 1 Q25 |
| 25 | 2 | Angle between two lines given in Cartesian form | 3D-DCDR | — | miss | not in Mock 1; in Mock 2 (A:Q20) |
| 26 | 3 | Balloon loses volume proportional to surface area: radius falls at constant rate | AOD-RATE | Q27: sand-cone rates | type | same method as Mock 1 Q27 |
| 27a | 3 | Find int (x - sin x)/(1 - cos x) dx | INT-PARTS | — | miss | predicted only in another section (B:Q23a) |
| 27b | 3 | Evaluate int_0^2 dx/sqrt(x^2 + 2x + 3) | INT-SPECIAL | — | miss | not in Mock 1; in Mock 2 (C:Q27a) |
| 28 | 3 | Solve (x + 2y^3) dy = y dx (linear in x) | DE-LINEAR | — | miss | predicted only in another section (D:Q34a) |
| 29 | 3 | Maximise Z = 2x/5 + 3y/10 graphically under two constraints | LPP-GRAPH | Q30: graphical LPP | type | same method as Mock 1 Q30 |
| 30a | 3 | Three toys on a line with given position vectors: find a | VEC-BASICS | — | miss | predicted only in another section (A:Q14, A:Q15) |
| 30b | 3 | Unit vectors: prove |a-b|^2 + |b-c|^2 + |c-a|^2 <= 9 | VEC-DOT | — | miss | predicted only in another section (A:Q13) |
| 31a | 3 | Die events A, B, C: P(A|C), P(C|A), P(A n B|C), P(A u B|C) | PROB-COND | — | miss | predicted only in another section (A:Q18) |
| 31b | 3 | Two cards with replacement: P(A and B); are A, B independent? | PROB-INDEP | Q31: independent events | type | same method as Mock 1 Q31 |
| 32 | 5 | Costs of apples, oranges, bananas by matrix method | MAT-INV-SOLVE | Q32: AB = 6I, solve system | topic | same chapter as Mock 1 Q32 (MAT-PRODUCT-SOLVE), different method |
| 33a | 5 | y sqrt(x^2+1) = log(sqrt(x^2+1) - x): show (x^2+1)y' + xy + 1 = 0 | CD-CHAIN ? | — | miss | predicted only in another section (A:Q8, B:Q22, B:Q24) |
| 33b | 5 | Differentiate x^(cot x) + (2x^2 - 3)/(x^2 - x + 2) | CD-LOG | — | miss | predicted only in another section (C:Q26a) |
| 34 | 5 | Sketch 100x^2 + 25y^2 = 2500 and find enclosed area by integration | AOI-AREA | — | miss | predicted only in another section (B:Q23b, C:Q28a, C:Q28b) |
| 35a | 5 | Foot of perpendicular from (0,2,3) to a line; perpendicular length | 3D-FOOT-IMAGE | Q35: lines intersect + ⟂ line | topic | same chapter as Mock 1 Q35 (3D-INTERSECT), different method |
| 35b | 5 | Find p so the shortest distance between two vector lines is 3/sqrt2 | 3D-SD | — | miss | not in Mock 1; in Mock 2 (D:Q34a) |
| 36(i) | 1 | 4 girls in A, 3 boys in B: number of relations A to B | RF-COUNT | Q36(iii)a: relation case (iii)a | topic | same chapter as Mock 1 Q36(iii)a (REL-LISTED), different method |
| 36(ii) | 1 | Listed relation from A to B: is it an injective function? | FUN-INJ-SURJ ? | Q36(iii)b: relation case (iii)b | topic | same chapter as Mock 1 Q36(iii)b (REL-LISTED), different method |
| 36(iii)a | 2 | Same-colony relation on A: equivalence relation? | REL-EQUIV | Q36(i): relation case (i) | topic | same chapter as Mock 1 Q36(i) (REL-LISTED), different method |
| 36(iii)b | 2 | Can any function from B to A be bijective? | FUN-INJ-SURJ | Q36(ii): relation case (ii) | topic | same chapter as Mock 1 Q36(ii) (REL-LISTED), different method |
| 37(i) | 1 | Vaccines A1, A2, A3: probability an A2 recipient gets infected | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 37(ii) | 1 | Total probability a random person is protected | PROB-BAYES | — | miss | Mock 1's E slot(s) of this type already used (Q38(i), Q38(ii)) |
| 37(iii)a | 2 | Person infected: probability they had vaccine A1 | PROB-BAYES | Q38(i): Bayes case (i) | type | same method as Mock 1 Q38(i) |
| 37(iii)b | 2 | Person not infected: probability they had vaccine A3 | PROB-BAYES | Q38(ii): Bayes case (ii) | type | same method as Mock 1 Q38(ii) |
| 38(i) | 2 | Open cylindrical tumbler, fixed surface area: dV/dr | AOD-OPTIMISE | Q37(i): can case (i) | type | same method as Mock 1 Q37(i) |
| 38(ii) | 2 | Maximum volume: relation between height and base radius | AOD-OPTIMISE | Q37(ii): can case (ii) | type | same method as Mock 1 Q37(ii) |

## What to change in the skill

- Don't let one sample paper decide the section layout. Use the latest SQP to confirm which types are in scope, but place types by their frequency across past papers. On the two fully out-of-sample targets so far (July 2025, March 2026) frequency-only placement beat the SQP-anchored one.
- Report 'same type anywhere in the paper' next to the strict score: it is the number a student cares about when revising (Mock 1: 66.4%), while the strict one tests the layout.
- Keep the independent grader and the contamination log: without them this run would have reported the 65/1 numbers and the hand-edited Mock 2 as if they were clean.

## Shareable line

> Retrospective test, CBSE Class 12 Maths 2026 (4 uncontaminated sets): Mock 1 matched 32.5% of the marks by question type and 51.3% by chapter; both mocks together 57.7%; Tier 1+2 topics carried 90.8% of the marks.

