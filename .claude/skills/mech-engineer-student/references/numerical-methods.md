# Numerical Methods & MATLAB Reference

> Graduate-level study companion for **ME 1311 — MATLAB for Engineers / Numerical Methods**.
> Covers MATLAB programming constructs, root finding, linear systems, interpolation, curve fitting, numerical differentiation/integration, and numerical ODE solvers.
> Math is plain text: `Σ` = sum, `∫` = integral, `≈` ≈, `√` = square root, `∂` = partial derivative, `|x|` = absolute value.

---

## 0. Numerical Computing Fundamentals

### 0.1 Sources of Error
| Error type | Cause |
|---|---|
| **Round-off error** | finite floating-point precision (≈16 significant digits, machine epsilon `eps ≈ 2.2e-16`) |
| **Truncation error** | approximating an infinite/continuous process by a finite one (e.g., truncating a Taylor series) |
| **Propagated error** | input errors carried/amplified through a computation |
| **Modeling error** | the math model itself imperfectly describes reality |

### 0.2 Error Measures
- **Absolute error:** `E_abs = |x_true − x_approx|`.
- **Relative error:** `E_rel = |x_true − x_approx| / |x_true|`.
- **Approximate relative error** (iterative): `ε_a = |(x_new − x_old)/x_new|` — used as a stopping test when the true value is unknown.

### 0.3 Stability & Conditioning
- A **well-conditioned** problem: small input changes → small output changes. **Ill-conditioned**: small input changes → large output changes.
- A **stable** algorithm does not amplify round-off error. Avoid subtracting nearly equal numbers (**catastrophic cancellation**).
- **Convergence order:** if `|e_{n+1}| ≈ C |e_n|^p`, the method is order `p` — `p=1` linear, `p=2` quadratic.

### 0.4 Stopping Criteria
Iterate until: `ε_a < tol` (relative change small), **and/or** `|f(x)| < tol` (residual small), **and/or** `iterations < max_iter` (safety cap — always include this).

---

## 1. MATLAB Programming Constructs for Engineers

### 1.1 Variables, Vectors, Matrices
```matlab
x = 5;                  % scalar; semicolon suppresses output
v = [1 2 3 4];          % row vector
c = [1; 2; 3];          % column vector
A = [1 2; 3 4];         % 2x2 matrix
t = 0:0.1:10;           % start:step:stop  -> evenly spaced vector
t = linspace(0,10,101); % 101 points from 0 to 10
z = zeros(3,3); o = ones(2,4); I = eye(3);  % preallocate
```

### 1.2 Element-wise vs. Matrix Operations (critical distinction)
| Operator | Meaning |
|---|---|
| `*  /  ^` | matrix multiply / solve / power (linear-algebra) |
| `.*  ./  .^` | **element-wise** multiply / divide / power |
| `'` | transpose (conjugate); `.'` plain transpose |
| `\` | left division — `A\b` solves `Ax = b` |

**Pitfall #1 for engineers:** forgetting the dot. `v^2` errors or does matrix power; `v.^2` squares each element. When applying a formula across a vector of inputs, you almost always want `.* ./ .^`.

### 1.3 Control Flow
```matlab
if cond,  ... elseif cond2, ... else, ... end
for k = 1:n,  ...  end
while cond,  ...  end
% vectorize instead of looping when possible — much faster
```

### 1.4 Functions
```matlab
function [out1, out2] = myfun(in1, in2)   % saved as myfun.m
    out1 = in1 + in2;
    out2 = in1 * in2;
end

f = @(x) x.^2 - 3*x + 2;   % anonymous function handle (use .^ for vector input)
g = @(x,y) x.*y + 1;
```

### 1.5 Output, Plotting, Debugging
```matlab
fprintf('x = %.4f, error = %.2e\n', x, err);
plot(t, y, 'b-o'); xlabel('t'); ylabel('y'); grid on; title('...');
hold on;            % overlay multiple curves
disp(A); format long;
```
Debugging: set breakpoints, inspect the Workspace, use `size()`, `length()`, `whos`. Common error: **dimension mismatch** — check with `size()`.

### 1.6 Preallocation & Vectorization
Growing an array inside a loop (`v(end+1)=...`) is slow. **Preallocate** (`v = zeros(1,n)`) then fill. Better still, replace loops with vectorized expressions.

---

## 2. Root Finding — Solving f(x) = 0

### 2.1 Bisection Method
**Idea:** if `f` is continuous and `f(a)·f(b) < 0`, a root lies in `[a,b]` (Intermediate Value Theorem). Repeatedly halve the interval.

**Algorithm:**
```
given a, b with f(a)*f(b) < 0, tolerance tol
repeat:
    c = (a + b)/2
    if f(a)*f(c) < 0:  b = c     % root in left half
    else:              a = c     % root in right half
until (b - a)/2 < tol  or  f(c) == 0
return c
```
- **Convergence:** linear, error halves each step. After `n` steps, error `≤ (b−a)/2^(n+1)`. Iterations needed: `n ≥ log₂((b−a)/tol) − 1`.
- **Pros:** always converges (bracketing, guaranteed). **Cons:** slow; needs a sign change (misses even-multiplicity roots).

```matlab
a = 1; b = 2; tol = 1e-6; f = @(x) x.^3 - x - 2;
while (b-a)/2 > tol
    c = (a+b)/2;
    if f(a)*f(c) < 0,  b = c;  else,  a = c;  end
end
root = (a+b)/2;
```

### 2.2 Newton–Raphson Method
**Idea:** follow the tangent line to its x-intercept.
```
x_{n+1} = x_n − f(x_n) / f'(x_n)
```
- **Convergence:** quadratic *near* a simple root (error roughly squares each step).
- **Pros:** very fast. **Cons:** needs the derivative `f'`; can diverge or cycle with a bad initial guess; fails if `f'(x_n) = 0`; only linear convergence at multiple roots.

```matlab
f = @(x) x.^3 - x - 2;  df = @(x) 3*x.^2 - 1;
x = 1.5; tol = 1e-8;
for k = 1:50
    xnew = x - f(x)/df(x);
    if abs(xnew - x) < tol,  break;  end
    x = xnew;
end
```

### 2.3 Secant Method
**Idea:** Newton's method but approximate `f'` with a finite difference using the last two iterates — no analytic derivative needed.
```
x_{n+1} = x_n − f(x_n) · (x_n − x_{n−1}) / (f(x_n) − f(x_{n−1}))
```
- **Convergence:** superlinear, order ≈ 1.618 (golden ratio). Between bisection and Newton in speed; no derivative required. Needs two starting points.

### 2.4 Fixed-Point Iteration
Rewrite `f(x) = 0` as `x = g(x)`; iterate `x_{n+1} = g(x_n)`.
- **Convergence theorem:** converges to a fixed point `x*` if `|g'(x*)| < 1` near `x*` (the smaller `|g'|`, the faster). Diverges if `|g'(x*)| > 1`.

### 2.5 MATLAB Built-ins
```matlab
root = fzero(f, x0);          % scalar root near x0; or fzero(f,[a b]) with a bracket
roots([1 0 -1 -2]);           % all roots of a polynomial (coefficients high->low degree)
sol = fsolve(F, x0);          % systems of nonlinear equations (Optimization Toolbox)
```
`fzero` combines bisection, secant, and inverse quadratic interpolation — robust and the practical default for one equation.

**Root-finding pitfalls:** bad initial guess (Newton diverges); roots of even multiplicity (no sign change, bisection fails, Newton slows to linear); choosing a bracket that contains zero or several roots; forgetting that `f` must be continuous on the bracket.

---

## 3. Solving Linear Systems Ax = b

### 3.1 Gaussian Elimination with Back Substitution
**Forward elimination:** use row operations to make `A` upper-triangular `U`. **Back substitution:** solve from the last equation upward.
- **Partial pivoting:** before eliminating column `k`, swap in the row with the largest `|pivot|`. Essential — avoids dividing by tiny/zero pivots and controls round-off growth.
- **Operation count:** `O(n³/3)` for elimination, `O(n²)` for back substitution.

### 3.2 LU Decomposition
Factor `A = LU` (`L` lower-triangular with unit diagonal, `U` upper-triangular). With pivoting: `PA = LU`.
**Solve `Ax = b`:** (1) forward-solve `Ly = Pb`; (2) back-solve `Ux = y`.
**Why:** factor once (`O(n³)`), then solve for many right-hand-sides cheaply (`O(n²)` each).

### 3.3 Iterative Methods
| Method | Update | Notes |
|---|---|---|
| **Jacobi** | `x_i^(k+1) = (b_i − Σ_{j≠i} a_ij x_j^(k)) / a_ii` | uses only old values |
| **Gauss–Seidel** | same but uses updated `x_j` as soon as available | usually faster than Jacobi |

**Convergence:** guaranteed if `A` is **strictly diagonally dominant** (`|a_ii| > Σ_{j≠i} |a_ij|` for every row). Best for large, sparse systems.

### 3.4 Condition Number
`cond(A) = ||A|| · ||A⁻¹||`. Large `cond(A)` ⇒ **ill-conditioned**: tiny perturbations in `b` cause huge changes in `x`. Roughly, you lose `log₁₀(cond(A))` digits of accuracy.

### 3.5 MATLAB Syntax
```matlab
x = A\b;              % backslash — preferred; picks the best solver automatically
[L,U,P] = lu(A);      % LU with permutation P
x = U\(L\(P*b));      % solve with the factors
inv(A);               % AVOID for solving systems — slower and less accurate than \
det(A);  rank(A);  cond(A);  norm(A);
[V,D] = eig(A);       % eigenvectors V, eigenvalues on diag(D)
```
**Pitfall:** using `x = inv(A)*b` instead of `x = A\b`. Backslash is faster and numerically better. Never invert a matrix just to solve one system.

---

## 4. Interpolation

**Goal:** find a function passing **exactly** through `n+1` data points `(x₀,y₀),...,(xₙ,yₙ)`.

### 4.1 Polynomial Interpolation — Existence
There is a **unique** polynomial of degree `≤ n` through `n+1` distinct points.

### 4.2 Lagrange Interpolating Polynomial
```
P(x) = Σ_{i=0}^{n} y_i · L_i(x),   L_i(x) = Π_{j≠i} (x − x_j)/(x_i − x_j)
```
Each basis polynomial `L_i` is 1 at `x_i` and 0 at every other node. No linear system to solve, but adding a point means recomputing everything.

### 4.3 Newton's Divided-Difference Form
```
P(x) = a₀ + a₁(x−x₀) + a₂(x−x₀)(x−x₁) + ...
```
Coefficients `aₖ` = divided differences `f[x₀,...,xₖ]`, built recursively:
```
f[xᵢ] = yᵢ
f[xᵢ,...,xᵢ₊ₖ] = (f[xᵢ₊₁,...,xᵢ₊ₖ] − f[xᵢ,...,xᵢ₊ₖ₋₁]) / (xᵢ₊ₖ − xᵢ)
```
**Advantage:** adding a new data point only adds one term — existing coefficients are reused.

### 4.4 Runge's Phenomenon
High-degree polynomial interpolation on **equally spaced** nodes can oscillate wildly near the interval ends. **Fixes:** use a lower degree, use Chebyshev nodes (clustered at the ends), or use piecewise/spline interpolation.

### 4.5 Spline Interpolation
Piecewise low-degree polynomials joined smoothly.
- **Linear spline:** connect points with straight segments (continuous, not smooth).
- **Cubic spline:** cubic on each interval, matching value, first, and second derivatives at interior knots. Smooth (`C²`) and avoids Runge oscillation — the practical default for smooth interpolation.

### 4.6 MATLAB Syntax
```matlab
yi = interp1(x, y, xi, 'linear');   % also 'spline', 'pchip', 'nearest'
yi = spline(x, y, xi);              % cubic spline
p  = polyfit(x, y, n);              % degree-n polynomial fit (exact if n = #pts-1)
yi = polyval(p, xi);                % evaluate polynomial p at xi
```

**Pitfalls:** confusing interpolation (passes *through* points) with regression (best *fit*, may miss points); using too high a degree (Runge); extrapolating outside the data range.

---

## 5. Curve Fitting — Least-Squares Regression

**Goal:** find a function that **best fits** noisy data — does *not* pass through every point. Minimizes the sum of squared residuals `S = Σ(yᵢ − ŷᵢ)²`.

### 5.1 Linear Least Squares (line `y = a₀ + a₁x`)
Normal equations give:
```
a₁ = [nΣxᵢyᵢ − ΣxᵢΣyᵢ] / [nΣxᵢ² − (Σxᵢ)²]
a₀ = ȳ − a₁ x̄
```

### 5.2 Polynomial & General Linear Least Squares
For `y = a₀ + a₁x + ... + aₘxᵐ`, form the design matrix `Z`; solve the **normal equations** `(ZᵀZ)a = Zᵀy`. (MATLAB's `polyfit`/`\` do this stably via QR.)

### 5.3 Goodness of Fit
- **Sum of squared residuals** `S_r = Σ(yᵢ − ŷᵢ)²`.
- **Total sum of squares** `S_t = Σ(yᵢ − ȳ)²`.
- **Coefficient of determination** `R² = 1 − S_r/S_t` — fraction of variance explained (`0 ≤ R² ≤ 1`, closer to 1 = better fit).
- **Standard error of the estimate** `s = √(S_r/(n − (m+1)))`.

### 5.4 Linearizing Nonlinear Models
| Model | Linearized form | Plot |
|---|---|---|
| `y = a e^(bx)` | `ln y = ln a + b x` | semilog-y |
| `y = a x^b` | `ln y = ln a + b ln x` | log-log |
| `y = a x/(b+x)` (saturation) | `1/y = 1/a + (b/a)(1/x)` | `1/y` vs `1/x` |

Fit the linear form, then transform coefficients back.

### 5.5 MATLAB Syntax
```matlab
p = polyfit(x, y, 1);          % linear fit; p = [slope, intercept]
yfit = polyval(p, x);
% R^2:
Sr = sum((y - yfit).^2);  St = sum((y - mean(y)).^2);  R2 = 1 - Sr/St;
% nonlinear least squares:
mdl = lsqcurvefit(@(b,x) b(1)*exp(b(2)*x), b0, x, y);
```

**Pitfalls:** over-fitting (high-degree polynomial chases noise — bad `R²` interpretation); linearization distorts the error weighting, so transformed-fit coefficients differ slightly from a true nonlinear fit; reporting `R²` without checking a residual plot.

---

## 6. Numerical Differentiation

Approximate derivatives from discrete data or hard-to-differentiate functions, using Taylor-series-derived finite differences. Step size `h`.

### 6.1 First-Derivative Formulas
| Formula | Expression | Truncation error |
|---|---|---|
| Forward difference | `f'(x) ≈ (f(x+h) − f(x))/h` | `O(h)` |
| Backward difference | `f'(x) ≈ (f(x) − f(x−h))/h` | `O(h)` |
| **Central difference** | `f'(x) ≈ (f(x+h) − f(x−h))/(2h)` | `O(h²)` — most accurate |

### 6.2 Second-Derivative (central)
```
f''(x) ≈ (f(x+h) − 2f(x) + f(x−h)) / h²        truncation error O(h²)
```

### 6.3 The Step-Size Trade-off
Total error = **truncation error** (decreases as `h → 0`) + **round-off error** (increases as `h → 0`, because of cancellation in the numerator). There is an **optimal `h`** — too small is as bad as too large. Differentiation **amplifies noise**; for noisy data, smooth first or fit a curve and differentiate that.

### 6.4 MATLAB Syntax
```matlab
dydx = diff(y) ./ diff(x);     % forward differences; result is one element shorter
dydx = gradient(y, x);         % central differences interior, one-sided at ends; same length
```

---

## 7. Numerical Integration (Quadrature)

Approximate `∫ₐᵇ f(x) dx`. Newton–Cotes rules fit a polynomial to `f` on subintervals and integrate that.

### 7.1 Trapezoidal Rule
Approximates `f` by straight segments.
- **Single:** `∫ₐᵇ f dx ≈ (h/2)[f(a) + f(b)]`, `h = b−a`.
- **Composite (n subintervals, `h = (b−a)/n`):**
```
∫ₐᵇ f dx ≈ (h/2)[f(x₀) + 2f(x₁) + 2f(x₂) + ... + 2f(x_{n−1}) + f(xₙ)]
```
- **Error:** `O(h²)`; exact for linear `f`.

### 7.2 Simpson's 1/3 Rule
Approximates `f` by parabolas — needs an **even** number of subintervals.
- **Single (2 subintervals):** `∫ ≈ (h/3)[f(x₀) + 4f(x₁) + f(x₂)]`.
- **Composite:**
```
∫ₐᵇ f dx ≈ (h/3)[f(x₀) + 4f(x₁) + 2f(x₂) + 4f(x₃) + ... + 4f(x_{n−1}) + f(xₙ)]
           (pattern: 1, 4, 2, 4, 2, ..., 4, 1)
```
- **Error:** `O(h⁴)`; exact for cubics — much more accurate than trapezoidal for smooth functions.

### 7.3 Simpson's 3/8 Rule
Uses cubics over groups of 3 subintervals: `∫ ≈ (3h/8)[f₀ + 3f₁ + 3f₂ + f₃]`. Useful when `n` is odd (combine with 1/3 rule).

### 7.4 Gaussian Quadrature
Instead of equally spaced nodes, choose **both** the nodes and weights optimally: `∫ ≈ Σ wᵢ f(xᵢ)`. An `n`-point Gauss rule integrates polynomials up to degree `2n−1` exactly — far more accurate per function evaluation than Newton–Cotes. Requires mapping `[a,b]` to `[−1,1]`.

### 7.5 Adaptive Quadrature
Recursively subdivide only where the integrand varies rapidly; concentrate effort where it's needed to hit a tolerance.

### 7.6 MATLAB Syntax
```matlab
I = trapz(x, y);                 % composite trapezoidal on data
I = integral(f, a, b);           % adaptive, high-accuracy, for a function handle
I = integral(f, a, b, 'RelTol', 1e-10);
% Simpson on data: implement the 1,4,2,...,4,1 weight pattern manually
```

**Pitfalls:** Simpson's 1/3 requires an even subinterval count — odd `n` gives wrong results; `trapz` needs data (use `integral` for a formula); singular or oscillatory integrands break standard rules; too-coarse `h` gives large truncation error.

---

## 8. Numerical Solution of ODEs (Initial Value Problems)

For `dy/dx = f(x,y)`, `y(x₀) = y₀`, step size `h`, advancing `x_{n+1} = x_n + h`.

### 8.1 Euler's Method (Forward Euler)
```
y_{n+1} = y_n + h · f(x_n, y_n)
```
- **Idea:** step along the tangent line.
- **Error:** local truncation `O(h²)`, global `O(h)` — **first-order**.
- **Pros:** simplest. **Cons:** low accuracy; can be unstable for stiff problems unless `h` is tiny.

### 8.2 Heun's Method / Improved Euler (RK2)
Predictor–corrector — average the slope at the start and the predicted end:
```
predictor:  y* = y_n + h·f(x_n, y_n)
corrector:  y_{n+1} = y_n + (h/2)·[ f(x_n, y_n) + f(x_{n+1}, y*) ]
```
- **Error:** global `O(h²)` — **second-order**.

### 8.3 Midpoint Method (RK2 variant)
```
k₁ = f(x_n, y_n)
k₂ = f(x_n + h/2, y_n + (h/2)k₁)
y_{n+1} = y_n + h·k₂
```

### 8.4 Classical Fourth-Order Runge–Kutta (RK4) — the workhorse
```
k₁ = f(x_n,        y_n)
k₂ = f(x_n + h/2,  y_n + (h/2)k₁)
k₃ = f(x_n + h/2,  y_n + (h/2)k₂)
k₄ = f(x_n + h,    y_n + h·k₃)
y_{n+1} = y_n + (h/6)·(k₁ + 2k₂ + 2k₃ + k₄)
```
- **Error:** local `O(h⁵)`, global `O(h⁴)` — **fourth-order**. Excellent accuracy-per-step; the standard choice for non-stiff problems.

### 8.5 Systems of ODEs & Higher-Order ODEs
Convert any `n`th-order ODE to a **first-order system** by introducing variables for the lower derivatives. Example: `y'' + 3y' + 2y = 0` becomes, with `y₁ = y, y₂ = y'`:
```
y₁' = y₂
y₂' = −3y₂ − 2y₁
```
Then apply Euler / RK4 to the **vector** `[y₁; y₂]` — every formula above works element-wise on vectors.

### 8.6 Stability & Stiffness
- **Stiff ODE:** has components decaying on vastly different time scales. Explicit methods (Euler, RK4) need impractically small `h` for stability. Use **implicit / adaptive stiff solvers**.
- **Step-size control:** adaptive solvers estimate local error and shrink/grow `h` automatically.

### 8.7 MATLAB ODE Solver Syntax
```matlab
% define the RHS as a function: must return a COLUMN vector for systems
dydt = @(t, y) [ y(2);  -3*y(2) - 2*y(1) ];

tspan = [0 10];          % integration interval (or a vector of output times)
y0    = [1; 0];          % initial conditions (column vector)
[t, Y] = ode45(dydt, tspan, y0);   % t = time column, Y = solution (rows = times, cols = states)

plot(t, Y(:,1));         % plot first state vs. time

opts = odeset('RelTol',1e-8,'AbsTol',1e-10);
[t,Y] = ode45(dydt, tspan, y0, opts);
```

| Solver | Use case |
|---|---|
| `ode45` | non-stiff, general-purpose default (adaptive RK4/5, Dormand–Prince) |
| `ode23` | non-stiff, lower accuracy / crude tolerances |
| `ode113` | non-stiff, smooth problems, stringent tolerances |
| `ode15s` | **stiff** problems (variable-order) |
| `ode23s` | stiff, crude tolerances |

**Pitfalls:** the RHS function must return a **column** vector for systems; mixing up the order of `(t,y)` arguments; using `ode45` on a stiff problem (it crawls — switch to `ode15s`); passing `y0` as a row vector; expecting fixed time steps from `ode45` (it's adaptive — pass a time vector as `tspan` if you need specific output points).

---

## 9. Cross-Cutting Algorithm Selection Guide

| Task | First choice | Notes |
|---|---|---|
| One root, have `f'` | Newton–Raphson | quadratic; needs good guess |
| One root, no `f'` | Secant or `fzero` | `fzero` is robust |
| Guaranteed root in a bracket | Bisection | slow but certain |
| Solve `Ax = b` | `A\b` (LU under the hood) | never `inv(A)*b` |
| Large sparse `Ax = b` | Gauss–Seidel | needs diagonal dominance |
| Pass exactly through data | spline / `interp1('spline')` | avoids Runge |
| Best fit to noisy data | `polyfit` / least squares | check `R²` and residuals |
| Derivative from data | `gradient` (central) | watch noise amplification |
| Integral of data | `trapz` | |
| Integral of a formula | `integral` (adaptive) | high accuracy |
| Non-stiff ODE/IVP | `ode45` | convert higher-order to a system first |
| Stiff ODE/IVP | `ode15s` | |

### Universal Pitfalls
- **Forgetting the dot** (`.* ./ .^`) in MATLAB vectorized formulas.
- **No `max_iter` cap** — iterative methods can loop forever.
- **Step size:** too large → truncation error; too small → round-off error (especially in differentiation).
- **Confusing interpolation with regression.**
- **Ignoring conditioning/stiffness** — a "wrong answer" is often an ill-conditioned problem or wrong solver, not a bug.
- **Trusting output without a sanity check** — plot it, check units, check limiting cases.

---

## Open-source sources used

- **Kong, Siauw & Bayen. _Python Programming and Numerical Methods: A Guide for Engineers and Scientists_ (UC Berkeley).** Open-access — https://pythonnumericalmethods.studentorg.berkeley.edu/ — Source for chapter scope and algorithm structure: root finding (bisection, Newton–Raphson), linear-algebra/systems, interpolation (linear, Lagrange, Newton, cubic spline), least-squares regression, numerical differentiation (finite differences), numerical integration (Riemann, trapezoid, Simpson), and ODE solvers (Euler, Runge–Kutta, shooting, finite difference).
- **Young & Mohlenkamp. _Introduction to Numerical Methods and MATLAB Programming for Engineers_ (Ohio University).** Open-access — http://www.ohiouniversityfaculty.com/youngt/IntNumMeth/book.pdf — Source for MATLAB programming constructs, error analysis, root-finding convergence properties, Gaussian elimination / LU / iterative linear solvers, quadrature rules and error orders, and Euler/RK MATLAB implementation patterns.
- **LibreTexts _Numerical Methods / Numerical Analysis_ Bookshelf.** https://math.libretexts.org/Bookshelves/Numerical_Analysis — Source for finite-difference error orders, Newton–Cotes derivations, Gaussian quadrature, conditioning/stability, and stiffness.
- **Holistic Numerical Methods (Autar Kaw, University of South Florida).** Open courseware — https://nm.mathforcollege.com/ — Source for step-by-step algorithm procedures, divided-difference interpolation, composite integration weight patterns, and the round-off/truncation step-size trade-off.
- **MIT OpenCourseWare — Numerical methods coursework (e.g., 18.330, 2.993J).** https://ocw.mit.edu/ — Source for convergence-order framing, stability analysis, and adaptive/stiff ODE solver context.
- **MathWorks MATLAB Documentation** (vendor open documentation) — https://www.mathworks.com/help/matlab/ — Source for verified syntax of `fzero`, `roots`, `polyfit`, `polyval`, `interp1`, `spline`, `trapz`, `integral`, `lu`, the backslash operator, and the `ode45`/`ode15s` solver family.
