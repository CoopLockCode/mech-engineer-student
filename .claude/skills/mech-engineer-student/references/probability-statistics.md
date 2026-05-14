# Probability & Statistics Reference

> Graduate-level study companion for **Probability & Data Analysis / Statistics**.
> Covers probability theory, random variables, distributions, descriptive & inferential statistics, hypothesis testing, regression, and engineering data analysis.
> Math is plain text: `Σ` = sum, `√` = square root, `μ` = mean, `σ` = standard deviation, `≈` ≈, `∫` = integral, `P(A)` = probability of A, `E[X]` = expected value.

---

## 1. Descriptive Statistics

### 1.1 Data Types
- **Categorical (qualitative):** nominal (no order — color) vs. ordinal (ordered — grade).
- **Numerical (quantitative):** discrete (counts) vs. continuous (measurements).

### 1.2 Measures of Center
| Measure | Formula | Notes |
|---|---|---|
| Mean | `x̄ = (Σ xᵢ)/n` (sample), `μ = (Σ xᵢ)/N` (population) | sensitive to outliers |
| Median | middle value of ordered data (avg of two middles if `n` even) | robust to outliers |
| Mode | most frequent value | only measure valid for nominal data |
| Trimmed mean | mean after removing a % from each tail | compromise between mean and median |

**Skewness rule of thumb:** right-skewed ⇒ mean > median; left-skewed ⇒ mean < median; symmetric ⇒ mean ≈ median.

### 1.3 Measures of Spread
| Measure | Formula |
|---|---|
| Range | `max − min` |
| Sample variance | `s² = Σ(xᵢ − x̄)² / (n − 1)` |
| Population variance | `σ² = Σ(xᵢ − μ)² / N` |
| Standard deviation | `s = √s²` (sample), `σ = √σ²` (population) |
| Interquartile range | `IQR = Q₃ − Q₁` |
| Coefficient of variation | `CV = s / x̄` (unitless relative spread) |

**Why divide by `n−1`?** Bessel's correction: using `x̄` (estimated from the same data) removes one degree of freedom; dividing by `n−1` makes `s²` an **unbiased** estimator of `σ²`.

### 1.4 Position & Shape
- **Percentiles / quartiles:** `Q₁`= 25th, `Q₂`= median, `Q₃`= 75th percentile.
- **Five-number summary:** min, Q₁, median, Q₃, max → **boxplot**.
- **Outlier rule (1.5×IQR):** below `Q₁ − 1.5·IQR` or above `Q₃ + 1.5·IQR`.
- **z-score:** `z = (x − x̄)/s` — number of SDs from the mean.
- **Empirical (68–95–99.7) rule** for roughly normal data: ≈68% within 1σ, ≈95% within 2σ, ≈99.7% within 3σ.
- **Chebyshev's inequality** (any distribution): at least `1 − 1/k²` of data lies within `k` SDs of the mean (`k > 1`).

### 1.5 Plots
Histogram, boxplot, dotplot, stem-and-leaf, scatterplot (bivariate), bar chart / pie (categorical), time series.

**Pitfall:** confusing bar charts (categorical, gaps between bars) with histograms (numerical, bars touch). Mean is the wrong center for strongly skewed data.

---

## 2. Probability Theory

### 2.1 Foundations
- **Sample space `S`:** set of all outcomes. **Event:** subset of `S`.
- **Axioms (Kolmogorov):** `0 ≤ P(A) ≤ 1`; `P(S) = 1`; for mutually exclusive events `P(A₁∪A₂∪...) = ΣP(Aᵢ)`.

### 2.2 Counting
- **Multiplication principle:** `k` stages with `n₁, n₂, ... nₖ` options → `n₁·n₂·...·nₖ` total.
- **Permutations (order matters):** `P(n,r) = n!/(n−r)!`.
- **Combinations (order doesn't):** `C(n,r) = "n choose r" = n! / [r!(n−r)!]`.

### 2.3 Probability Rules
| Rule | Formula |
|---|---|
| Complement | `P(Aᶜ) = 1 − P(A)` |
| Addition (general) | `P(A∪B) = P(A) + P(B) − P(A∩B)` |
| Addition (mutually exclusive) | `P(A∪B) = P(A) + P(B)` |
| Conditional probability | `P(A|B) = P(A∩B) / P(B)`, `P(B) > 0` |
| Multiplication (general) | `P(A∩B) = P(A|B) P(B) = P(B|A) P(A)` |
| Multiplication (independent) | `P(A∩B) = P(A) P(B)` |

**Independence:** `A, B` independent iff `P(A|B) = P(A)` iff `P(A∩B) = P(A)P(B)`.
**Pitfall:** independent ≠ mutually exclusive. Mutually exclusive events with nonzero probability are *dependent* (knowing one occurred forces the other not to).

### 2.4 Law of Total Probability & Bayes' Theorem
If `B₁,...,Bₖ` partition `S`:
```
Law of total probability:  P(A) = Σ P(A|Bᵢ) P(Bᵢ)
Bayes' theorem:            P(Bⱼ|A) = P(A|Bⱼ) P(Bⱼ) / Σ P(A|Bᵢ) P(Bᵢ)
```
**Use:** updating a prior `P(Bⱼ)` to a posterior `P(Bⱼ|A)` after observing evidence `A`. Classic application: diagnostic-test accuracy (false positives dominate when the base rate is low).

---

## 3. Random Variables

### 3.1 Definitions
A **random variable (RV)** `X` assigns a number to each outcome.
- **Discrete RV:** countable values; described by a **probability mass function (PMF)** `p(x) = P(X = x)`, with `Σ p(x) = 1`.
- **Continuous RV:** uncountable values; described by a **probability density function (PDF)** `f(x) ≥ 0`, with `∫ f(x) dx = 1`. For continuous RVs `P(X = x) = 0`; probabilities are areas: `P(a ≤ X ≤ b) = ∫ₐᵇ f(x) dx`.
- **Cumulative distribution function (CDF):** `F(x) = P(X ≤ x)`. Discrete: sum of PMF up to `x`. Continuous: `F(x) = ∫_{−∞}^x f(t) dt`, and `f(x) = F'(x)`.

### 3.2 Expected Value & Variance
| Quantity | Discrete | Continuous |
|---|---|---|
| Mean / expectation | `E[X] = Σ x·p(x)` | `E[X] = ∫ x·f(x) dx` |
| `E[g(X)]` | `Σ g(x) p(x)` | `∫ g(x) f(x) dx` |
| Variance | `Var(X) = E[(X−μ)²] = E[X²] − (E[X])²` | same |
| SD | `σ = √Var(X)` | same |

**Linearity of expectation:** `E[aX + bY + c] = a E[X] + b E[Y] + c` — always, even if `X, Y` dependent.
**Variance rules:** `Var(aX + b) = a² Var(X)`. If `X, Y` independent: `Var(X ± Y) = Var(X) + Var(Y)`.
**Covariance:** `Cov(X,Y) = E[XY] − E[X]E[Y]`; **correlation** `ρ = Cov(X,Y)/(σ_X σ_Y)`, `−1 ≤ ρ ≤ 1`.

**Pitfall:** `Var(X − Y) = Var(X) + Var(Y)` (a `+`, not a `−`) for independent RVs — variances always add.

---

## 4. Common Distributions

### 4.1 Discrete Distributions
| Distribution | PMF / setup | Mean | Variance | When to use |
|---|---|---|---|---|
| **Bernoulli(p)** | one trial, `P(1)=p, P(0)=1−p` | `p` | `p(1−p)` | single success/failure |
| **Binomial(n,p)** | `P(X=k) = C(n,k) p^k (1−p)^(n−k)` | `np` | `np(1−p)` | # successes in `n` independent fixed trials |
| **Geometric(p)** | `P(X=k) = (1−p)^(k−1) p` | `1/p` | `(1−p)/p²` | # trials until first success |
| **Negative binomial(r,p)** | trials until `r`th success | `r/p` | `r(1−p)/p²` | waiting for `r` successes |
| **Poisson(λ)** | `P(X=k) = λ^k e^(−λ) / k!` | `λ` | `λ` | # rare events in fixed interval |
| **Hypergeometric** | sampling without replacement | — | — | finite population, no replacement |

**Binomial conditions (BINS):** Binary outcomes, Independent trials, fixed Number `n`, constant Success prob `p`.
**Poisson approximation to binomial:** valid when `n` large, `p` small, `λ = np` moderate.

### 4.2 Continuous Distributions
| Distribution | PDF / setup | Mean | Variance |
|---|---|---|---|
| **Uniform(a,b)** | `f(x) = 1/(b−a)` on `[a,b]` | `(a+b)/2` | `(b−a)²/12` |
| **Normal(μ,σ²)** | `f(x) = (1/(σ√(2π))) e^(−(x−μ)²/(2σ²))` | `μ` | `σ²` |
| **Exponential(λ)** | `f(x) = λ e^(−λx)`, `x ≥ 0` | `1/λ` | `1/λ²` |
| **Standard normal Z** | `Normal(0,1)` | `0` | `1` |

**Standardizing:** `Z = (X − μ)/σ`. Then use the standard normal table / `normcdf`.
**Exponential = memoryless:** `P(X > s+t | X > s) = P(X > t)`. Models time between Poisson events.

### 4.3 Sampling Distributions (the bridge to inference)
| Distribution | Used for |
|---|---|
| **Normal / Z** | means with known σ, or large `n`; proportions |
| **Student's t** (df = n−1) | means with unknown σ (estimated by `s`); heavier tails than normal |
| **Chi-square χ²** (df) | variance inference, goodness-of-fit, tests of independence |
| **F** (df₁, df₂) | comparing two variances, ANOVA |

---

## 5. Sampling Distributions & the Central Limit Theorem

### 5.1 Sampling Distribution of the Sample Mean
For a sample of size `n` from a population with mean `μ`, SD `σ`:
- `E[x̄] = μ` (the sample mean is **unbiased**).
- `SD(x̄) = σ/√n` — the **standard error of the mean**.

### 5.2 Central Limit Theorem (CLT)
**Statement:** for sufficiently large `n`, the sampling distribution of `x̄` is approximately `Normal(μ, σ²/n)` **regardless of the population's shape**. Rule of thumb: `n ≥ 30` usually suffices; fewer if the population is already roughly normal, more if strongly skewed.

**Why it matters:** the CLT is the engine of inference — it lets us attach probabilities to `x̄` even without knowing the population distribution.

### 5.3 Sampling Distribution of a Proportion
`p̂ = X/n`. `E[p̂] = p`, `SD(p̂) = √(p(1−p)/n)`. Approximately normal when `np ≥ 10` and `n(1−p) ≥ 10`.

**Pitfall:** the *population* SD `σ` does not shrink with `n` — only the **standard error** `σ/√n` does. Don't confuse spread of data with spread of the statistic.

---

## 6. Estimation & Confidence Intervals

### 6.1 Point Estimation
A **point estimate** is a single-number guess (`x̄` for `μ`, `p̂` for `p`, `s²` for `σ²`). Desirable properties: **unbiased** (`E[estimator] = parameter`), **low variance**, **consistent** (converges as `n → ∞`).

### 6.2 Confidence Interval (CI) — General Form
```
point estimate  ±  (critical value) × (standard error)
```
A `(1−α)·100%` CI: if we repeated the sampling many times, that fraction of intervals would contain the true parameter.

| Parameter | Conditions | CI |
|---|---|---|
| Mean, σ known | normal pop. or large `n` | `x̄ ± z_{α/2} · σ/√n` |
| Mean, σ unknown | normal pop. or large `n` | `x̄ ± t_{α/2, n−1} · s/√n` |
| Proportion | `np̂ ≥ 10, n(1−p̂) ≥ 10` | `p̂ ± z_{α/2} · √(p̂(1−p̂)/n)` |
| Difference of means (indep.) | both ~normal / large | `(x̄₁−x̄₂) ± t* · √(s₁²/n₁ + s₂²/n₂)` |
| Difference of proportions | success/failure ≥ 10 each | `(p̂₁−p̂₂) ± z* · √(p̂₁(1−p̂₁)/n₁ + p̂₂(1−p̂₂)/n₂)` |

Common critical values: `z_{0.025} = 1.96` (95%), `z_{0.005} = 2.576` (99%), `z_{0.05} = 1.645` (90%).

**Margin of error** `E = critical value × SE`. **Sample size for a mean:** `n = (z_{α/2} σ / E)²`. **For a proportion:** `n = z_{α/2}² p̂(1−p̂)/E²` (use `p̂ = 0.5` for the conservative worst case).

**Interpretation pitfall:** "95% confident" describes the *procedure*, not a probability about *this* fixed interval. Once computed, the interval either contains `μ` or it doesn't. Wider CI ⇐ higher confidence, smaller `n`, or larger spread.

---

## 7. Hypothesis Testing

### 7.1 Logic & Vocabulary
- **Null hypothesis `H₀`:** the status-quo / "no effect" claim (always contains `=`).
- **Alternative hypothesis `Hₐ` (or `H₁`):** the research claim (`≠`, `<`, or `>`).
- **Test statistic:** standardized distance of the estimate from the `H₀` value.
- **p-value:** probability, *assuming `H₀` is true*, of getting a test statistic at least as extreme as observed.
- **Significance level `α`:** the threshold (commonly 0.05). Reject `H₀` if `p-value ≤ α`.
- **Decision:** `p ≤ α` → reject `H₀`; `p > α` → fail to reject `H₀` (never "accept `H₀`").

### 7.2 Error Types & Power
| | `H₀` true | `H₀` false |
|---|---|---|
| Reject `H₀` | **Type I error** (prob = `α`) | correct (prob = power = `1−β`) |
| Fail to reject | correct | **Type II error** (prob = `β`) |

**Power** = `1 − β` = probability of correctly detecting a real effect. Power increases with larger `n`, larger true effect size, larger `α`, and smaller `σ`.
**Pitfall:** `α` and `β` trade off — shrinking `α` (fewer false alarms) raises `β` (more missed effects) unless `n` increases.

### 7.3 The Five-Step Procedure
1. **State** `H₀` and `Hₐ`; choose `α`.
2. **Check conditions** (random sample, independence, normality / sample-size rules).
3. **Compute the test statistic** (and degrees of freedom if applicable).
4. **Find the p-value** (or compare to the critical value).
5. **Decide and conclude in context** — reject or fail to reject; state what it means.

### 7.4 Test Statistic Formulas
| Test | Statistic | Distribution |
|---|---|---|
| One mean, σ known | `z = (x̄ − μ₀)/(σ/√n)` | standard normal |
| One mean, σ unknown | `t = (x̄ − μ₀)/(s/√n)` | t, df = n−1 |
| One proportion | `z = (p̂ − p₀)/√(p₀(1−p₀)/n)` | standard normal |
| Two means (indep., unequal var) | `t = (x̄₁−x̄₂ − Δ₀)/√(s₁²/n₁+s₂²/n₂)` | t (Welch df) |
| Paired means | `t = (d̄ − μ_d0)/(s_d/√n)` on the differences | t, df = n−1 |
| Two proportions | `z = (p̂₁−p̂₂)/√(p̂(1−p̂)(1/n₁+1/n₂))`, `p̂` pooled | standard normal |

**Critical-value approach (equivalent to p-value):** reject `H₀` if the test statistic falls in the rejection region defined by `z_{α}` / `t_{α}` for one-tailed, or `±z_{α/2}` for two-tailed.

### 7.5 Confidence Intervals ↔ Tests
A two-sided test at level `α` rejects `H₀: parameter = θ₀` exactly when `θ₀` lies **outside** the `(1−α)` CI. The two are the same inference viewed two ways.

### 7.6 Common Misinterpretations (Pitfalls)
- The p-value is **not** `P(H₀ true)`. It is `P(data this extreme | H₀)`.
- "Fail to reject `H₀`" ≠ "`H₀` is true" — it means insufficient evidence.
- **Statistical significance ≠ practical significance.** A huge `n` makes trivial effects "significant."
- One-tailed vs. two-tailed must be chosen *before* seeing the data.
- Multiple testing inflates the family-wise Type I error rate.

---

## 8. Chi-Square Tests

| Test | Purpose | Statistic |
|---|---|---|
| **Goodness-of-fit** | does a categorical variable follow a claimed distribution? | `χ² = Σ (O−E)²/E`, df = (categories − 1) |
| **Test of independence** | are two categorical variables associated? | `χ² = Σ (O−E)²/E` over a contingency table, df = (r−1)(c−1) |
| **Test of homogeneity** | do several populations share the same category distribution? | same statistic and df form |

`O` = observed count, `E` = expected count under `H₀`. For independence, `E = (row total × column total)/grand total`.
**Condition:** all expected counts `≥ 5`. Chi-square tests are always **right-tailed**.

---

## 9. ANOVA (Analysis of Variance)

**Purpose:** test whether `k ≥ 3` population means are all equal. `H₀: μ₁ = μ₂ = ... = μₖ`; `Hₐ`: at least one differs.

**Idea:** partition total variability into **between-group** (signal) and **within-group** (noise).
```
SST = SSB + SSW
F = MSB / MSW = [SSB/(k−1)] / [SSW/(N−k)]
```
df: numerator `k−1`, denominator `N−k`. Large `F` ⇒ reject `H₀`. Always right-tailed.
**Conditions:** independent samples, approximate normality within groups, roughly equal variances.
**Post-hoc:** if `H₀` rejected, use Tukey HSD / Bonferroni to find *which* means differ.

---

## 10. Correlation & Linear Regression

### 10.1 Correlation
**Pearson correlation coefficient** `r` measures linear association strength, `−1 ≤ r ≤ 1`:
```
r = Σ[(xᵢ−x̄)(yᵢ−ȳ)] / [√Σ(xᵢ−x̄)² · √Σ(yᵢ−ȳ)²]
```
`r ≈ ±1` strong linear; `r ≈ 0` no *linear* relationship (could still be nonlinear).
**Pitfall:** correlation ≠ causation; `r` is sensitive to outliers; `r = 0` does not mean "no relationship."

### 10.2 Simple Linear Regression — Least Squares
Model: `y = β₀ + β₁x + ε`, `ε ~ Normal(0, σ²)` independent.
Fitted line `ŷ = b₀ + b₁x` minimizes `Σ(yᵢ − ŷᵢ)²` (sum of squared residuals):
```
b₁ = Σ[(xᵢ−x̄)(yᵢ−ȳ)] / Σ(xᵢ−x̄)²  = r · (s_y / s_x)
b₀ = ȳ − b₁ x̄
```
The least-squares line always passes through `(x̄, ȳ)`.

### 10.3 Assessing Fit
- **Residual** `eᵢ = yᵢ − ŷᵢ`. Residual plot should show random scatter — no pattern, no funnel shape.
- **Coefficient of determination** `R² = r²` = fraction of variance in `y` explained by the model. `R² = 1 − SSE/SST`.
- **Standard error of the estimate** `s_e = √(SSE/(n−2))` = typical residual size.

### 10.4 Inference on the Slope
Test `H₀: β₁ = 0` (no linear relationship):
```
t = b₁ / SE(b₁),   df = n − 2,   SE(b₁) = s_e / √Σ(xᵢ−x̄)²
```
CI for slope: `b₁ ± t_{α/2, n−2} · SE(b₁)`.

### 10.5 Multiple & Logistic Regression (overview)
- **Multiple regression:** `ŷ = b₀ + b₁x₁ + ... + bₖxₖ`. Use **adjusted R²** to compare models (penalizes extra predictors). Watch for **multicollinearity** (correlated predictors).
- **Logistic regression:** for a binary outcome; models `log(p/(1−p)) = β₀ + β₁x` (the log-odds).

### 10.6 Regression Pitfalls
- **Extrapolation:** predicting outside the observed `x` range is unreliable.
- **Influential points / high-leverage outliers** can swing the line.
- **Lurking variables** can create spurious associations.
- A high `R²` does not confirm causation or that the linear model is *correct* — always check residuals.

---

## 11. Engineering Data Analysis Notes

- **Measurement error:** total error = systematic (bias) + random (precision). Calibration reduces bias; averaging reduces random error (`SE = σ/√n`).
- **Propagation of uncertainty:** for `Q = f(x,y,...)` with independent errors, `σ_Q² ≈ (∂f/∂x)²σ_x² + (∂f/∂y)²σ_y² + ...`.
- **Control charts (SPC):** plot a process statistic over time with center line and ±3σ control limits; points outside or non-random patterns signal an out-of-control process.
- **Design of experiments (DOE):** factorial designs, randomization, blocking, replication — isolate factor effects efficiently.
- **Significant figures & reporting:** report estimates with uncertainty (`x̄ ± SE`), not false precision.

---

## 12. Quick-Reference Decision Guide

| Question | Tool |
|---|---|
| Summarize one numerical variable | mean/median, SD/IQR, histogram, boxplot |
| Chance of a compound event | probability rules, tree diagrams |
| Update belief after evidence | Bayes' theorem |
| # successes in fixed trials | binomial |
| # rare events per interval | Poisson |
| Continuous measurement, bell-shaped | normal (standardize with `z`) |
| Estimate a mean, σ unknown | t-interval / t-test, df = n−1 |
| Estimate a proportion | z-interval / z-test (check `np ≥ 10`) |
| Compare 2 means | two-sample t |
| Compare 3+ means | ANOVA (F-test) |
| Categorical vs. categorical | chi-square test of independence |
| Fit a categorical distribution | chi-square goodness-of-fit |
| Linear relationship between two numerical variables | correlation `r`, simple linear regression, t-test on slope |

---

## Open-source sources used

- **Diez, Çetinkaya-Rundel & Barr. _OpenIntro Statistics_, 4th ed.** Open-access textbook — https://www.openintro.org/book/os/ (CC BY-SA). Source for chapter scope and methodology: summarizing data, probability rules, distributions of random variables (normal/binomial/geometric/Poisson), foundations for inference and the CLT, inference for categorical and numerical data, ANOVA, and introduction to linear / multiple / logistic regression.
- **Shafer & Zhang. _Introductory Statistics_ (LibreTexts).** https://stats.libretexts.org/Bookshelves/Introductory_Statistics/Introductory_Statistics_(Shafer_and_Zhang) (CC BY-NC-SA). Source for descriptive statistics, discrete/continuous random variables, sampling distributions, estimation, the five-step hypothesis-testing procedure, two-sample problems, correlation/regression, and chi-square / F-tests.
- **Grinstead & Snell. _Introduction to Probability_ (AMS).** Open-access — https://math.dartmouth.edu/~prob/prob/prob.pdf (GNU FDL). Source for probability axioms, counting, conditional probability, Bayes' theorem, expectation/variance, and the formal treatment of common distributions.
- **OpenStax _Introductory Statistics_ / _Statistics_.** https://openstax.org/ — Source for confidence-interval and hypothesis-test formula tables, sample-size formulas, and the regression-inference framework.
- **LibreTexts _Statistics_ Bookshelf.** https://stats.libretexts.org/ — Source for sampling-distribution theory, chi-square tests, ANOVA partitioning, and engineering data-analysis notes.
