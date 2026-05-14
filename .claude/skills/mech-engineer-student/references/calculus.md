# Calculus I–III Reference

A comprehensive, graduate-level study companion covering the full single- and multivariable calculus sequence:

- **Calculus I** — limits, continuity, derivatives, applications of differentiation, introduction to integration
- **Calculus II** — integration techniques, applications of integrals, sequences & series, parametric equations & polar coordinates
- **Calculus III** — vectors & 3-D geometry, vector-valued functions, multivariable differential calculus, multiple integrals, vector calculus (Green's, Stokes', Divergence theorems)

Notation conventions used throughout: `lim` = limit, `∫` = integral, `Σ` = summation, `∂` = partial derivative, `∇` = del/gradient operator, `→` = vector or "approaches", `∞` = infinity, `⇒` = implies, `∈` = element of. Vectors are written in bold-equivalent as **v** or with the component form ⟨a, b, c⟩.

---

# PART I — CALCULUS I

## 1. Functions and Precalculus Foundations

### 1.1 Function fundamentals
A **function** f from set A (domain) to set B is a rule assigning each x ∈ A exactly one output f(x) ∈ B. The **range** is { f(x) : x ∈ A }.

- **Vertical line test**: a curve is a function iff every vertical line meets it at most once.
- **Even function**: f(−x) = f(x) (symmetric about y-axis). **Odd function**: f(−x) = −f(x) (symmetric about origin).
- **Composition**: (f ∘ g)(x) = f(g(x)); domain is { x ∈ dom(g) : g(x) ∈ dom(f) }.
- **One-to-one (injective)**: f(x₁) = f(x₂) ⇒ x₁ = x₂. Passes the **horizontal line test**. Only one-to-one functions have inverses.
- **Inverse function**: f⁻¹ satisfies f(f⁻¹(x)) = x and f⁻¹(f(x)) = x. Graph of f⁻¹ is reflection of f across y = x. Domain/range swap.

### 1.2 Catalog of elementary functions
| Class | Form | Key facts |
|---|---|---|
| Polynomial | aₙxⁿ + … + a₀ | Continuous & differentiable everywhere; end behavior set by leading term |
| Rational | p(x)/q(x) | Domain excludes zeros of q; vertical asymptotes / holes there |
| Power | xᵃ | Domain depends on a (e.g. x^(1/2) needs x ≥ 0) |
| Exponential | bˣ, b > 0 | Domain ℝ, range (0, ∞), bˣ > 0 always; eˣ special base |
| Logarithmic | log_b x | Inverse of bˣ; domain (0, ∞); ln x = log_e x |
| Trigonometric | sin, cos, tan, … | sin, cos periodic 2π; tan periodic π |
| Inverse trig | arcsin, arccos, arctan | Restricted domains to force one-to-one |

**Key exponential/log identities**: b^(x+y) = bˣbʸ; (bˣ)ʸ = b^(xy); log_b(xy) = log_b x + log_b y; log_b(x/y) = log_b x − log_b y; log_b(xⁿ) = n log_b x; change of base log_b x = ln x / ln b.

**Key trig identities** (needed constantly in Calc II): sin²x + cos²x = 1; 1 + tan²x = sec²x; 1 + cot²x = csc²x; double angle sin 2x = 2 sin x cos x, cos 2x = cos²x − sin²x = 2cos²x − 1 = 1 − 2sin²x; power-reduction sin²x = (1 − cos 2x)/2, cos²x = (1 + cos 2x)/2.

---

## 2. Limits and Continuity

### 2.1 Intuitive and formal definition
**Intuitive**: lim_{x→a} f(x) = L means f(x) can be made arbitrarily close to L by taking x sufficiently close to a (but x ≠ a).

**Formal (ε–δ) definition**: lim_{x→a} f(x) = L iff for every ε > 0 there exists δ > 0 such that 0 < |x − a| < δ ⇒ |f(x) − L| < ε.

*Proof pattern for ε–δ*: Start from the target |f(x) − L| < ε. Algebraically factor out |x − a| and bound the remaining factor (often by first restricting δ ≤ 1). Then choose δ = min(1, ε / bound). Reverse the algebra to write the formal proof.

**One-sided limits**: lim_{x→a⁻} (from the left), lim_{x→a⁺} (from the right). 
**Theorem**: lim_{x→a} f(x) = L iff lim_{x→a⁻} f(x) = lim_{x→a⁺} f(x) = L.

### 2.2 Limit Laws
If lim_{x→a} f(x) = L and lim_{x→a} g(x) = M exist, then:
- Sum/Difference: lim (f ± g) = L ± M
- Constant multiple: lim (cf) = cL
- Product: lim (fg) = LM
- Quotient: lim (f/g) = L/M, provided M ≠ 0
- Power: lim (f)ⁿ = Lⁿ; Root: lim (f)^(1/n) = L^(1/n) (L > 0 for even n)
- Polynomials & rationals: limits found by **direct substitution** wherever defined.

### 2.3 Techniques for indeterminate forms
When direct substitution gives 0/0:
1. **Factor and cancel** the common factor causing the zero.
2. **Rationalize** (multiply by conjugate) when radicals are present.
3. **Combine fractions** / simplify complex fractions.
4. **Trig limits** — use the special limits below.
5. **L'Hôpital's Rule** (after derivatives are available — see §4.7).

**Special trig limits**: 
- lim_{x→0} (sin x)/x = 1 
- lim_{x→0} (1 − cos x)/x = 0

### 2.4 Squeeze (Sandwich) Theorem
If g(x) ≤ f(x) ≤ h(x) near a (except possibly at a) and lim_{x→a} g(x) = lim_{x→a} h(x) = L, then lim_{x→a} f(x) = L. *Standard use*: bounding oscillatory functions, e.g. lim_{x→0} x² sin(1/x) = 0 via −x² ≤ x² sin(1/x) ≤ x².

### 2.5 Infinite limits and limits at infinity
- **Vertical asymptote** at x = a: lim_{x→a} f(x) = ±∞.
- **Limits at infinity** describe **horizontal asymptotes**: lim_{x→∞} f(x) = L.
- **Rational function at infinity rule**: compare degrees of numerator (n) and denominator (m). If n < m, limit = 0. If n = m, limit = ratio of leading coefficients. If n > m, limit = ±∞ (no horizontal asymptote; possibly a slant asymptote when n = m + 1).

### 2.6 Continuity
**Definition**: f is continuous at a iff (1) f(a) is defined, (2) lim_{x→a} f(x) exists, (3) lim_{x→a} f(x) = f(a).

**Types of discontinuity**: removable (hole — limit exists but ≠ f(a) or f(a) undefined), jump (one-sided limits differ), infinite (vertical asymptote).

**Continuity theorems**: sums, differences, products, quotients (denominator ≠ 0), and compositions of continuous functions are continuous. Polynomials, rational, root, exponential, log, and trig functions are continuous on their domains.

**Intermediate Value Theorem (IVT)**: If f is continuous on [a, b] and N is any value between f(a) and f(b), then there exists c ∈ (a, b) with f(c) = N. *Standard use*: proving a root exists in an interval (show f changes sign).

**Pitfalls**: forgetting x ≠ a in the limit definition; assuming a limit exists when one-sided limits disagree; using L'Hôpital on a form that is *not* indeterminate.

---

## 3. The Derivative

### 3.1 Definition
The **derivative** of f at a:
f′(a) = lim_{h→0} [f(a + h) − f(a)] / h = lim_{x→a} [f(x) − f(a)] / (x − a).

As a function: f′(x) = lim_{h→0} [f(x + h) − f(x)] / h.

**Interpretations**: (1) slope of the tangent line at (a, f(a)); (2) instantaneous rate of change; (3) velocity if f is position.

**Tangent line** at (a, f(a)): y = f(a) + f′(a)(x − a). **Normal line**: slope −1/f′(a).

**Differentiability ⇒ continuity** (converse false: |x| is continuous but not differentiable at 0). A function fails to be differentiable at corners, cusps, vertical tangents, and discontinuities.

### 3.2 Differentiation rules
| Rule | Statement |
|---|---|
| Constant | d/dx[c] = 0 |
| Power | d/dx[xⁿ] = n·xⁿ⁻¹ (all real n) |
| Constant multiple | d/dx[c·f] = c·f′ |
| Sum/Difference | d/dx[f ± g] = f′ ± g′ |
| Product | d/dx[fg] = f′g + fg′ |
| Quotient | d/dx[f/g] = (f′g − fg′)/g² |
| Chain | d/dx[f(g(x))] = f′(g(x))·g′(x) |

### 3.3 Derivatives of elementary functions
| f(x) | f′(x) |
|---|---|
| sin x | cos x |
| cos x | −sin x |
| tan x | sec²x |
| cot x | −csc²x |
| sec x | sec x tan x |
| csc x | −csc x cot x |
| eˣ | eˣ |
| bˣ | bˣ ln b |
| ln x | 1/x |
| log_b x | 1/(x ln b) |
| arcsin x | 1/√(1 − x²) |
| arccos x | −1/√(1 − x²) |
| arctan x | 1/(1 + x²) |
| arcsec x | 1/(|x|√(x² − 1)) |

### 3.4 Chain rule — the workhorse
For composite y = f(u), u = g(x): dy/dx = (dy/du)(du/dx). Extends to arbitrary depth. *Procedure*: identify outer and inner functions, differentiate outer (leaving inner intact), multiply by derivative of inner, repeat.

### 3.5 Implicit differentiation
When y is defined implicitly by an equation F(x, y) = 0:
1. Differentiate both sides with respect to x, treating y as a function of x.
2. Every term with y picks up a factor dy/dx via the chain rule.
3. Collect dy/dx terms on one side, factor, and solve for dy/dx.

*Use*: curves not solvable for y (circles, folium of Descartes), and deriving inverse-function derivatives.

### 3.6 Logarithmic differentiation
For products/quotients/powers of many factors, or variable-base-variable-exponent forms y = f(x)^g(x):
1. Take ln of both sides.
2. Use log laws to expand into sums.
3. Differentiate implicitly: (1/y)·y′ = (expanded derivative).
4. Multiply by y and substitute back.

### 3.7 Higher-order derivatives
f″ = (f′)′, f‴, …, f⁽ⁿ⁾. Second derivative gives **acceleration** (if f is position) and **concavity**.

### 3.8 Related rates
*Algorithm*:
1. Draw a diagram; label quantities that change as functions of time t.
2. Write an equation relating the variables (geometry: Pythagorean, similar triangles, area/volume formulas).
3. Differentiate both sides with respect to t (chain rule — every variable gets a d/dt).
4. Substitute known instantaneous values **last** (never before differentiating).
5. Solve for the unknown rate; include units.

**Pitfalls**: substituting numerical values before differentiating; mismatched units; forgetting that a "constant" in the snapshot (e.g. a fixed ladder length) is genuinely constant and differentiates to 0.

---

## 4. Applications of Differentiation

### 4.1 Extrema and critical points
- **Absolute (global) max/min** on a set; **local (relative) max/min**.
- **Critical point**: interior point c where f′(c) = 0 or f′(c) does not exist.
- **Fermat's Theorem**: if f has a local extremum at c and f′(c) exists, then f′(c) = 0.
- **Extreme Value Theorem (EVT)**: a continuous function on a closed bounded interval [a, b] attains both an absolute max and an absolute min.

**Closed-interval method**: evaluate f at all critical points in (a, b) and at the endpoints a, b; the largest/smallest values are the absolute extrema.

### 4.2 Mean Value Theorem (MVT) and Rolle's Theorem
**Rolle's Theorem**: if f is continuous on [a, b], differentiable on (a, b), and f(a) = f(b), then there exists c ∈ (a, b) with f′(c) = 0.

**Mean Value Theorem**: if f is continuous on [a, b] and differentiable on (a, b), then there exists c ∈ (a, b) with f′(c) = [f(b) − f(a)] / (b − a) — i.e. some instantaneous rate equals the average rate.

**Consequences**: if f′ = 0 on an interval, f is constant; if f′ = g′, then f and g differ by a constant (foundation of antiderivatives).

### 4.3 Monotonicity and the First Derivative Test
- f′ > 0 on an interval ⇒ f increasing; f′ < 0 ⇒ f decreasing.
- **First Derivative Test**: at a critical point c, if f′ changes + → − then local max; − → + then local min; no sign change then neither.

### 4.4 Concavity and the Second Derivative Test
- f″ > 0 ⇒ concave up; f″ < 0 ⇒ concave down.
- **Inflection point**: where concavity changes (requires f″ = 0 or undefined *and* a sign change).
- **Second Derivative Test**: at critical c with f′(c) = 0: if f″(c) > 0 ⇒ local min; if f″(c) < 0 ⇒ local max; if f″(c) = 0 ⇒ test inconclusive (fall back to first derivative test).

### 4.5 Curve sketching — full procedure
1. Domain; x- and y-intercepts.
2. Symmetry (even/odd/periodic).
3. Asymptotes — vertical (zeros of denominator), horizontal (limits at ±∞), slant.
4. f′: critical points, intervals of increase/decrease, local extrema.
5. f″: concavity intervals, inflection points.
6. Plot key points; connect respecting all the above.

### 4.6 Optimization (applied max/min)
*Algorithm*:
1. Read carefully; draw and label a diagram.
2. Write the **objective function** (the quantity to be maximized/minimized).
3. Write **constraint equation(s)** relating the variables.
4. Use the constraint to reduce the objective to **one variable**; note its valid domain.
5. Differentiate, find critical points, apply first/second derivative test or closed-interval method.
6. Confirm it is the desired extremum; answer the actual question with units.

**Pitfalls**: optimizing the constraint instead of the objective; ignoring the physical domain; forgetting to check endpoints.

### 4.7 L'Hôpital's Rule
If lim f/g is of indeterminate form 0/0 or ±∞/±∞, and f, g differentiable near a with g′ ≠ 0, then
lim_{x→a} f(x)/g(x) = lim_{x→a} f′(x)/g′(x),
provided the right side exists (or is ±∞). May be applied repeatedly.

**Other indeterminate forms** — convert first:
- 0·∞ → rewrite as 0/0 or ∞/∞ (move one factor to denominator).
- ∞ − ∞ → combine into a single fraction.
- 1^∞, 0⁰, ∞⁰ → set y = expression, take ln, evaluate lim of ln y, then exponentiate.

**Pitfall**: applying L'Hôpital to non-indeterminate forms (gives wrong answers); differentiating the quotient with the quotient rule instead of differentiating numerator and denominator separately.

### 4.8 Newton's Method
Root-finding iteration: x_{n+1} = xₙ − f(xₙ)/f′(xₙ). Converges quadratically near a simple root if the initial guess is good. *Failure modes*: f′(xₙ) = 0, oscillation, divergence with a poor initial guess.

### 4.9 Linear approximation and differentials
**Linearization** of f at a: L(x) = f(a) + f′(a)(x − a) ≈ f(x) for x near a.
**Differential**: dy = f′(x) dx. Used for error propagation: Δy ≈ dy. Relative error ≈ dy/y.

---

## 5. Introduction to Integration

### 5.1 Antiderivatives and indefinite integrals
F is an **antiderivative** of f if F′ = f. The **general antiderivative** is F(x) + C. The **indefinite integral** ∫ f(x) dx = F(x) + C.

**Basic antiderivative table**:
| ∫ f dx | Result |
|---|---|
| ∫ xⁿ dx (n ≠ −1) | xⁿ⁺¹/(n+1) + C |
| ∫ (1/x) dx | ln|x| + C |
| ∫ eˣ dx | eˣ + C |
| ∫ bˣ dx | bˣ/ln b + C |
| ∫ sin x dx | −cos x + C |
| ∫ cos x dx | sin x + C |
| ∫ sec²x dx | tan x + C |
| ∫ sec x tan x dx | sec x + C |
| ∫ csc²x dx | −cot x + C |
| ∫ csc x cot x dx | −csc x + C |
| ∫ 1/√(1 − x²) dx | arcsin x + C |
| ∫ 1/(1 + x²) dx | arctan x + C |
| ∫ 1/(|x|√(x² − 1)) dx | arcsec|x| + C |

### 5.2 Riemann sums and the definite integral
Partition [a, b] into n subintervals of width Δx = (b − a)/n with sample points xᵢ*. The **Riemann sum** is Σᵢ f(xᵢ*) Δx. Left, right, and midpoint sums differ by sample-point choice.

**Definite integral**: ∫ₐᵇ f(x) dx = lim_{n→∞} Σᵢ₌₁ⁿ f(xᵢ*) Δx, when the limit exists (f integrable; guaranteed if f continuous on [a, b]).

**Geometric meaning**: signed area between the curve and the x-axis (area below the axis counts negative).

**Properties**: 
- ∫ₐᵃ f = 0; ∫ₐᵇ f = −∫_bᵃ f
- ∫ₐᵇ (f ± g) = ∫ₐᵇ f ± ∫ₐᵇ g; ∫ₐᵇ cf = c∫ₐᵇ f
- ∫ₐᵇ f = ∫ₐᶜ f + ∫_cᵇ f
- Comparison: f ≤ g on [a, b] ⇒ ∫ₐᵇ f ≤ ∫ₐᵇ g

**Useful summation formulas**: Σ i = n(n+1)/2; Σ i² = n(n+1)(2n+1)/6; Σ i³ = [n(n+1)/2]².

### 5.3 Fundamental Theorem of Calculus
**FTC Part 1**: if f is continuous on [a, b] and g(x) = ∫ₐˣ f(t) dt, then g is differentiable and g′(x) = f(x). With a variable upper limit u(x): d/dx ∫ₐ^{u(x)} f(t) dt = f(u(x))·u′(x) (chain rule). With both limits variable, split and apply to each.

**FTC Part 2 (Evaluation Theorem)**: if f is continuous on [a, b] and F is *any* antiderivative of f, then ∫ₐᵇ f(x) dx = F(b) − F(a).

**Mean Value Theorem for Integrals**: there exists c ∈ [a, b] with f(c) = (1/(b − a)) ∫ₐᵇ f(x) dx. This f(c) is the **average value** f_avg of f on [a, b].

### 5.4 The Net Change Theorem
∫ₐᵇ F′(x) dx = F(b) − F(a): the integral of a rate of change is the net change. *Application*: if v(t) is velocity, ∫ v dt = displacement, while ∫ |v| dt = total distance traveled.

### 5.5 Substitution (u-substitution)
Reverses the chain rule. For ∫ f(g(x)) g′(x) dx, let u = g(x), du = g′(x) dx ⇒ ∫ f(u) du.
*Procedure*: choose u (usually the "inside" function whose derivative also appears, up to a constant); compute du; rewrite the entire integrand (and, for definite integrals, **change the limits** to u-values — or substitute back before evaluating). 

**Pitfalls**: forgetting to change limits in definite integrals; leaving a leftover x; sign errors with the du constant.

---

# PART II — CALCULUS II

## 6. Techniques of Integration

### 6.1 Integration by parts
Reverses the product rule. ∫ u dv = uv − ∫ v du.

**LIATE heuristic** for choosing u (pick the type that comes *first*): **L**ogarithmic, **I**nverse trig, **A**lgebraic (polynomial), **T**rigonometric, **E**xponential. The remaining part is dv.

*Patterns*:
- ∫ xⁿ eˣ dx, ∫ xⁿ sin x dx — algebraic = u; may need repeated parts (tabular method speeds this up).
- ∫ ln x dx, ∫ arctan x dx — the lone transcendental is u, dv = dx.
- **Cyclic / boomerang** integrals (∫ eˣ sin x dx): apply parts twice; the original integral reappears — solve algebraically for it.

**Tabular integration**: for ∫ (polynomial)·(easily integrated function), tabulate successive derivatives of the polynomial and successive antiderivatives of the other factor, multiply along diagonals with alternating signs.

### 6.2 Trigonometric integrals
**∫ sinᵐx cosⁿx dx**:
- If m odd: split off one sin x, convert remaining sin² = 1 − cos², substitute u = cos x.
- If n odd: split off one cos x, convert remaining cos² = 1 − sin², substitute u = sin x.
- If both even: use power-reduction sin²x = (1 − cos 2x)/2, cos²x = (1 + cos 2x)/2 repeatedly.

**∫ tanᵐx secⁿx dx**:
- If n even (n ≥ 2): split off sec²x, convert remaining sec² = 1 + tan², substitute u = tan x.
- If m odd: split off sec x tan x, convert remaining tan² = sec² − 1, substitute u = sec x.

**Products of different angles** ∫ sin(mx) cos(nx) dx etc.: use product-to-sum identities.

### 6.3 Trigonometric substitution
For integrands containing these radicals, substitute to eliminate the root:
| Radical | Substitution | Identity used |
|---|---|---|
| √(a² − x²) | x = a sin θ | 1 − sin²θ = cos²θ |
| √(a² + x²) | x = a tan θ | 1 + tan²θ = sec²θ |
| √(x² − a²) | x = a sec θ | sec²θ − 1 = tan²θ |

*Procedure*: substitute x and dx; simplify the radical; integrate in θ; convert back using a **reference right triangle** (label sides from the substitution). For definite integrals, either change limits to θ or convert back.

### 6.4 Partial fraction decomposition
For ∫ p(x)/q(x) dx with deg p < deg q (if not, do **polynomial long division** first):
1. Factor q(x) completely into linear and irreducible quadratic factors.
2. Set up the decomposition:
   - Each distinct linear factor (x − a): term A/(x − a).
   - Repeated linear (x − a)ᵏ: terms A₁/(x − a) + A₂/(x − a)² + … + Aₖ/(x − a)ᵏ.
   - Each irreducible quadratic (x² + bx + c): term (Bx + C)/(x² + bx + c).
   - Repeated irreducible quadratic: analogous tower of terms.
3. Multiply through by q(x); solve for constants (substitute convenient x-values, and/or equate coefficients).
4. Integrate term-by-term: linear terms → ln; quadratic terms → ln and/or arctan (complete the square as needed).

### 6.5 Strategy and numerical integration
**General strategy**: simplify algebraically; recognize a basic form; try substitution; classify by form (parts? trig? trig sub? partial fractions?); manipulate (multiply by a conjugate, split fractions).

**Numerical integration** (when no elementary antiderivative exists):
- **Midpoint Rule**: M_n = Δx Σ f(midpointᵢ).
- **Trapezoidal Rule**: T_n = (Δx/2)[f(x₀) + 2f(x₁) + … + 2f(x_{n−1}) + f(xₙ)].
- **Simpson's Rule** (n even): S_n = (Δx/3)[f(x₀) + 4f(x₁) + 2f(x₂) + 4f(x₃) + … + 4f(x_{n−1}) + f(xₙ)].
- **Error bounds**: trapezoid error ≤ K(b−a)³/(12n²) with |f″| ≤ K; Simpson error ≤ K(b−a)⁵/(180n⁴) with |f⁽⁴⁾| ≤ K. Simpson is exact for cubics.

### 6.6 Improper integrals
**Type 1 (infinite interval)**: ∫ₐ^∞ f dx = lim_{t→∞} ∫ₐᵗ f dx; similarly to −∞. For ∫_{−∞}^∞ split at any point — **both** pieces must converge.

**Type 2 (discontinuous integrand)**: if f has an infinite discontinuity at b, ∫ₐᵇ f dx = lim_{t→b⁻} ∫ₐᵗ f dx. Split at any interior discontinuity.

An improper integral **converges** if the limit is finite, otherwise **diverges**.

**p-integral benchmarks**: ∫₁^∞ dx/xᵖ converges iff p > 1. ∫₀¹ dx/xᵖ converges iff p < 1.

**Comparison Theorem**: if 0 ≤ f ≤ g, then ∫ g converges ⇒ ∫ f converges; ∫ f diverges ⇒ ∫ g diverges.

**Pitfall**: evaluating an improper integral as if it were proper (failing to notice an interior discontinuity) — a leading cause of wrong "finite" answers.

---

## 7. Applications of Integration

### 7.1 Area between curves
- With respect to x: A = ∫ₐᵇ [top(x) − bottom(x)] dx. Find intersection points for limits; split where the top/bottom curves switch.
- With respect to y: A = ∫_cᵈ [right(y) − left(y)] dy — often simpler when curves are functions of y.

### 7.2 Volumes by slicing
General principle: V = ∫ A(x) dx, where A(x) is the cross-sectional area perpendicular to the axis.

**Disk method** (solid of revolution, no gap): V = π ∫ [R(x)]² dx.
**Washer method** (revolution with a hole): V = π ∫ ([R_outer]² − [R_inner]²) dx.
**Known cross-sections**: V = ∫ A(x) dx with A given (squares, equilateral triangles, semicircles, etc.).

*Procedure*: sketch the region and the axis of revolution; decide whether a representative slice is perpendicular (disk/washer) or parallel (shell) to the axis; express radii as functions of the integration variable; set limits.

### 7.3 Volumes by cylindrical shells
For revolution where slices parallel to the axis are convenient:
V = 2π ∫ (radius)(height) d(variable) = 2π ∫ₐᵇ x·f(x) dx (revolution about the y-axis, region under f).

**Choosing disk/washer vs. shell**: if the slice is **perpendicular** to the axis of revolution → disk/washer; if **parallel** → shell. Pick whichever avoids solving the curve for the other variable.

### 7.4 Arc length
For y = f(x) on [a, b]: L = ∫ₐᵇ √(1 + [f′(x)]²) dx.
For x = g(y) on [c, d]: L = ∫_cᵈ √(1 + [g′(y)]²) dy.
Parametric form (see §10): L = ∫ √[(dx/dt)² + (dy/dt)²] dt.

### 7.5 Surface area of revolution
About the x-axis: S = ∫ 2π·y·√(1 + (y′)²) dx.
About the y-axis: S = ∫ 2π·x·√(1 + (x′)²) dx (or analogous in y). The factor 2π·(radius) is the circumference traced by the arc-length element.

### 7.6 Physical applications
- **Work**: W = ∫ₐᵇ F(x) dx. Spring (Hooke's law F = kx): W = ∫ kx dx. **Pumping/lifting fluid**: W = ∫ (weight density)·(volume of slice)·(distance lifted) — set up a representative slice.
- **Hydrostatic force** on a submerged plate: F = ∫ (fluid weight density)·(depth)·(width) d(depth).
- **Center of mass / centroid** of a planar lamina of density ρ between curves: 
  M_x = ρ ∫ ½([f]² − [g]²) dx, M_y = ρ ∫ x[f − g] dx, mass m = ρ ∫ [f − g] dx; centroid x̄ = M_y/m, ȳ = M_x/m.
- **Probability**: a probability density function (pdf) satisfies f ≥ 0 and ∫_{−∞}^∞ f = 1; P(a ≤ X ≤ b) = ∫ₐᵇ f; mean μ = ∫ x f(x) dx.

### 7.7 Differential equations (introductory)
- **Separable equations**: dy/dx = g(x)h(y) ⇒ ∫ dy/h(y) = ∫ g(x) dx. Solve, then apply the initial condition to find C.
- **Exponential growth/decay**: dy/dt = ky ⇒ y = y₀e^{kt}.
- **Logistic model**: dy/dt = ky(1 − y/L) ⇒ solution approaches carrying capacity L.
- **Slope fields** visualize solution families; **Euler's method** y_{n+1} = yₙ + h·f(xₙ, yₙ) gives numerical approximations.

---

## 8. Sequences and Series

### 8.1 Sequences
A **sequence** {aₙ} is a function on the positive integers. **Convergence**: lim_{n→∞} aₙ = L (formally: ∀ε>0 ∃N such that n > N ⇒ |aₙ − L| < ε). Otherwise it **diverges**.

- Limit laws and L'Hôpital (treat n as continuous) apply.
- **Squeeze theorem** for sequences holds.
- **Monotone Convergence Theorem**: a bounded monotone sequence converges.
- Key facts: lim rⁿ = 0 if |r| < 1; lim n^(1/n) = 1; lim x^(1/n) = 1 (x > 0); lim (1 + x/n)ⁿ = eˣ; n! grows faster than any exponential, exponentials faster than any power.

### 8.2 Series and partial sums
A **series** Σ aₙ has **partial sums** s_N = Σ_{n=1}^N aₙ. The series **converges** to S if s_N → S; otherwise diverges.

**Geometric series** Σ arⁿ⁻¹: converges iff |r| < 1, with sum **a/(1 − r)**; diverges if |r| ≥ 1.

**Telescoping series**: write aₙ as a difference (often via partial fractions) so consecutive terms cancel; the sum is found from the surviving boundary terms.

**Divergence (nth-term) Test**: if lim aₙ ≠ 0 (or DNE), Σ aₙ diverges. *Caution*: lim aₙ = 0 does **not** imply convergence (harmonic series).

**p-series** Σ 1/nᵖ: converges iff p > 1. (p = 1 is the divergent **harmonic series**.)

### 8.3 Convergence tests — full toolkit
| Test | Applies to | Conclusion |
|---|---|---|
| **Divergence Test** | any series | lim aₙ ≠ 0 ⇒ diverges |
| **Geometric** | Σ arⁿ | converges iff \|r\| < 1 |
| **p-series** | Σ 1/nᵖ | converges iff p > 1 |
| **Integral Test** | aₙ = f(n), f positive, continuous, decreasing | Σ aₙ and ∫₁^∞ f dx converge or diverge together |
| **Comparison Test** | positive terms | 0 ≤ aₙ ≤ bₙ: Σbₙ conv ⇒ Σaₙ conv; Σaₙ div ⇒ Σbₙ div |
| **Limit Comparison** | positive terms | if lim aₙ/bₙ = c, 0 < c < ∞, both behave the same |
| **Alternating Series Test** | Σ(−1)ⁿbₙ, bₙ > 0 | converges if bₙ decreasing and bₙ → 0 |
| **Ratio Test** | any series | L = lim \|a_{n+1}/aₙ\|: L<1 abs conv, L>1 div, L=1 inconclusive |
| **Root Test** | any series | L = lim \|aₙ\|^(1/n): L<1 abs conv, L>1 div, L=1 inconclusive |

**Integral Test remainder estimate**: ∫_{N+1}^∞ f ≤ R_N ≤ ∫_N^∞ f.

### 8.4 Absolute vs. conditional convergence
- Σ aₙ **converges absolutely** if Σ |aₙ| converges. **Absolute convergence ⇒ convergence.**
- **Conditionally convergent**: Σ aₙ converges but Σ |aₙ| diverges (e.g. alternating harmonic series Σ(−1)ⁿ⁺¹/n).
- **Alternating Series Estimation Theorem**: error |S − s_N| ≤ b_{N+1} (first omitted term).
- Ratio/Root tests detect *absolute* convergence.

**Test-selection strategy**: check the divergence test first; recognize geometric/p-series; factorials or nth powers → ratio/root; rational/algebraic terms → limit comparison with a p-series; alternating → alternating series test (then check for absolute via the |aₙ| series); aₙ = f(n) nicely integrable → integral test.

### 8.5 Power series
A **power series** centered at a: Σ cₙ(x − a)ⁿ. There is a **radius of convergence** R such that the series converges absolutely for |x − a| < R and diverges for |x − a| > R (endpoints tested separately). The set of convergence is the **interval of convergence**.

*Procedure to find R and the interval*: apply the **ratio test** to |c_{n+1}(x−a)^{n+1} / cₙ(x−a)ⁿ|, set the limit < 1, solve for |x − a| < R. Then test each endpoint individually with an appropriate series test.

**Operations**: within (−R + a, a + R), a power series may be **differentiated and integrated term-by-term**, with the same R (endpoints may change).

### 8.6 Taylor and Maclaurin series
**Taylor series** of f about a: f(x) = Σ_{n=0}^∞ f⁽ⁿ⁾(a)/n! · (x − a)ⁿ.
**Maclaurin series**: the special case a = 0.

**Taylor's Theorem with remainder**: f(x) = T_N(x) + R_N(x), where the **Lagrange remainder** R_N(x) = f⁽ᴺ⁺¹⁾(z)/(N+1)! · (x − a)^{N+1} for some z between a and x. The series represents f exactly where R_N → 0.

**Essential Maclaurin series** (memorize):
| Function | Series | Interval |
|---|---|---|
| eˣ | Σ xⁿ/n! | (−∞, ∞) |
| sin x | Σ (−1)ⁿ x^{2n+1}/(2n+1)! | (−∞, ∞) |
| cos x | Σ (−1)ⁿ x^{2n}/(2n)! | (−∞, ∞) |
| 1/(1 − x) | Σ xⁿ | (−1, 1) |
| ln(1 + x) | Σ (−1)ⁿ⁺¹ xⁿ/n | (−1, 1] |
| arctan x | Σ (−1)ⁿ x^{2n+1}/(2n+1) | [−1, 1] |
| (1 + x)ᵏ | Σ C(k,n) xⁿ (binomial series) | (−1, 1) generally |

**Strategy for new series**: rather than computing derivatives, manipulate known series — substitute, multiply/divide by powers of x, differentiate, integrate, or multiply two series.

**Applications**: approximate values of functions and integrals with no elementary antiderivative (e.g. ∫ e^{−x²} dx); evaluate limits; bound approximation error via the remainder.

**Pitfalls**: forgetting to test endpoints; confusing radius with interval; ignoring that term-by-term integration can change endpoint behavior; using a series outside its interval of convergence.

---

## 9. Parametric Equations and Polar Coordinates

### 9.1 Parametric curves
A curve given by x = x(t), y = y(t), t ∈ I. **Eliminating the parameter** recovers a Cartesian relation (but may lose direction/range information).

- **Slope**: dy/dx = (dy/dt)/(dx/dt), provided dx/dt ≠ 0.
- **Second derivative**: d²y/dx² = (d/dt[dy/dx]) / (dx/dt).
- **Horizontal tangents**: dy/dt = 0 (and dx/dt ≠ 0); **vertical tangents**: dx/dt = 0 (and dy/dt ≠ 0).
- **Arc length**: L = ∫ₐᵇ √[(dx/dt)² + (dy/dt)²] dt.
- **Surface area** (revolution about x-axis): S = ∫ 2πy √[(dx/dt)² + (dy/dt)²] dt.
- **Area enclosed**: A = ∫ y dx = ∫_α^β y(t) x′(t) dt.

### 9.2 Polar coordinates
A point is (r, θ): r = directed distance from the pole, θ = angle from the polar axis.
**Conversion**: x = r cos θ, y = r sin θ; r² = x² + y², tan θ = y/x. Points have non-unique representations: (r, θ) = (r, θ + 2πn) = (−r, θ + π).

**Common polar curves**: circles r = a, r = 2a cos θ; cardioids r = a(1 ± cos θ); limaçons r = a ± b cos θ; roses r = a cos(nθ) (n petals if n odd, 2n if n even); lemniscates r² = a² cos 2θ.

- **Slope of a polar curve**: with x = r(θ) cos θ, y = r(θ) sin θ, dy/dx = (r′ sin θ + r cos θ)/(r′ cos θ − r sin θ).
- **Area in polar coordinates**: A = ½ ∫_α^β [r(θ)]² dθ. For area between two polar curves, integrate ½(r_outer² − r_inner²). Find intersection angles carefully (watch for the pole and multiple representations).
- **Arc length in polar**: L = ∫_α^β √[r² + (dr/dθ)²] dθ.

### 9.3 Conic sections
- **Parabola**: set of points equidistant from a focus and directrix. y² = 4px (horizontal), x² = 4py (vertical).
- **Ellipse**: x²/a² + y²/b² = 1 (a > b); foci at (±c, 0), c² = a² − b²; sum of focal distances = 2a.
- **Hyperbola**: x²/a² − y²/b² = 1; foci c² = a² + b²; asymptotes y = ±(b/a)x; difference of focal distances = 2a.
- **Polar form of conics**: r = ed/(1 ± e cos θ) or r = ed/(1 ± e sin θ), where e is eccentricity (e = 0 circle, 0 < e < 1 ellipse, e = 1 parabola, e > 1 hyperbola) and the focus is at the pole.

---

# PART III — CALCULUS III

## 10. Vectors and the Geometry of Space

### 10.1 Three-dimensional coordinate system
Right-handed system with axes x, y, z. **Distance** between P₁ and P₂: √[(Δx)² + (Δy)² + (Δz)²]. **Sphere** of radius r centered at (a, b, c): (x−a)² + (y−b)² + (z−c)² = r² (complete the square to identify spheres).

### 10.2 Vectors
A **vector** has magnitude and direction; **v** = ⟨v₁, v₂, v₃⟩. Standard basis **i** = ⟨1,0,0⟩, **j** = ⟨0,1,0⟩, **k** = ⟨0,0,1⟩.
- **Magnitude**: |**v**| = √(v₁² + v₂² + v₃²). **Unit vector**: **û** = **v**/|**v**|.
- **Operations**: addition, scalar multiplication componentwise. Parallelogram/triangle law geometrically.

### 10.3 Dot product
**v** · **w** = v₁w₁ + v₂w₂ + v₃w₃ = |**v**||**w**| cos θ.
- **v** · **v** = |**v**|².
- **Angle**: cos θ = (**v** · **w**)/(|**v**||**w**|).
- **Orthogonal** iff **v** · **w** = 0.
- **Scalar projection** of **v** onto **w**: comp_w **v** = (**v** · **w**)/|**w**|. **Vector projection**: proj_w **v** = [(**v** · **w**)/|**w**|²] **w**.
- **Work**: W = **F** · **d**.

### 10.4 Cross product
**v** × **w** = ⟨v₂w₃ − v₃w₂, v₃w₁ − v₁w₃, v₁w₂ − v₂w₁⟩ — computed as the symbolic determinant of [**i j k**; v₁ v₂ v₃; w₁ w₂ w₃].
- |**v** × **w**| = |**v**||**w**| sin θ = area of the parallelogram spanned by **v**, **w**.
- **v** × **w** is **orthogonal to both** **v** and **w**; direction by the right-hand rule.
- **Anticommutative**: **v** × **w** = −(**w** × **v**); **v** × **v** = **0**.
- **Parallel** vectors: **v** × **w** = **0**.
- **Scalar triple product** **u** · (**v** × **w**) = det[**u**; **v**; **w**] = signed volume of the parallelepiped; = 0 iff the three vectors are coplanar.

### 10.5 Lines and planes
**Line** through P₀ with direction **v**: vector form **r**(t) = **r₀** + t**v**; parametric x = x₀ + at, etc.; symmetric (x−x₀)/a = (y−y₀)/b = (z−z₀)/c.
**Plane** through P₀ with normal **n** = ⟨a, b, c⟩: a(x−x₀) + b(y−y₀) + c(z−z₀) = 0.
- **Distance from a point to a plane**: |a x₁ + b y₁ + c z₁ + d| / √(a² + b² + c²).
- Two planes are parallel iff normals are parallel; the angle between planes = angle between normals.
- Lines: parallel (directions parallel), intersecting, or **skew** (neither parallel nor intersecting).

### 10.6 Quadric surfaces
Identified by **traces** (cross-sections in coordinate planes): ellipsoid, elliptic paraboloid, hyperbolic paraboloid (saddle), cone, hyperboloid of one sheet, hyperboloid of two sheets. Cylinders: one variable missing.

### 10.7 Cylindrical and spherical coordinates
- **Cylindrical** (r, θ, z): x = r cos θ, y = r sin θ, z = z. Good for axial symmetry.
- **Spherical** (ρ, θ, φ): x = ρ sin φ cos θ, y = ρ sin φ sin θ, z = ρ cos φ; ρ ≥ 0, 0 ≤ φ ≤ π. Here ρ² = x² + y² + z². Good for spherical symmetry.

---

## 11. Vector-Valued Functions

### 11.1 Definition and calculus
**r**(t) = ⟨f(t), g(t), h(t)⟩ traces a space curve. Limits, derivatives, and integrals are taken **componentwise**.
- **r**′(t) = ⟨f′, g′, h′⟩ is the **tangent vector**; the **unit tangent** **T**(t) = **r**′/|**r**′|.
- **Differentiation rules**: product rules hold for scalar·vector, dot products, and cross products (order matters for the cross product).
- ∫ **r**(t) dt = ⟨∫f, ∫g, ∫h⟩ + **C**.

### 11.2 Arc length and curvature
- **Arc length**: L = ∫ₐᵇ |**r**′(t)| dt. **Arc length parameter**: s(t) = ∫ₐᵗ |**r**′(u)| du.
- **Curvature**: κ = |d**T**/ds| = |**T**′(t)| / |**r**′(t)| = |**r**′ × **r**″| / |**r**′|³.
- **Unit normal**: **N** = **T**′/|**T**′|; **binormal**: **B** = **T** × **N**. The trio {**T**, **N**, **B**} is the moving (Frenet) frame; the plane of **T**, **N** is the **osculating plane**.

### 11.3 Motion in space
If **r**(t) is position: velocity **v** = **r**′, speed = |**v**|, acceleration **a** = **r**″.
**Tangential/normal decomposition**: **a** = a_T **T** + a_N **N**, where a_T = d|**v**|/dt = (**v** · **a**)/|**v**| and a_N = κ|**v**|² = |**v** × **a**|/|**v**|. (No component along **B**.)

---

## 12. Partial Derivatives — Multivariable Differential Calculus

### 12.1 Functions of several variables
z = f(x, y): domain a region in the plane; visualized by **graphs**, **level curves** (f = k), and **contour maps**. For three variables, **level surfaces**.

### 12.2 Limits and continuity
lim_{(x,y)→(a,b)} f(x,y) = L means f approaches L **along every path**. To show a limit **does not exist**, find two paths giving different values (e.g. along x-axis vs. y-axis vs. y = x vs. y = mx vs. y = x²). To prove a limit exists, use the squeeze theorem or convert to polar coordinates. f is **continuous** at (a, b) if the limit equals f(a, b).

### 12.3 Partial derivatives
f_x = ∂f/∂x = lim_{h→0} [f(x+h, y) − f(x, y)]/h: differentiate treating y as constant. Similarly f_y.
**Higher-order**: f_xx, f_yy, f_xy, f_yx. **Clairaut's Theorem**: if f_xy and f_yx are continuous near (a,b), then f_xy(a,b) = f_yx(a,b) (mixed partials are equal).

### 12.4 Tangent planes and linear approximation
**Tangent plane** to z = f(x, y) at (a, b): z = f(a, b) + f_x(a,b)(x − a) + f_y(a,b)(y − b).
**Linearization** L(x,y) = that expression; **differential** dz = f_x dx + f_y dy.
f is **differentiable** at (a, b) if it can be well-approximated by its tangent plane (sufficient condition: f_x, f_y exist and are continuous near the point).

### 12.5 The Chain Rule (multivariable)
- If z = f(x, y), x = x(t), y = y(t): dz/dt = (∂z/∂x)(dx/dt) + (∂z/∂y)(dy/dt).
- If x = x(s, t), y = y(s, t): ∂z/∂s = (∂z/∂x)(∂x/∂s) + (∂z/∂y)(∂y/∂s), similarly ∂z/∂t.
- **Tree diagram** method: sum over every path from the dependent variable down to the independent variable, multiplying derivatives along each path.
- **Implicit differentiation**: if F(x, y) = 0, dy/dx = −F_x/F_y; if F(x, y, z) = 0, ∂z/∂x = −F_x/F_z, ∂z/∂y = −F_y/F_z.

### 12.6 Directional derivatives and the gradient
**Gradient**: ∇f = ⟨f_x, f_y, f_z⟩.
**Directional derivative** in the direction of unit vector **u**: D_**u** f = ∇f · **u**.
Key properties:
- ∇f points in the direction of **maximum rate of increase**; that maximum rate is |∇f|.
- The minimum rate is −|∇f| (direction −∇f); D_**u**f = 0 for **u** ⊥ ∇f.
- ∇f is **normal to level curves** (2-D) and **level surfaces** (3-D). Hence the tangent plane to a level surface F(x,y,z) = k at P is ∇F(P) · ⟨x−x₀, y−y₀, z−z₀⟩ = 0.

### 12.7 Maxima and minima
**Critical points**: ∇f = **0** (or a partial undefined).
**Second Derivative Test** for f(x, y): let D = f_xx f_yy − (f_xy)² at a critical point.
- D > 0 and f_xx > 0 ⇒ local minimum.
- D > 0 and f_xx < 0 ⇒ local maximum.
- D < 0 ⇒ saddle point.
- D = 0 ⇒ test inconclusive.

**Absolute extrema on a closed bounded region**: (1) find critical points in the interior; (2) find extrema on the boundary (parametrize the boundary, or use Lagrange multipliers); (3) compare all candidate values.

### 12.8 Lagrange multipliers
To optimize f subject to constraint g = k: solve the system ∇f = λ∇g together with g = k. Geometrically, at a constrained extremum the level curve of f is tangent to the constraint curve, so their gradients are parallel.
- **Two constraints** g = k₁, h = k₂: ∇f = λ∇g + μ∇h, with both constraints.
*Procedure*: write the component equations, solve for the variables and λ (be careful with cases where a variable or λ is zero), evaluate f at every solution, pick the largest/smallest. Always check that extrema exist (e.g. constraint set compact).

**Pitfalls**: forgetting the constraint equation itself; dividing by a quantity that might be zero (losing solutions); confusing the multiplier value λ with the answer.

---

## 13. Multiple Integrals

### 13.1 Double integrals over rectangles
∫∫_R f(x,y) dA = lim of Riemann sums Σ f(xᵢⱼ*, yᵢⱼ*) ΔA. Represents signed volume under z = f(x,y).
**Fubini's Theorem**: over a rectangle R = [a,b]×[c,d], ∫∫_R f dA = ∫ₐᵇ ∫_cᵈ f dy dx = ∫_cᵈ ∫ₐᵇ f dx dy (iterated integrals, either order).

### 13.2 Double integrals over general regions
- **Type I** (vertically simple): a ≤ x ≤ b, g₁(x) ≤ y ≤ g₂(x): ∫∫ f dA = ∫ₐᵇ ∫_{g₁(x)}^{g₂(x)} f dy dx.
- **Type II** (horizontally simple): c ≤ y ≤ d, h₁(y) ≤ x ≤ h₂(y): ∫∫ f dA = ∫_cᵈ ∫_{h₁(y)}^{h₂(y)} f dx dy.
- **Changing the order of integration**: sketch the region, re-describe it in the other type's language, rewrite the limits. Often essential when the inner antiderivative is intractable in one order.
- **Properties**: linearity; additivity over subregions; ∫∫_R 1 dA = area of R.

### 13.3 Double integrals in polar coordinates
For regions with circular symmetry: ∫∫_R f(x,y) dA = ∫_α^β ∫_{r₁(θ)}^{r₂(θ)} f(r cos θ, r sin θ) **r** dr dθ.
**The extra factor r is the Jacobian** and must never be omitted. Convert x² + y² → r², and recognize disks, annuli, and sectors.

### 13.4 Applications of double integrals
- **Area**: ∫∫_R dA. **Volume** between two surfaces: ∫∫_R (top − bottom) dA.
- **Mass** of a lamina with density ρ(x,y): m = ∫∫_R ρ dA.
- **Moments**: M_x = ∫∫ y ρ dA, M_y = ∫∫ x ρ dA; **center of mass** x̄ = M_y/m, ȳ = M_x/m.
- **Moments of inertia**: I_x = ∫∫ y² ρ dA, I_y = ∫∫ x² ρ dA, I₀ = I_x + I_y.
- **Surface area** of z = f(x,y) over R: S = ∫∫_R √(1 + f_x² + f_y²) dA.

### 13.5 Triple integrals
∫∫∫_E f(x,y,z) dV, evaluated as an iterated integral. Describe E by projecting onto a coordinate plane and bounding the third variable between two surfaces, e.g. ∫∫_D ∫_{u₁(x,y)}^{u₂(x,y)} f dz dA.
- **Volume**: ∫∫∫_E dV. **Mass**, **center of mass**, **moments of inertia** generalize directly.

### 13.6 Triple integrals in cylindrical and spherical coordinates
- **Cylindrical**: dV = **r** dz dr dθ. Use for cylinders, cones, paraboloids about an axis.
- **Spherical**: dV = **ρ² sin φ** dρ dφ dθ. Use for spheres, cones from the origin, regions bounded by ρ = const or φ = const. Bounds: ρ ≥ 0, 0 ≤ φ ≤ π, θ over the relevant angular range.
- The volume elements r and ρ² sin φ are the Jacobians of the respective coordinate transformations — omitting them is the single most common error.

### 13.7 Change of variables (Jacobian)
For a transformation x = x(u,v), y = y(u,v):
∫∫_R f dA = ∫∫_S f(x(u,v), y(u,v)) |∂(x,y)/∂(u,v)| du dv,
where the **Jacobian** ∂(x,y)/∂(u,v) = det[x_u x_v; y_u y_v]. The triple-integral version uses the 3×3 Jacobian. *Procedure*: choose a substitution that simplifies the integrand **or** the region; compute the Jacobian; transform the region S; rewrite and integrate. Polar/cylindrical/spherical are special cases.

---

## 14. Vector Calculus

### 14.1 Vector fields
**F**(x,y) = ⟨P(x,y), Q(x,y)⟩ or **F**(x,y,z) = ⟨P, Q, R⟩ assigns a vector to each point. Examples: velocity fields, force fields, gradient fields ∇f.
A **conservative** vector field is one that equals ∇f for some **potential function** f.

### 14.2 Line integrals
**Scalar line integral**: ∫_C f ds = ∫ₐᵇ f(**r**(t)) |**r**′(t)| dt. (Independent of orientation.)
**Vector line integral** (work): ∫_C **F** · d**r** = ∫ₐᵇ **F**(**r**(t)) · **r**′(t) dt = ∫_C P dx + Q dy + R dz. (Reverses sign with orientation.)
*Procedure*: parametrize C; substitute into **F** and compute **r**′(t); take the dot product; integrate over the parameter interval. Piecewise curves: sum over the pieces.

### 14.3 Fundamental Theorem for Line Integrals
If **F** = ∇f and C goes from point A to point B, then
∫_C **F** · d**r** = f(B) − f(A).
Consequences: the integral of a conservative field is **path-independent**; ∮_C **F** · d**r** = 0 around any closed loop.

**Test for conservative fields** (on a simply connected domain):
- In 2-D: **F** = ⟨P, Q⟩ is conservative iff ∂P/∂y = ∂Q/∂x.
- In 3-D: **F** = ⟨P, Q, R⟩ is conservative iff curl **F** = **0**, i.e. R_y = Q_z, P_z = R_x, Q_x = P_y.

**Finding the potential function f**: integrate P with respect to x (constant of integration is a function g(y[,z])); differentiate the result with respect to y and match Q to pin down g; repeat for z if 3-D.

### 14.4 Green's Theorem
Relates a line integral around a positively oriented (counterclockwise), piecewise-smooth, simple closed curve C to a double integral over the enclosed region D:
**∮_C P dx + Q dy = ∫∫_D (∂Q/∂x − ∂P/∂y) dA.**
- **Circulation–curl form**: ∮_C **F** · d**r** = ∫∫_D (curl **F**) · **k** dA.
- **Flux–divergence form**: ∮_C **F** · **n** ds = ∫∫_D div **F** dA.
- **Area via Green's Theorem**: A = ∮_C x dy = −∮_C y dx = ½ ∮_C (x dy − y dx).
- For regions with holes, orient outer boundary counterclockwise and inner boundaries clockwise.

### 14.5 Curl and divergence
For **F** = ⟨P, Q, R⟩:
- **curl F** = ∇ × **F** = ⟨R_y − Q_z, P_z − R_x, Q_x − P_y⟩ — measures rotation; curl **F** = **0** ⇒ irrotational (conservative on simply connected domains).
- **div F** = ∇ · **F** = P_x + Q_y + R_z — a scalar measuring net outflow (source/sink density).
**Identities**: div(curl **F**) = 0; curl(∇f) = **0**; ∇·(∇f) = ∇²f = f_xx + f_yy + f_zz (the Laplacian).

### 14.6 Parametric surfaces and surface integrals
**Parametric surface**: **r**(u,v) = ⟨x(u,v), y(u,v), z(u,v)⟩. The **normal vector** is **r**_u × **r**_v; surface area element dS = |**r**_u × **r**_v| dA.
- **Surface area**: S = ∫∫_D |**r**_u × **r**_v| du dv. For a graph z = g(x,y): dS = √(1 + g_x² + g_y²) dA.
- **Scalar surface integral**: ∫∫_S f dS = ∫∫_D f(**r**(u,v)) |**r**_u × **r**_v| du dv.
- **Flux integral** (oriented surface, **n** the unit normal): ∫∫_S **F** · d**S** = ∫∫_S **F** · **n** dS = ∫∫_D **F** · (**r**_u × **r**_v) du dv. Choose **r**_u × **r**_v consistent with the desired orientation (e.g. outward).

### 14.7 Stokes' Theorem
Generalizes Green's Theorem to surfaces in space. For an oriented, piecewise-smooth surface S with positively oriented boundary curve ∂S:
**∮_{∂S} F · dr = ∫∫_S (curl F) · dS.**
The orientation rule: if you walk along ∂S with the surface normal pointing "up" (toward you on your left), you traverse the boundary so the surface is on your left. Often used to (a) replace a hard line integral by an easier surface integral or (b) replace one surface by another sharing the same boundary.

### 14.8 The Divergence Theorem (Gauss's Theorem)
For a solid region E with closed boundary surface S oriented outward:
**∫∫_S F · dS = ∫∫∫_E div F dV.**
Converts a flux integral over a closed surface into a triple integral of the divergence — usually far easier. *Requirement*: S must be a **closed** surface enclosing E; if a problem gives an open surface, close it with an auxiliary surface (e.g. a cap), apply the theorem, then subtract the auxiliary flux.

### 14.9 The unifying picture
All of these are instances of the generalized Stokes' theorem "∫ (boundary) = ∫ (derivative over interior)":
| Theorem | Lower-dim integral | Higher-dim integral |
|---|---|---|
| FTC | F at endpoints | ∫ F′ dx over an interval |
| FT for Line Integrals | f at endpoints of C | ∫_C ∇f · d**r** |
| Green's Theorem | ∮_C **F** · d**r** | ∫∫_D (Q_x − P_y) dA |
| Stokes' Theorem | ∮_{∂S} **F** · d**r** | ∫∫_S curl **F** · d**S** |
| Divergence Theorem | ∫∫_S **F** · d**S** | ∫∫∫_E div **F** dV |

**Pitfalls in vector calculus**: wrong orientation (sign errors); using Green's/Stokes'/Divergence theorems when hypotheses fail (curve not closed, surface not closed, field not defined on the whole region — e.g. a singularity at the origin); forgetting the Jacobian/surface-element factor; mixing up curl (vector) and divergence (scalar); assuming a field is conservative without checking on a *simply connected* domain.

---

## Appendix A — Cross-Course Pitfall Summary

- **Algebra/trig decay**: most calculus errors are actually algebra or trig errors. Keep identities sharp.
- **+C**: never omit the constant on an indefinite integral; in differential equations it must be found from initial conditions before the solution is "done."
- **Limits of integration under substitution**: change them (or back-substitute) — do not leave x-limits with a u-integrand.
- **Indeterminate forms**: confirm the form is genuinely indeterminate before L'Hôpital; convert 0·∞, ∞−∞, 1^∞, 0⁰, ∞⁰ first.
- **Series**: lim aₙ = 0 is necessary, not sufficient; always test endpoints of an interval of convergence; ratio/root test L = 1 means *try something else*.
- **Multivariable limits**: one path is never enough to prove existence; two disagreeing paths *do* prove non-existence.
- **Jacobians**: r in polar, r in cylindrical, ρ² sin φ in spherical, and the determinant factor in general change-of-variables — omitting these is the most common multiple-integral mistake.
- **Orientation**: line, surface, and flux integrals are orientation-sensitive; Green's/Stokes'/Divergence theorems require specific orientations and closure/smoothness hypotheses.
- **Conservative fields**: the partial-derivative test only guarantees conservativeness on a *simply connected* domain.

---

## Open-source sources used

- **OpenStax Calculus, Volume 1** (Strang, Herman, et al.) — limits, derivatives, applications of differentiation, introduction to integration. openstax.org/details/books/calculus-volume-1
- **OpenStax Calculus, Volume 2** — integration techniques, applications of integrals, sequences & series, parametric equations & polar coordinates. openstax.org/details/books/calculus-volume-2
- **OpenStax Calculus, Volume 3** — parametric/polar review, vectors & 3-D geometry, vector-valued functions, multivariable differentiation, multiple integrals, vector calculus. openstax.org/details/books/calculus-volume-3
- **Paul's Online Math Notes** (Paul Dawkins, Lamar University) — Calculus I, II, and III complete note sets; theorem statements, solution algorithms, and worked-example patterns. tutorial.math.lamar.edu
- **MIT OpenCourseWare 18.01 (Single Variable Calculus)** and **18.02 (Multivariable Calculus)** — lecture notes, theorem framing, and the unifying view of the fundamental theorems. ocw.mit.edu
- **APEX Calculus** (Hartman et al.) — open-source calculus text; reinforcement of integration techniques, series tests, and vector calculus. apexcalculus.com
- **LibreTexts Mathematics — Calculus** (libretexts.org) — Calculus I–III open course shelves, cross-referenced for definitions and theorem statements.
