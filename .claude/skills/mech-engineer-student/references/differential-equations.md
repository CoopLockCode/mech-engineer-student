# Differential Equations Reference

> Graduate-level study companion for **MATH 2306 — Ordinary Differential Equations** (Kennesaw State University).
> Covers first-order ODEs, second-order linear ODEs, higher-order linear ODEs, systems of ODEs, Laplace transforms, series solutions, and mechanical/electrical applications.
> Math is written in plain text: `y'` = dy/dx, `∫` = integral, `Σ` = sum, `√` = square root, `≈` = approximately.

---

## 0. Foundational Definitions and Classification

**Differential equation (DE):** an equation relating an unknown function to its derivatives.

**Ordinary DE (ODE):** unknown function depends on **one** independent variable. (Partial DEs involve several — not the focus of this course.)

**Order:** the order of the highest derivative appearing. `y'' + 3y' + 2y = 0` is second order.

**Degree:** the power of the highest-order derivative *after* the equation is made polynomial in derivatives.

**Linear ODE (order n):** can be written
```
a_n(x) y⁽ⁿ⁾ + a_{n-1}(x) y⁽ⁿ⁻¹⁾ + ... + a_1(x) y' + a_0(x) y = g(x)
```
Key property: the unknown `y` and *all* its derivatives appear to the **first power only**, with **no products** of `y` with its derivatives and **no nonlinear functions** of `y` (no `sin y`, `y²`, `e^y`, `y·y'`).

- **Homogeneous** linear ODE: `g(x) = 0`.
- **Nonhomogeneous** linear ODE: `g(x) ≠ 0`.
- **Constant-coefficient:** all `a_i` are constants.

**Solution:** a function `φ(x)` that, when substituted, satisfies the DE on an interval `I`.
- **General solution:** family containing all solutions (has `n` arbitrary constants for an `n`th-order linear ODE).
- **Particular solution:** constants fixed by side conditions.
- **Singular solution:** a solution not obtainable from the general solution by any choice of constants.

**Initial Value Problem (IVP):** DE plus conditions all given at the *same* point `x₀`: `y(x₀)=y₀, y'(x₀)=y₁, ...`.
**Boundary Value Problem (BVP):** conditions given at *different* points (e.g., `y(0)=0, y(L)=0`).

### Theorem — Existence & Uniqueness (first-order)
If `f(x,y)` and `∂f/∂y` are continuous on a rectangle `R` containing `(x₀,y₀)`, then the IVP `y' = f(x,y), y(x₀)=y₀` has a **unique** solution on some interval about `x₀`.

### Theorem — Existence & Uniqueness (linear nth-order)
If `a_n,...,a_0, g` are continuous on `I` and `a_n(x) ≠ 0` on `I`, then for any `x₀ ∈ I` the IVP has a **unique** solution on the **whole** interval `I`.

**Pitfall:** Existence/uniqueness can fail where `f` is not smooth. `y' = y^(1/3), y(0)=0` has infinitely many solutions because `∂f/∂y` blows up at `y=0`.

---

## 1. First-Order ODEs

General form: `y' = f(x,y)` or `M(x,y) dx + N(x,y) dy = 0`.

### 1.1 Separable Equations
**Form:** `y' = g(x) h(y)`, i.e., the RHS factors into an `x`-only part and a `y`-only part.

**Procedure:**
1. Rewrite as `dy/h(y) = g(x) dx`.
2. Integrate both sides: `∫ dy/h(y) = ∫ g(x) dx + C`.
3. Solve for `y` if possible (otherwise leave implicit).
4. Apply initial condition to find `C`.

**Pitfall:** Dividing by `h(y)` can lose constant (equilibrium) solutions where `h(y)=0`. Check those separately.

### 1.2 First-Order Linear Equations
**Standard form:** `y' + P(x) y = Q(x)`.

**Integrating factor:** `μ(x) = exp(∫ P(x) dx)`.

**Procedure:**
1. Put in standard form (coefficient of `y'` must be 1).
2. Compute `μ(x) = e^(∫P dx)`.
3. Multiply through: the LHS becomes `(μ y)'`.
4. Integrate: `μ y = ∫ μ Q dx + C`.
5. Solve: `y = (1/μ)[∫ μ Q dx + C]`.

**Why it works:** `μ' = μP`, so `μy' + μPy = (μy)'` by the product rule.

**Pitfall:** Forgetting to divide first so the `y'` coefficient is 1. Forgetting `+C` *inside* before dividing by `μ`.

### 1.3 Exact Equations
**Form:** `M(x,y) dx + N(x,y) dy = 0` is **exact** if there exists `F(x,y)` with `∂F/∂x = M` and `∂F/∂y = N`.

**Test for exactness:** `∂M/∂y = ∂N/∂x` (on a simply connected region).

**Procedure:**
1. Verify `M_y = N_x`.
2. Integrate `M` w.r.t. `x`: `F = ∫ M dx + g(y)`.
3. Differentiate that `F` w.r.t. `y`, set equal to `N`, solve for `g'(y)`, integrate to get `g(y)`.
4. Solution: `F(x,y) = C`.

**Integrating factors for non-exact equations:**
- If `(M_y − N_x)/N` is a function of `x` alone, then `μ(x) = exp(∫ (M_y−N_x)/N dx)`.
- If `(N_x − M_y)/M` is a function of `y` alone, then `μ(y) = exp(∫ (N_x−M_y)/M dy)`.

### 1.4 Bernoulli Equations
**Form:** `y' + P(x) y = Q(x) y^n`, `n ≠ 0, 1`.

**Substitution:** `v = y^(1−n)`. Then `v' = (1−n) y^(−n) y'`, which converts the equation into the **linear** equation
```
v' + (1−n) P(x) v = (1−n) Q(x).
```
Solve with the integrating factor, then back-substitute `y = v^(1/(1−n))`.

### 1.5 Homogeneous (in the degree sense) Equations
**Form:** `y' = f(x,y)` where `f(tx,ty) = f(x,y)` — RHS depends only on `y/x`.
**Substitution:** `v = y/x` ⇒ `y = vx`, `y' = v + x v'`. This separates.

### 1.6 Autonomous Equations & Equilibrium Analysis
**Autonomous:** `y' = f(y)` (no explicit `x`).
- **Equilibrium (critical) points:** values where `f(y) = 0`; constant solutions.
- **Stability (phase line):** if `f` changes `+ → −` through `y*`, it is **asymptotically stable** (sink); `− → +` is **unstable** (source); same sign on both sides is **semi-stable**.

### 1.7 Applications of First-Order ODEs
| Application | Model |
|---|---|
| Exponential growth/decay | `y' = ky` ⇒ `y = y₀ e^(kt)` |
| Newton's law of cooling | `T' = k(T − T_env)` |
| Mixing / tank problems | `dA/dt = (rate in) − (rate out)`, rate out `= (flow) · A/V` |
| RC / RL circuits | `R q' + q/C = E(t)`  or  `L i' + R i = E(t)` |
| Logistic growth | `P' = rP(1 − P/K)` (separable; K = carrying capacity) |
| Free fall with drag | `m v' = mg − k v` (linear) or `mg − k v²` (separable) |

---

## 2. Second-Order Linear ODEs

General form: `y'' + p(x) y' + q(x) y = g(x)`.

### 2.1 Theory of the Homogeneous Equation
For `y'' + p y' + q y = 0`:

**Superposition principle:** if `y₁, y₂` are solutions, so is `c₁y₁ + c₂y₂`.

**Wronskian:** `W(y₁,y₂)(x) = y₁ y₂' − y₂ y₁'`.

**Theorem (fundamental set):** `y₁, y₂` form a fundamental set of solutions on `I` iff `W(y₁,y₂) ≠ 0` somewhere on `I`. Then the general homogeneous solution is `y_c = c₁y₁ + c₂y₂`.

**Abel's Theorem:** `W(x) = W(x₀) · exp(−∫ p(x) dx)`. Consequence: the Wronskian is either identically zero or never zero on `I`.

**Linear independence:** two functions are linearly independent on `I` iff their Wronskian is not identically zero (for solutions of the same linear ODE).

### 2.2 Constant-Coefficient Homogeneous: Characteristic Equation
For `a y'' + b y' + c y = 0`, try `y = e^(rx)`. Get the **characteristic (auxiliary) equation**:
```
a r² + b r + c = 0,   roots r = (−b ± √(b²−4ac)) / (2a).
```

| Discriminant `b²−4ac` | Roots | General solution |
|---|---|---|
| `> 0` | real, distinct `r₁ ≠ r₂` | `y = c₁ e^(r₁x) + c₂ e^(r₂x)` |
| `= 0` | real, repeated `r` | `y = c₁ e^(rx) + c₂ x e^(rx)` |
| `< 0` | complex `α ± βi` | `y = e^(αx)(c₁ cos βx + c₂ sin βx)` |

**Repeated-root second solution:** comes from **reduction of order** — `xe^(rx)` is genuinely independent.
**Complex-root form:** uses Euler's formula `e^(iβx) = cos βx + i sin βx` to produce real solutions.

### 2.3 Reduction of Order
If one solution `y₁` of `y'' + p y' + q y = 0` is known, a second independent solution is
```
y₂ = y₁ · ∫ [ exp(−∫ p dx) / y₁² ] dx.
```
**Use:** generating the `x e^(rx)` solution, or solving variable-coefficient equations when one solution is guessable.

### 2.4 Nonhomogeneous Equations — General Structure
General solution: `y = y_c + y_p`, where `y_c` solves the homogeneous equation and `y_p` is **any** particular solution.

#### Method A — Undetermined Coefficients (constant coefficients only)
Works when `g(x)` is a polynomial, exponential, sine/cosine, or product/sum of these.

| `g(x)` | Trial `y_p` |
|---|---|
| `Pₙ(x)` (degree-n polynomial) | `Aₙxⁿ + ... + A₁x + A₀` |
| `e^(αx)` | `A e^(αx)` |
| `cos βx` or `sin βx` | `A cos βx + B sin βx` |
| `Pₙ(x) e^(αx)` | `(Aₙxⁿ+...+A₀) e^(αx)` |
| `e^(αx) cos βx` or `e^(αx) sin βx` | `e^(αx)(A cos βx + B sin βx)` |
| `Pₙ(x) cos βx` etc. | `(Aₙxⁿ+...) cos βx + (Bₙxⁿ+...) sin βx` |

**The modification rule (critical):** if any term of the trial `y_p` already appears in `y_c`, multiply the **entire** offending block by `x` (by `x²` if a double root is involved). Always compute `y_c` *first*.

**Procedure:** (1) find `y_c`; (2) write trial `y_p`; (3) apply modification rule; (4) compute `y_p', y_p''`; (5) substitute, collect like terms; (6) match coefficients, solve the linear system; (7) `y = y_c + y_p`.

**Pitfall:** Using undetermined coefficients when `g(x) = tan x`, `sec x`, `ln x`, `1/x` — these are *not* of the allowed form. Use variation of parameters instead.

#### Method B — Variation of Parameters (any continuous g)
For `y'' + p y' + q y = g(x)` with fundamental set `{y₁,y₂}`:
```
y_p = −y₁ ∫ (y₂ g / W) dx  +  y₂ ∫ (y₁ g / W) dx,
```
where `W = W(y₁,y₂)`. Equivalently `u₁' = −y₂ g / W`, `u₂' = y₁ g / W`, then `y_p = u₁y₁ + u₂y₂`.

**Procedure:** (1) put DE in standard form (coefficient of `y''` = 1) — this is essential because `g` must be the *standard-form* RHS; (2) find `y₁,y₂` and `W`; (3) integrate the two formulas; (4) assemble `y_p`.

**Pitfall:** Forgetting to normalize so the `y''` coefficient is 1 before reading off `g`.

---

## 3. Higher-Order Linear ODEs

Everything from §2 generalizes. For `a_n y⁽ⁿ⁾ + ... + a_0 y = g(x)`:
- Characteristic polynomial of degree `n`; `n` roots (with multiplicity).
- A real root `r` of multiplicity `k` contributes `e^(rx), x e^(rx), ..., x^(k−1) e^(rx)`.
- A complex pair `α ± βi` of multiplicity `k` contributes `e^(αx) cos βx, e^(αx) sin βx, ..., x^(k−1)e^(αx)cos βx, x^(k−1)e^(αx)sin βx`.
- Undetermined coefficients and variation of parameters extend directly (general `n×n` Wronskian system for the latter).

### Cauchy–Euler (Equidimensional) Equation
**Form:** `a xⁿ y⁽ⁿ⁾ + ... + a₁ x y' + a₀ y = 0`. Try `y = x^m`. For second order `a x²y'' + b x y' + c y = 0`, the **indicial equation** is
```
a m(m−1) + b m + c = 0.
```
| Roots | Solution |
|---|---|
| real distinct `m₁,m₂` | `y = c₁ x^(m₁) + c₂ x^(m₂)` |
| repeated `m` | `y = c₁ x^m + c₂ x^m ln x` |
| complex `α ± βi` | `y = x^α [c₁ cos(β ln x) + c₂ sin(β ln x)]` |

Alternative: substitute `x = e^t` to convert to a constant-coefficient ODE in `t`.

---

## 4. Mechanical & Electrical Vibrations (Applications of 2nd-Order ODEs)

### 4.1 Mass–Spring–Damper
```
m x'' + c x' + k x = F(t)
```
`m` = mass, `c` = damping coefficient, `k` = spring constant, `F(t)` = external forcing.

**Free, undamped (c=0, F=0):** `x'' + ω₀² x = 0`, `ω₀ = √(k/m)` = natural frequency.
Solution `x = A cos(ω₀t − φ)`; amplitude `A = √(c₁²+c₂²)`, phase `φ = arctan(c₂/c₁)`.

**Free, damped:** characteristic roots `r = (−c ± √(c²−4mk))/(2m)`. Define **critical damping** `c_cr = 2√(mk)`.
| Case | Condition | Behavior |
|---|---|---|
| Overdamped | `c² > 4mk` | two real negative roots; no oscillation, slow return |
| Critically damped | `c² = 4mk` | repeated root; fastest non-oscillatory return |
| Underdamped | `c² < 4mk` | complex roots; decaying oscillation, `x = e^(−c t/2m)(c₁cos μt + c₂sin μt)`, `μ = √(4mk−c²)/(2m)` |

**Forced, undamped — resonance:** `x'' + ω₀² x = (F₀/m) cos ωt`.
- If `ω ≠ ω₀`: bounded oscillation; **beats** when `ω ≈ ω₀`.
- If `ω = ω₀`: **pure resonance**, `y_p` has a factor of `t` ⇒ amplitude grows without bound.

**Forced, damped — steady state:** transient `y_c → 0`; the **steady-state** response is the `y_p` oscillation at the driving frequency `ω`. Amplitude is maximized near `ω ≈ ω₀` (practical resonance).

### 4.2 RLC Circuits (direct analogy)
```
L q'' + R q' + (1/C) q = E(t),    i = q'.
```
| Mechanical | Electrical |
|---|---|
| mass `m` | inductance `L` |
| damping `c` | resistance `R` |
| spring `k` | inverse capacitance `1/C` |
| displacement `x` | charge `q` |
| force `F(t)` | EMF `E(t)` |

---

## 5. The Laplace Transform

### 5.1 Definition
```
L{f(t)} = F(s) = ∫₀^∞ e^(−st) f(t) dt,
```
defined for `s` large enough. `f` must be **piecewise continuous** and of **exponential order** (`|f(t)| ≤ M e^(ct)`) for the transform to exist.

### 5.2 Core Transform Table
| `f(t)` | `F(s)` |
|---|---|
| `1` | `1/s` |
| `t^n` (n = 0,1,2,...) | `n! / s^(n+1)` |
| `e^(at)` | `1/(s−a)` |
| `sin(bt)` | `b/(s²+b²)` |
| `cos(bt)` | `s/(s²+b²)` |
| `sinh(bt)` | `b/(s²−b²)` |
| `cosh(bt)` | `s/(s²−b²)` |
| `e^(at) sin(bt)` | `b/((s−a)²+b²)` |
| `e^(at) cos(bt)` | `(s−a)/((s−a)²+b²)` |
| `t sin(bt)` | `2bs/(s²+b²)²` |
| `t cos(bt)` | `(s²−b²)/(s²+b²)²` |
| `t^n e^(at)` | `n!/(s−a)^(n+1)` |
| `u_c(t)` (Heaviside step at `c`) | `e^(−cs)/s` |
| `δ(t−c)` (Dirac delta) | `e^(−cs)` |

### 5.3 Operational Properties
| Property | Statement |
|---|---|
| Linearity | `L{af + bg} = aF + bG` |
| First shift (s-shift) | `L{e^(at) f(t)} = F(s−a)` |
| Second shift (t-shift) | `L{u_c(t) f(t−c)} = e^(−cs) F(s)` |
| Transform of derivative | `L{f'} = sF(s) − f(0)` |
| | `L{f''} = s²F(s) − s f(0) − f'(0)` |
| | `L{f⁽ⁿ⁾} = sⁿF − s^(n−1)f(0) − ... − f⁽ⁿ⁻¹⁾(0)` |
| Derivative of transform | `L{t^n f(t)} = (−1)^n F⁽ⁿ⁾(s)` |
| Transform of integral | `L{∫₀ᵗ f(τ)dτ} = F(s)/s` |
| Convolution | `L{(f∗g)(t)} = F(s)G(s)`, where `(f∗g)(t) = ∫₀ᵗ f(t−τ)g(τ)dτ` |
| Periodic function (period T) | `L{f} = (1/(1−e^(−sT))) ∫₀ᵀ e^(−st)f(t)dt` |

### 5.4 Solving an IVP with Laplace Transforms
1. Take the transform of **both sides**; use the derivative property — this is where the initial conditions enter.
2. Solve **algebraically** for `Y(s)`.
3. Simplify `Y(s)` — usually **partial fractions**.
4. Take the **inverse transform** term-by-term (table + shift theorems) to get `y(t)`.

**Why it's powerful:** turns calculus (the ODE) into algebra, and handles discontinuous/impulsive forcing (`u_c`, `δ`) that undetermined coefficients cannot.

### 5.5 Step Functions & Piecewise Forcing
Heaviside `u_c(t) = 0` for `t < c`, `1` for `t ≥ c`. Rewrite piecewise `f(t)` as a combination of steps:
`f(t) = f₀(t) + [f₁(t) − f₀(t)] u_{c₁}(t) + ...`. To use the t-shift theorem, force every factor into the form `g(t − c)`.

### 5.6 Dirac Delta & Impulse Response
`δ(t−c)` models an instantaneous unit impulse: `∫ δ(t−c)g(t) dt = g(c)` (sifting property). The solution of `L{y} = δ(t−c)` (with the differential operator) is the **impulse response**; convolving it with a general forcing gives the response to any input.

### 5.7 Inverse Transform Toolkit
- **Partial fractions** for rational `F(s)`.
- **Completing the square** in a denominator → match `e^(at)sin/cos` forms.
- **Convolution theorem** when `F(s)` factors but the inverse of the product is awkward.

**Pitfalls:** forgetting that `L{f'}` injects `f(0)`; mismatching the shift `e^(−cs)` with a function not yet written as `g(t−c)`; algebra errors in partial fractions.

---

## 6. Series Solutions

For `y'' + p(x) y' + q(x) y = 0` with **variable coefficients** that have no elementary closed form.

### 6.1 Classification of Points
Write in standard form `y'' + p(x)y' + q(x)y = 0`.
- **Ordinary point** `x₀`: `p` and `q` are analytic (have convergent power series) at `x₀`.
- **Singular point:** not ordinary.
- **Regular singular point** `x₀`: `(x−x₀)p(x)` and `(x−x₀)²q(x)` are both analytic at `x₀`.
- **Irregular singular point:** singular but not regular.

### 6.2 Power Series Solution at an Ordinary Point
**Theorem:** if `x₀` is an ordinary point, there exist two linearly independent solutions of the form `y = Σ_{n=0}^∞ aₙ (x−x₀)ⁿ`, with radius of convergence at least the distance to the nearest singular point.

**Procedure:**
1. Assume `y = Σ aₙ xⁿ`; differentiate term-by-term for `y', y''`.
2. Substitute into the ODE.
3. **Re-index** all sums to the same power of `x` and same starting index.
4. Combine into one series; set each coefficient to zero.
5. Get the **recurrence relation** for `aₙ`.
6. Compute terms; identify the two independent series (typically the even/`a₀` family and odd/`a₁` family).

**Pitfall:** index shifting errors — the single most common mistake. After shifting, always check the lower limit and the first few terms by hand.

### 6.3 Method of Frobenius (at a Regular Singular Point)
Assume `y = (x−x₀)^r Σ_{n=0}^∞ aₙ (x−x₀)ⁿ`, `a₀ ≠ 0`.

Substituting gives the **indicial equation** `r(r−1) + p₀ r + q₀ = 0`, where `p₀ = lim (x−x₀)p`, `q₀ = lim (x−x₀)²q`. Let roots be `r₁ ≥ r₂`.

| Case | Second solution |
|---|---|
| `r₁ − r₂` not an integer | two independent Frobenius series, one per root |
| `r₁ = r₂` | `y₂ = y₁ ln x + x^(r₁) Σ bₙ xⁿ` |
| `r₁ − r₂` a positive integer | `y₂ = C y₁ ln x + x^(r₂) Σ bₙ xⁿ` (the constant `C` may be 0) |

**Bessel's equation** `x²y'' + x y' + (x²−ν²)y = 0` is the canonical Frobenius example (solutions `J_ν`, `Y_ν`).

---

## 7. Systems of First-Order Linear ODEs

### 7.1 Setup
A system `x' = A x + g(t)`, where `x` is a vector, `A` an `n×n` matrix. **Any** higher-order linear ODE converts to a first-order system by letting `x₁ = y, x₂ = y', ...`.

### 7.2 Homogeneous Constant-Coefficient System: Eigenvalue Method
For `x' = A x`, try `x = v e^(λt)` ⇒ `(A − λI)v = 0`. So `λ` = eigenvalue, `v` = eigenvector.

**Procedure:** (1) `det(A − λI) = 0` → eigenvalues; (2) for each `λ`, solve `(A−λI)v = 0` → eigenvector; (3) build the general solution.

| Eigenvalue case | General solution piece |
|---|---|
| Real, distinct `λ₁,λ₂,...` | `x = c₁ v₁ e^(λ₁t) + c₂ v₂ e^(λ₂t) + ...` |
| Complex pair `α ± βi`, eigenvector `a ± bi` | real solutions `e^(αt)(a cos βt − b sin βt)` and `e^(αt)(a sin βt + b cos βt)` |
| Repeated `λ`, deficient (one eigenvector) | `x = c₁ v e^(λt) + c₂ (v t + w) e^(λt)`, where `(A−λI)w = v` (generalized eigenvector) |

### 7.3 Phase Plane & Stability Classification (2×2 systems)
The origin's type is read off the eigenvalues:
| Eigenvalues | Type | Stability |
|---|---|---|
| real, same sign, distinct | node | stable if both `< 0`, unstable if both `> 0` |
| real, opposite signs | saddle | unstable (always) |
| complex, nonzero real part | spiral (focus) | stable if `Re λ < 0`, unstable if `> 0` |
| pure imaginary | center | neutrally stable (closed orbits) |
| repeated, two eigenvectors | star/proper node | stable/unstable by sign |
| repeated, deficient | improper (degenerate) node | stable/unstable by sign |

### 7.4 Nonhomogeneous Systems
- **Undetermined coefficients** — vector version, same modification idea.
- **Variation of parameters** — `x_p = X(t) ∫ X⁻¹(t) g(t) dt`, where `X(t)` is a **fundamental matrix** (columns = independent solutions).
- **Matrix exponential** `e^(At) = Σ (At)ⁿ/n!`; then `x = e^(At) x₀ + ∫₀ᵗ e^(A(t−s)) g(s) ds`. `e^(At)` is a fundamental matrix with `e^(A·0) = I`.

---

## 8. Numerical Methods for ODEs (Bridge to ME 1311)

For IVP `y' = f(x,y), y(x₀)=y₀`, step size `h`:

| Method | Update formula | Local error |
|---|---|---|
| Euler (forward) | `y_{n+1} = y_n + h f(x_n, y_n)` | `O(h²)` local, `O(h)` global |
| Improved Euler (Heun) | predictor–corrector average of slopes | `O(h³)` local, `O(h²)` global |
| RK4 | weighted average of 4 slopes (see Numerical Methods reference) | `O(h⁵)` local, `O(h⁴)` global |

**Pitfall:** Euler accumulates error fast; for stiff equations explicit methods can be unstable regardless of `h`.

---

## 9. Cross-Cutting Student Pitfalls

- **Misclassifying the equation** → choosing the wrong method. Always classify (order, linear?, constant coeff?, separable?) before solving.
- **Losing solutions when dividing.** Separable and Bernoulli methods can drop equilibrium solutions.
- **Forgetting `+C`** — and putting it in the wrong place (it must enter *before* dividing by an integrating factor).
- **Undetermined coefficients without checking `y_c` first** → missing the `×x` modification.
- **Variation of parameters without standard form** → wrong `g`.
- **Laplace: forgetting initial conditions** in the derivative rule; mishandling the `t`-shift.
- **Series solutions: index-shift bookkeeping errors.**
- **Complex eigenvalues:** forgetting to extract *real* solutions from `e^(αt)(a±bi)`.
- **Resonance:** not recognizing that `ω = ω₀` forces a `t`-factor in `y_p`.
- **Initial conditions applied too early** — apply them to the *general* solution, not midway.

---

## Open-source sources used

- **Lebl, Jiří. _Notes on Diffy Qs: Differential Equations for Engineers_.** Open-access textbook — https://www.jirka.org/diffyqs/ (CC BY-NC-SA). Source for chapter scope on first-order equations, higher-order linear ODEs, mechanical vibrations, systems of ODEs, Laplace transforms, power-series/Frobenius methods, and the Laplace transform tables in the appendix.
- **Paul's Online Math Notes — Differential Equations (Paul Dawkins, Lamar University).** https://tutorial.math.lamar.edu/Classes/DE/DE.aspx — Source for the integrating-factor procedure, the undetermined-coefficients trial-function table and modification rule, the Laplace transform table and operational properties, and the systems/eigenvalue-method structure.
- **MIT OpenCourseWare 18.03 _Differential Equations_.** https://ocw.mit.edu/courses/18-03-differential-equations-spring-2010/ — Source for existence/uniqueness framing, stability/phase-plane classification, and the mechanical/electrical vibration analogy.
- **OpenStax / LibreTexts — _Differential Equations_ and _Calculus Volume 2_ (ODE chapters).** https://openstax.org/ and https://math.libretexts.org/ — Source for separable/exact equation procedures, applications (mixing, cooling, logistic, circuits), and Cauchy–Euler equations.
