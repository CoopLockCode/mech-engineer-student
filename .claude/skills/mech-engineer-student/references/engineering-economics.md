# Engineering Economics Reference

Time value of money, alternative comparison, depreciation, after-tax analysis, and risk-adjusted decisions.

---

## 0. Notation and Sign Conventions

Symbols used throughout:

- `P` — present worth (single cash flow at time 0)
- `F` — future worth (single cash flow at time n)
- `A` — uniform end-of-period cash flow over n periods (annuity)
- `G` — arithmetic gradient amount (constant period-to-period increase)
- `g` — geometric gradient rate (constant fractional period-to-period change)
- `i` — effective interest rate per compounding period
- `r` — nominal annual interest rate (NOT effective unless m = 1)
- `m` — compounding periods per year
- `n` — number of compounding periods in the analysis horizon
- `f` — inflation rate per period
- `t` — effective income tax rate (combined federal + state, net of deductions)
- `MARR` — minimum attractive rate of return (hurdle rate)

Cash flow sign convention: outflows (costs, investments) negative; inflows (revenue, savings, salvage) positive. End-of-period (EOP) convention assumed unless stated. All cash flows are placed on a cash-flow diagram before applying any factor — drawing the diagram is the single most useful debugging tool in engineering economics.

---

## 1. Time Value of Money — Single-Payment Factors

A dollar today is not equivalent to a dollar one period from now because the dollar today can earn interest. The fundamental equivalence relation is

```
F = P * (1 + i)^n
```

This is the **single-payment compound amount factor**, written `(F/P, i, n) = (1 + i)^n`. Its reciprocal is the **single-payment present worth factor**:

```
P = F * (1 + i)^(-n)        (P/F, i, n) = (1 + i)^(-n)
```

### Reading factor notation

The notation `(X/Y, i, n)` means "find X given Y at interest rate i over n periods." Multiply the known quantity by the factor:

```
X = Y * (X/Y, i, n)
```

So `F = P * (F/P, i, n)` reads as "find F given P." The position of the slash is mnemonic, not algebraic — there is no division implied. Factors are tabulated in standard tables for discrete `i` and `n`; modern practice computes them directly from the closed-form expressions.

### Pitfalls

- **Compounding period vs. cash flow period must match.** If interest compounds monthly and cash flows happen annually, you must convert the rate to an effective annual rate (see Section 4) or convert the cash flows to monthly equivalents. Mismatching the two is the most common student error.
- **The exponent n is the number of compounding periods, not years.** If `i = 0.5% per month` and the horizon is 3 years, `n = 36`, not 3.
- **`(1 + i)^n` grows superlinearly.** For long horizons (n > 30), small differences in i produce large differences in F. Always sanity-check by re-computing one period at a time when n is small.

### Worked-example pattern

> "What is the future value of $X invested today at i for n years, compounded annually?" — Apply `F = P * (1 + i)^n` directly. If the rate is given as nominal with non-annual compounding, first convert to the effective per-period rate matching the time units of n.

---

## 2. Uniform Series Factors

A **uniform series** is a sequence of equal end-of-period cash flows of magnitude A, lasting n periods. Four standard factors relate the series to P and to F.

### The six standard factors

| Factor | Name | Converts | Formula |
|--------|------|----------|---------|
| (F/P, i, n) | Single-payment compound amount | P → F | (1 + i)^n |
| (P/F, i, n) | Single-payment present worth | F → P | (1 + i)^(-n) |
| (F/A, i, n) | Uniform series compound amount | A → F | [(1 + i)^n − 1] / i |
| (A/F, i, n) | Sinking fund | F → A | i / [(1 + i)^n − 1] |
| (P/A, i, n) | Uniform series present worth | A → P | [(1 + i)^n − 1] / [i * (1 + i)^n] |
| (A/P, i, n) | Capital recovery | P → A | [i * (1 + i)^n] / [(1 + i)^n − 1] |

Memory anchors:
- `(F/A)` is built from `(F/P)`: a uniform series is a geometric sum, so `(F/A) = ((1+i)^n − 1) / i`.
- `(A/F)` and `(F/A)` are reciprocals; so are `(A/P)` and `(P/A)`.
- `(A/P) = (A/F) + i`. This identity is useful for sanity checks: capital recovery equals sinking fund plus interest on the original principal.

### When each applies

- **(F/A) Sinking fund accumulation forward.** Saving A every period — how much is in the account at year n? *Example: monthly retirement contributions, final balance at age 65.*
- **(A/F) Sinking fund deposit.** Need F dollars at year n — how much do I deposit each period? *Example: bond sinking fund, plant decommissioning reserve.*
- **(P/A) Present worth of an annuity.** Equipment generates A in savings per year for n years — what is it worth today? *Example: PV of a lease, NPV of a uniform cost-savings stream.*
- **(A/P) Capital recovery / loan amortization.** Borrow P today — what is the equal periodic payment to repay over n? *Example: mortgage payment, equipment lease payment, equivalent annual cost of a capital purchase.*

### Pitfalls

- **First payment timing.** Standard factors assume end-of-period cash flows. If the first A occurs at time 0 (annuity-due), shift by one period: `P_due = P_ordinary * (1 + i)`.
- **Deferred annuities.** If a series of A's starts at year k+1 (not year 1), compute `P_at_k = A * (P/A, i, n)` then discount that lump sum back to time 0 via `(P/F, i, k)`. Two factors, not one.
- **The (P/A) factor produces P at the end of period 0**, one period before the first A. This is the most common indexing mistake.

### Worked-example pattern (capital recovery)

> "A machine costs P today and lasts n years with salvage S. What is its equivalent annual cost (EAC) at MARR i?" — Use `EAC = P * (A/P, i, n) − S * (A/F, i, n)`. The salvage term is negative (a recovered inflow) and uses sinking fund because it is a single future payment converted to an annuity equivalent. A common shortcut: `EAC = (P − S) * (A/P, i, n) + S * i`, which is algebraically identical via the `(A/P) = (A/F) + i` identity.

---

## 3. Gradient Series — Arithmetic and Geometric

Real cash flows rarely stay uniform. The two standard gradient forms handle linear and exponential growth.

### Arithmetic gradient

Cash flow at end of period k is `(k − 1) * G` for k = 1 to n. So flows are 0, G, 2G, 3G, ..., (n−1)G. (The base flow A is handled separately and superposed.)

Present worth and equivalent uniform annual flow:

```
(P/G, i, n) = [(1 + i)^n − i*n − 1] / [i^2 * (1 + i)^n]
(A/G, i, n) = 1/i  −  n / [(1 + i)^n − 1]
```

A typical "base + gradient" stream `A, A+G, A+2G, ..., A+(n−1)G` is decomposed:

```
P = A * (P/A, i, n) + G * (P/G, i, n)
A_eq = A + G * (A/G, i, n)
```

### Geometric gradient

Cash flow at end of period k is `A_1 * (1 + g)^(k − 1)` for k = 1 to n. So flows grow (or shrink) by a constant fraction g each period.

Present worth, with the standard convention that A_1 occurs at end of period 1:

```
If g ≠ i:    P = A_1 * [1 − ((1 + g)/(1 + i))^n] / (i − g)
If g = i:    P = A_1 * n / (1 + i)
```

The g = i case is degenerate (the series grows at exactly the discount rate). Watch for it — both spreadsheet templates and student algebra trip over the zero denominator.

### Pitfalls

- **Gradient base year.** The arithmetic gradient `G * (P/G, i, n)` returns P at time 0, but the first nonzero gradient cash flow is at end of period 2 (period 1 has zero gradient). Forgetting this shifts results by one period.
- **Geometric gradient growth rate sign.** `g < 0` is valid (declining series). Verify the `((1+g)/(1+i))^n` term is computed with the signed value.
- **Confusing real growth with apparent growth.** If g already includes inflation and i is a real rate, double-counting will compound the error.

### Worked-example pattern

> "Operating costs are $A in year 1 and increase by $G each year for n years." — Decompose into a uniform A and a pure arithmetic gradient G. Discount each separately. Total `P = A*(P/A) + G*(P/G)`. If costs instead grow by g% each year, use the geometric form.

---

## 4. Nominal vs. Effective Interest Rates

A **nominal annual rate** r compounded m times per year is *not* the same as the effective annual rate. The effective rate per compounding period is `r/m`, and the effective annual rate is

```
i_eff = (1 + r/m)^m − 1
```

For continuous compounding (m → ∞), the effective annual rate is

```
i_eff = e^r − 1
```

### Common conversions

| Stated rate | Compounding | Effective annual rate |
|-------------|-------------|-----------------------|
| 12% nominal | Annually (m=1) | 12.000% |
| 12% nominal | Semiannually (m=2) | (1.06)^2 − 1 = 12.360% |
| 12% nominal | Quarterly (m=4) | (1.03)^4 − 1 = 12.551% |
| 12% nominal | Monthly (m=12) | (1.01)^12 − 1 = 12.683% |
| 12% nominal | Daily (m=365) | (1 + 0.12/365)^365 − 1 = 12.747% |
| 12% nominal | Continuous (m=∞) | e^0.12 − 1 = 12.750% |

Continuous compounding sets the ceiling — daily compounding lands within 0.003% of it for typical rates, which is why many financial products quote "compounded daily" as effectively continuous.

### Choosing the right rate

The interest rate used in any factor must match the period of n. If cash flows are monthly, use the **effective monthly rate**: `i_month = (1 + r/m)^(m/12) − 1` when r and m correspond to a different period, or simply `r/12` if r is nominal annual and you want monthly periodic. To convert between effective rates at different periods:

```
i_period_B = (1 + i_period_A)^(period_B / period_A) − 1
```

Example: convert effective annual 12% to effective monthly: `(1.12)^(1/12) − 1 = 0.949%` per month, NOT 1.000% per month.

### Pitfalls

- **APR vs. APY in consumer finance.** APR is the nominal rate r. APY is the effective annual rate i_eff. Lenders advertise the lower number for loans (APR) and the higher number for deposits (APY). Always check which one is stated.
- **Mortgage math.** US mortgages quote nominal annual compounded monthly. Monthly periodic rate is `r/12`, not `(1+r)^(1/12) − 1`. This is a regulatory convention, not a derivation.
- **Continuous compounding in problem statements.** "Force of interest" is the continuous-compounding rate. `e^(rn)` accumulates a single payment under continuous compounding; uniform series under continuous compounding use modified factors that most textbooks tabulate separately.

---

## 5. Inflation — Real, Apparent, and Constant-Dollar Analysis

Inflation erodes purchasing power. Engineering economics distinguishes three rates:

- `i_real` (also `i_r`) — real interest rate (purchasing-power growth)
- `f` — inflation rate
- `i_combined` (also `i_market`, `i_apparent`) — the rate observed in the market, which already includes inflation

The Fisher relation links them:

```
1 + i_combined = (1 + i_real) * (1 + f)
i_combined = i_real + f + i_real * f
```

The cross-term `i_real * f` is often dropped in approximation but is the source of most reconciliation errors when rates are large. At i_real = 4% and f = 3%, the true combined rate is 7.12%, not 7.00%.

### Two consistent analyses

You can do everything in constant dollars or everything in current dollars, but never mix them in the same cash flow stream.

| Mode | Cash flows in | Discount rate |
|------|---------------|---------------|
| Constant-dollar (real) | Today's purchasing power | `i_real` |
| Current-dollar (actual / then-current) | Actual dollars of the year they occur, including inflation | `i_combined` |

The two methods yield identical present worth when applied consistently. Constant-dollar analysis simplifies any cash flow that is fixed in real terms (e.g., labor that adjusts with inflation). Current-dollar analysis is required when a cash flow is fixed in nominal terms (e.g., a loan payment, a fixed-price contract).

### Pitfalls

- **Mixing real and nominal.** Discounting current-dollar cash flows at the real rate inflates NPV; discounting constant-dollar flows at the combined rate deflates NPV. Always tag each cash flow with its dollar basis.
- **Tax effects always use current-dollar.** Depreciation deductions are fixed in nominal dollars by tax law, so after-tax analysis is almost always done in current dollars.
- **Differential inflation.** Some line items (energy, healthcare) inflate at rates ≠ the general index f. Use line-specific rates when the difference is material.

---

## 6. Comparing Alternatives — PW, AW, FW

Three equivalent valuation methods exist; pick whichever best matches the decision frame.

| Method | Convert all cash flows to | Decision rule for one project | Decision rule for mutually exclusive |
|--------|--------------------------|-------------------------------|--------------------------------------|
| Present Worth (PW) | A lump sum at time 0 | PW > 0 → accept | Largest PW wins |
| Annual Worth (AW) / EUAC | An equivalent uniform annual flow | AW > 0 → accept | Largest AW wins (or lowest EUAC for cost-only) |
| Future Worth (FW) | A lump sum at end of horizon | FW > 0 → accept | Largest FW wins |

All three give identical accept/reject conclusions when applied to the same horizon at the same MARR. They differ in convenience: AW handles unequal lives elegantly, PW maps directly to NPV in corporate finance, FW is intuitive for accumulation problems.

### Equal-life alternatives

Compute PW (or AW, FW) of each alternative at the MARR; pick the best. Trivial.

### Unequal-life alternatives — two valid approaches

1. **Common study period.** Force all alternatives to a single horizon. Truncate the longer-lived asset (assigning salvage at the end of the study) or extend the shorter-lived asset (specifying what fills the gap). The study period is set by the decision context, not by either asset's life.
2. **Repeatability assumption (least common multiple, LCM).** Assume each asset is replaced in kind at the end of its life and use a study period equal to LCM of the lives. Equivalent to comparing the alternatives' AW values over their own native lives — which is why **AW is the workhorse method for unequal lives**: under the repeatability assumption, AW over one cycle equals AW over LCM cycles.

The repeatability assumption is strong; check whether the asset is actually replaceable in kind at the same cost (technology change, supplier availability, demand shifts).

### Incremental analysis

When ranking mutually exclusive alternatives, compute the incremental cash flow `Δ = (higher-cost alternative) − (lower-cost alternative)`. The extra investment in the higher-cost alternative is justified only if its incremental return clears MARR. This matters most for IRR and B/C comparisons (see Sections 7 and 8) — PW rankings already imply incremental acceptance, so PW does not require an explicit incremental step.

### Pitfalls

- **Sunk costs in alternative comparison.** Past purchases or already-paid costs are NOT included in the cash flows. Only future cash flows that differ between alternatives are relevant.
- **Including the do-nothing alternative.** Many decisions include a do-nothing baseline (PW = 0). Forgetting it can lead to accepting a project just because it is the best of a bad set.
- **Different MARRs.** All alternatives in a comparison must be discounted at the same MARR; otherwise the ranking is meaningless.

---

## 7. Rate of Return — IRR, ERR, MARR

The **internal rate of return (IRR)** is the discount rate that makes the present worth of a cash flow stream equal to zero:

```
0 = Σ_{k=0}^{n}  CF_k * (1 + IRR)^(-k)
```

For a conventional cash flow (one sign change, typically an initial outflow followed by inflows), IRR is unique and easily found by trial-and-error, bisection, or Newton's method. Accept the project if IRR > MARR.

### The multiple-root problem

For non-conventional cash flows (multiple sign changes — e.g., a project with major remediation costs at end of life), the IRR polynomial can have multiple real positive roots. Two tests bound the issue:

- **Descartes' rule of signs.** The number of positive real roots is at most equal to the number of sign changes in the cash flow series (and differs from it by an even number).
- **Norstrom's criterion.** If the *cumulative* cash flow series starts negative and has only one sign change, the IRR is unique.

If Norstrom's criterion fails, IRR is not a reliable decision metric. Two remedies:

- **External rate of return (ERR), also modified IRR (MIRR).** Reinvest positive cash flows at an explicit external rate (often MARR) until end of horizon; discount negative cash flows at a finance rate back to time 0; solve for the single rate that connects them. This eliminates the multiple-root issue by removing the implicit assumption that interim cash flows are reinvested at IRR.
- **Use PW or AW instead.** These are always unique. IRR is popular because percentages are intuitive, but PW is the rigorous tool.

### Reinvestment assumption

A subtle but important issue: classical IRR implicitly assumes positive cash flows are reinvested at IRR, which is often unrealistic for very-high-IRR projects. PW assumes reinvestment at MARR — a much safer assumption. When IRR substantially exceeds MARR, the ranking by IRR can disagree with the ranking by PW; **trust PW** for the accept/select decision.

### Pitfalls

- **Comparing IRRs across mutually exclusive alternatives directly.** Use incremental IRR on the cash-flow difference, not a direct IRR-vs-IRR comparison. The alternative with the larger IRR may have a smaller absolute PW.
- **Ignoring the sign-change count.** Always inspect the cash flow profile before quoting an IRR.
- **Solver convergence.** Numerical IRR solvers may return any root within the search range. For non-conventional flows, plot PW(i) across a range to find all roots before trusting one.

---

## 8. Benefit-Cost Analysis

The **benefit-cost (B/C) ratio** is the standard accept/reject criterion for public-sector projects, where decisions hinge on whether monetized social benefits exceed costs. Two formulations are common.

### Conventional B/C ratio

```
B/C = PW(benefits) / [PW(initial cost) + PW(O&M)]
                     OR
B/C = PW(benefits − disbenefits) / PW(costs)
```

Disbenefits are negative consequences to the public (e.g., a new highway increases traffic for adjacent residents). They are subtracted from benefits, not added to costs.

### Modified B/C ratio

```
B/C_modified = [PW(benefits) − PW(O&M)] / PW(initial cost)
```

Operating cost is moved to the numerator (as a reduction in benefits) so the denominator captures only capital cost. The two ratios produce identical accept/reject conclusions (both ≥ 1 simultaneously) but generally different numerical values — so always state which form you are reporting.

### Decision rule

- For one project against do-nothing: accept if B/C ≥ 1.
- For mutually exclusive alternatives: rank by increasing cost, then **use incremental B/C** on each step-up. Accept the step-up if `ΔB/ΔC ≥ 1`. This is the most error-prone step in public-project analysis — selecting the alternative with the highest absolute B/C ratio can produce a worse outcome than selecting the largest cumulative-justified alternative.

### Pitfalls

- **Classification of items.** Whether an item is a "cost" or a "disbenefit" can flip the ratio across the 1.0 threshold without changing the actual project value. The incremental form is robust to this; the absolute ratio is not.
- **Discount rate selection.** Public projects often use a social discount rate distinct from private MARR; the choice can dominate the analysis.
- **Monetization of intangibles.** Quality-of-life, environmental, and safety benefits require explicit valuation methods (statistical value of life, willingness-to-pay surveys). Always disclose the valuation basis.

---

## 9. Depreciation

Depreciation is the accounting allocation of an asset's cost (the **basis** B) over its useful life. It is not a cash flow itself — it is a tax-relevant non-cash deduction. The book value `BV_n` at end of year n is

```
BV_n = B − Σ_{k=1}^{n} D_k
```

where `D_k` is the depreciation charge in year k. At the end of useful life, BV equals the salvage value S (or zero, for tax methods that ignore salvage).

### Methods compared

| Method | Annual depreciation D_n | Book value at year n | Notes |
|--------|------------------------|----------------------|-------|
| Straight Line (SL) | (B − S) / N | B − n*(B−S)/N | Simplest; uniform; common for book accounting |
| Declining Balance (DB) | d * BV_(n−1) | B * (1 − d)^n | d = constant rate; accelerated |
| Double Declining Balance (DDB) | (2/N) * BV_(n−1) | B * (1 − 2/N)^n | DB with d = 2/N; switches to SL when SL > DB |
| Sum-of-Years-Digits (SOYD) | (B − S) * (N − n + 1) / SOY | computed by cumulative D | SOY = N(N+1)/2; accelerated, ignores switch |
| Units of Production (UoP) | (B − S) * (units_n / total units) | usage-driven | Best when wear is usage-based |
| MACRS | B * rate_n (from IRS table) | B − cumulative D | US tax law; ignores salvage; half-year (or other) convention |

### MACRS (US tax depreciation)

The Modified Accelerated Cost Recovery System is the required US tax depreciation system. Key properties:

- **Salvage is ignored.** Assets are fully depreciated to zero book value.
- **Recovery period (class life) is set by IRS tables**, NOT by the asset's actual useful life. Common classes: 3, 5, 7, 10, 15, 20, 27.5 (residential rental), 39 (nonresidential real).
- **Convention adds a half-year of life.** Under the half-year convention, only a half-year of depreciation is taken in the year of acquisition and a half-year in the year after the class life, so an N-year class actually spans N+1 tax years.
- **Rates are applied to the original basis B**, not to declining book value, even though the rate schedule is derived from a DDB-then-SL hybrid. This is the single most counterintuitive feature of MACRS.

Half-year convention rates for the common classes (year-1 depreciation as a fraction of basis):

| Class | Year 1 | Year 2 | Year 3 | ... | Last year |
|-------|--------|--------|--------|-----|-----------|
| 3-year | 33.33% | 44.45% | 14.81% | 7.41% | — |
| 5-year | 20.00% | 32.00% | 19.20% | 11.52% | 11.52% | 5.76% |
| 7-year | 14.29% | 24.49% | 17.49% | ... | 4.46% |

(Always pull current rates from the IRS publication; tables are revised periodically.)

### Pitfalls

- **Confusing book depreciation with tax depreciation.** A firm may use SL for financial reporting and MACRS for tax filings. Engineering economics decisions almost always use tax depreciation because that drives cash flow.
- **DB with salvage.** If the declining-balance method depreciates below salvage, deductions stop; this is automatic in DDB-switch-to-SL but easy to miss in pure DB.
- **Disposal year cash flow.** If the asset is sold at end of year n for price `S_sale`, the gain `S_sale − BV_n` is taxed at the ordinary rate (depreciation recapture) up to original basis. Gains above basis are capital gains. Losses are deductions. Don't forget this in after-tax analysis.

---

## 10. After-Tax Cash Flow Analysis

The general after-tax cash flow (ATCF) formula in year n is

```
ATCF_n = (Revenue_n − Expense_n − Depreciation_n) * (1 − t) + Depreciation_n
       = (Revenue_n − Expense_n) * (1 − t) + t * Depreciation_n
```

The first form makes the logic explicit: taxable income is revenue minus expense minus depreciation; cash tax = t * taxable income; the cash flow is pre-tax cash flow minus cash tax. The depreciation term reappears because it is a non-cash expense — added back to convert accounting income to cash. The second form is algebraically equivalent and highlights the **depreciation tax shield** `t * D_n`, the only place depreciation enters the cash flow.

### Year-0 and disposal-year flows

- **Year 0:** the capital purchase `−B` is the cash flow. Working capital additions are also year-0 outflows.
- **Disposal year (year N):** add `S_sale − t * (S_sale − BV_N)`. If `S_sale > BV_N`, the bracketed term is positive (depreciation recapture taxed). If `S_sale < BV_N`, the bracketed term is negative (loss reduces tax, increasing net inflow). Working capital is recovered.

### After-tax IRR and MARR

Compute IRR on the ATCF series; compare to the after-tax MARR. The relationship between pre-tax and after-tax MARR is approximately

```
MARR_after_tax ≈ MARR_pre_tax * (1 − t)
```

but this is only exact for a debt-free, depreciation-free, single-period analysis; in general the conversion is nontrivial because of the timing of tax shields. Most rigorous analyses set the MARR after tax directly and compute everything on an ATCF basis.

### Pitfalls

- **Effective tax rate vs. marginal tax rate.** Use the marginal rate (the rate on the next dollar of income) for incremental project analysis. Effective tax rate (cash tax / income) blends bracket effects and credits; it is wrong for marginal decisions.
- **Loan interest as a deductible expense.** Interest on debt financing is tax-deductible at the corporate level. This is a real cash benefit, but it interacts with capital structure decisions and is typically handled by adjusting the discount rate (after-tax cost of capital) rather than the cash flows. Mixing both is double-counting.
- **Negative taxable income.** If a project produces a loss, the firm-level taxable income matters: a stand-alone money-losing project has no tax shield unless the firm has other income to offset. Engineering economics typically assumes the firm has sufficient income; state the assumption explicitly.

---

## 11. Replacement Analysis

The replacement question: should we keep the **defender** (currently owned asset) or replace with the **challenger** (proposed new asset)? Two decision frameworks dominate, both built on equivalent uniform annual cost (EUAC).

### Economic life (minimum-EUAC life)

The **economic service life** of an asset is the life N* that minimizes EUAC over all possible lives 1 to N_max:

```
EUAC(n) = B * (A/P, i, n) − S_n * (A/F, i, n) + Σ O&M_k contributions
N* = argmin_n EUAC(n)
```

Compute EUAC for each candidate life n from 1 to N_max, retaining the salvage and O&M schedule appropriate to a life of n years (operating costs rise with age; salvage falls). The minimum point trades off the falling capital recovery cost (spread over more years) against the rising O&M cost.

For the challenger, this gives a single number: the challenger's minimum EUAC at its economic life.

For the defender, the analogous question is "how much longer should we keep this asset?" — and is best answered by the **marginal cost** approach.

### Marginal cost (one-more-year-test)

The marginal cost of keeping the defender one more year, year n, is

```
MC_n = loss in market value during year n
     + interest on the start-of-year market value
     + O&M and operating costs during year n
```

Each year the defender lives, you forgo (a) the market value it had at the start of the year and (b) the interest that value could have earned. Adding the year's O&M gives the true incremental cost of one more year of service.

Decision rule: **keep the defender as long as its marginal cost is less than the minimum EUAC of the challenger.** Stop when marginal cost crosses the challenger's EUAC line — that is the replacement signal.

### Sunk cost rule

Past expenditures on the defender — original purchase price, prior overhauls — are sunk and **must not appear in the replacement analysis**. The only defender-side number that matters is its current market value (the opportunity cost of keeping it). Conversely, any difference between market value and current book value generates a tax consequence (gain or loss on disposal) that DOES belong in the after-tax replacement cash flows.

### Pitfalls

- **Using book value instead of market value as the defender's "first cost."** This is the classic sunk-cost trap.
- **Comparing defender's remaining life to challenger's full life.** Compare on a per-year EUAC basis or use a common study period; never compare a 3-year remaining defender to a 10-year challenger on PW alone.
- **Trade-in value vs. market value.** A trade-in offer that exceeds market value is partially a price reduction on the new asset; allocate accordingly to avoid distorting both sides.

---

## 12. Breakeven and Sensitivity Analysis

**Breakeven analysis** finds the value of one input parameter at which the decision metric (PW, AW, IRR) equals a threshold (zero, MARR, or the value for a competing alternative). Two common forms:

### Breakeven volume

For a make-or-buy decision with fixed cost F, variable cost v per unit, and price p per unit, the breakeven volume is

```
Q_BE = F / (p − v)
```

with `(p − v)` the contribution margin per unit. Below Q_BE the project loses money; above, it profits. Sensitivity to v and p is direct.

### Breakeven interest rate

The interest rate at which PW(A) = PW(B) is the indifference point between two alternatives. Below it, one alternative wins; above it, the other. Plotting PW vs. i for both alternatives and locating the intersection is the visual form of this analysis and is the same procedure used to find IRR (intersection with the i-axis).

### Sensitivity analysis

Vary one input at a time (univariate sensitivity), holding others at base case, and plot the decision metric. The slope of PW with respect to each input indicates relative importance; the steepest-slope inputs are the priorities for refined estimation. The **spider plot** (multi-input on one chart) and **tornado diagram** (sorted bar chart of swings) are the standard visualization tools.

For multivariate variation, three approaches:

- **Scenarios** — best/expected/worst combinations of inputs chosen jointly.
- **Decision trees** — discrete branches with probabilities (see Section 14).
- **Monte Carlo** — distributions assigned to each input, with thousands of trials. The cumulative distribution of the output metric replaces the point estimate.

### Pitfalls

- **One-at-a-time sensitivity ignores correlations.** If commodity input price and product output price are positively correlated, varying one without the other is misleading.
- **Treating breakeven as a probability.** A breakeven of "we need to sell 100,000 units" is not a forecast; it is the threshold below which the project fails. The marketing forecast (with its own uncertainty) is a separate input.

---

## 13. Cost Estimating — Indices, Scaling, Learning Curves

### Cost indices (inflation adjustment)

Historical cost data must be brought forward to current dollars before use:

```
Cost_today = Cost_historical * (Index_today / Index_historical)
```

Common indices:

- **CEPCI** — Chemical Engineering Plant Cost Index. Published monthly in *Chemical Engineering*. The standard for chemical, petrochemical, and refining facilities.
- **ENR** — Engineering News-Record indices: Construction Cost Index (CCI) and Building Cost Index (BCI). Standard for civil and building construction.
- **Marshall & Swift** — equipment-focused; preferred for piece-level equipment estimating.
- **Nelson-Farrar** — refinery-specific.

Use the index that matches the cost being adjusted; cross-index substitution introduces material error over long time spans.

### Six-tenths rule (capacity scaling)

For similar plants or equipment at different capacities, the cost-to-capacity scaling exponent averages ~0.6 over a wide range of process industries:

```
Cost_B = Cost_A * (Capacity_B / Capacity_A)^x
```

with x typically 0.5 to 0.7 (called the **size factor exponent**). x = 0.6 is the default when no better information is available — hence "six-tenths rule." For specific equipment types, published exponents range from 0.3 (some heat exchangers) to 1.0 (linear scaling, rare). Outside roughly a 10x capacity ratio, the assumption deteriorates and a fresh estimate is preferred.

The rule embodies the **economy of scale** — doubling capacity costs less than doubling cost because surface-area-driven equipment cost grows slower than volume-driven capacity.

### Learning curves

For repetitive manufacturing, the time (or cost) to produce the n-th unit declines as cumulative experience grows:

```
T_n = T_1 * n^b
```

where `b = log(s) / log(2)` and s is the **learning rate** (e.g., s = 0.80 means each doubling of cumulative units reduces unit time to 80% of the prior level — a "20% learning curve" in confusingly common nomenclature). Equivalently `b = −log_2(1/s)`.

For batches or cumulative averages, integrate (or sum) the unit form to get total production time across a run of units. Learning curves are most valid for labor-intensive, manually assembled products; they are weaker for automated production where capital cost dominates.

### Fixed, variable, marginal cost

- **Fixed cost (FC):** independent of output (rent, insurance, salary).
- **Variable cost (VC):** scales with output (materials, hourly labor, utilities).
- **Total cost:** `TC = FC + VC(Q)`.
- **Marginal cost:** `MC = d(TC)/dQ` — the cost of one more unit.
- **Average cost:** `AC = TC / Q`. AC falls then rises as fixed cost is spread thin and then variable cost ramps; minimum AC occurs at AC = MC.

### Pitfalls

- **Currency conversion across years.** Combine index adjustment with currency conversion in a defined order (index first to match an inflation-aligned year, then currency).
- **Capacity not equal to throughput.** A plant rated at 100 t/day rarely operates at 100 t/day average; cost-to-capacity uses nameplate, but cash-flow estimates use realistic throughput.
- **Learning curve double-counting.** Learning effects may already be embedded in supplier quotes; applying a learning curve on top double-discounts.

---

## 14. Risk and Probability in Economic Analysis

### Expected value of cash flows

If a cash flow CF in year n takes value `CF_k` with probability `p_k`,

```
E[CF_n] = Σ_k p_k * CF_k
E[PW] = Σ_n E[CF_n] * (1 + i)^(-n)
```

Expected PW is the standard risk-neutral decision metric. Risk-averse decisions add a **risk premium** (raise the discount rate) or apply a **certainty equivalent** (lower the cash flow). Both methods can be justified rigorously under expected utility theory; both are sensitive to the chosen risk-adjustment parameter.

### Decision trees

A decision tree alternates **decision nodes** (square — the analyst chooses) with **chance nodes** (circle — nature chooses with stated probabilities). Solve by **backward induction**:

1. At each terminal node, compute the PW.
2. At each chance node, replace with the expected PW of its branches.
3. At each decision node, replace with the maximum PW across its branches; record the choice.
4. The root-node value is the project's expected PW under the optimal policy.

Decision trees are most useful when the project includes meaningful real options — abandon, expand, defer — whose value depends on resolving uncertainty over time. The **value of perfect information** is the difference between expected PW under perfect future knowledge and expected PW under current information; it bounds what should be paid for studies, pilots, or data acquisition.

### Monte Carlo simulation (concept)

Assign a probability distribution to each uncertain input (cost, revenue, life, salvage). For each trial:

1. Sample one value from each input distribution.
2. Compute PW (or IRR, or any metric) for that combination.
3. Repeat 10^3 to 10^5 times.

The resulting empirical distribution of PW gives the probability of acceptance (P(PW > 0)), the expected value, the standard deviation, and tail percentiles (e.g., 5th-percentile downside).

Monte Carlo is straightforward in spreadsheet add-ins or general-purpose code; the value-add is in honest input distributions (not pretending you know a distribution you do not) and recognition of input correlations. Independent sampling of correlated inputs (e.g., output price and input price both driven by the macroeconomy) underestimates dispersion in PW.

### Pitfalls

- **Reporting only the expected value.** A project with a 50% chance of $+200 and 50% chance of $−100 has expected PW $+50, but a risk-averse decision-maker may decline it. Always include dispersion.
- **Confusing risk with uncertainty.** Risk = probabilities are known. Uncertainty (Knightian) = probabilities are themselves unknown. Engineering economics typically operates in the risk regime; uncertainty regimes call for robust optimization or worst-case analysis.
- **Using historical volatility for a forward project.** Historical data on similar projects is informative but not predictive; structural changes in technology, regulation, or market conditions can render historical distributions invalid.

---

## Quick Reference — Standard Factors

```
Single payment:
  (F/P, i, n) = (1+i)^n
  (P/F, i, n) = (1+i)^(-n)

Uniform series:
  (F/A, i, n) = [(1+i)^n − 1] / i
  (A/F, i, n) = i / [(1+i)^n − 1]
  (P/A, i, n) = [(1+i)^n − 1] / [i*(1+i)^n]
  (A/P, i, n) = [i*(1+i)^n] / [(1+i)^n − 1]

Arithmetic gradient:
  (P/G, i, n) = [(1+i)^n − i*n − 1] / [i^2 * (1+i)^n]
  (A/G, i, n) = 1/i − n / [(1+i)^n − 1]

Geometric gradient (g ≠ i):
  P = A_1 * [1 − ((1+g)/(1+i))^n] / (i − g)

Nominal → effective:
  i_eff_annual = (1 + r/m)^m − 1            (discrete)
  i_eff_annual = e^r − 1                    (continuous)

Fisher (inflation):
  (1 + i_combined) = (1 + i_real)*(1 + f)

Depreciation tax shield:
  ATCF_n = (Rev − Exp)*(1 − t) + t*D_n

EUAC (capital recovery with salvage):
  EUAC = (B − S)*(A/P, i, n) + S*i

Six-tenths scaling:
  Cost_B = Cost_A * (Cap_B / Cap_A)^0.6

Learning curve:
  T_n = T_1 * n^b,  b = log(s)/log(2)
```

---

## Open-source sources used

- NCEES FE Reference Handbook (engineering economics section, single-payment and uniform-series factor formulas, gradient factor formulas, nominal/effective interest conversion) — public reference handbook distributed by NCEES at ncees.org and mirrored at university course-resource pages.
- LibreTexts and Saskatchewan OER engineering economics chapters (time value of money, gradient series, benefit-cost analysis at saskoer.ca/engecon) — open educational resources.
- University of Texas at El Paso open course notes (chapters 9–11 on benefit-cost evaluation and replacement studies, engineering.utep.edu/enge/ee).
- Blank & Tarquin "Engineering Economy" lecture-slide companions (replacement & retention decisions, multiple-root and Descartes/Norstrom rules) — publisher-provided instructor resources distributed openly.
- Oxford University Press companion website for Park's "Contemporary Engineering Economics" (after-tax cash flow tables, MACRS spreadsheets) — global.oup.com companion resources.
- IRS Publication 946 (MACRS class lives, half-year convention, recovery period tables) — public US tax authority publication.
- AIChE *Chemical Engineering Progress* CEPCI methodology articles and chemical-industry cost-estimation lecture notes (six-tenths rule, CEPCI usage, Chilton scaling) — open trade publication and academic course material.
- "Engineering Economy" first-edition chapter mirrors at University of Memphis civil engineering course pages (single-payment and series factor derivations).
