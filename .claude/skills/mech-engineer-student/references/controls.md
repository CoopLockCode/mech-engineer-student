# Dynamic Systems & Control Theory Reference

> PhD-level study companion for ME 3501 — Dynamic Systems & Control Theory.
> Covers system modeling (mechanical, electrical, fluid, thermal), transfer functions and
> state-space, Laplace-domain analysis, time-domain response (first/second order), block
> diagrams, stability (Routh-Hurwitz), root locus, frequency response (Bode, Nyquist), and
> PID control design & tuning.
> Plain-text math: `s` = Laplace variable, `*` = multiply, `^` = power, `w` = omega,
> `w_n` = natural frequency, `zeta` = damping ratio, `j` = imaginary unit.

---

## 1. System Modeling

### 1.1 Goal

Produce a mathematical model — an ODE, transfer function, or state-space form — that captures
the input-output dynamics. Modeling assumptions (linearity, lumped parameters, time-invariance)
must be stated; control theory in this course assumes **LTI** (linear, time-invariant) systems.

### 1.2 Mechanical Translational Elements

| Element | Constitutive law (force) |
|---|---|
| Mass m | f = m·x_ddot |
| Spring k | f = k·x |
| Damper b | f = b·x_dot |

Procedure: free-body diagram each mass, apply Newton's 2nd law (sum F = m·a), one ODE per mass.

### 1.3 Mechanical Rotational Elements

| Element | Constitutive law (torque) |
|---|---|
| Inertia J | T = J·theta_ddot |
| Torsional spring K | T = K·theta |
| Rotational damper B | T = B·theta_dot |

### 1.4 Electrical Elements

| Element | v–i relation | Impedance (s-domain) |
|---|---|---|
| Resistor R | v = R·i | R |
| Inductor L | v = L·di/dt | L·s |
| Capacitor C | i = C·dv/dt | 1/(C·s) |

Use KVL (sum of voltages around a loop = 0) and KCL (sum of currents at a node = 0).
**Mechanical-electrical analogy** (force-voltage): m↔L, b↔R, k↔1/C, force↔voltage, velocity↔current.

### 1.5 Fluid Systems

For a tank with cross-section A, liquid height h, inflow q_in, outflow through resistance R:
- **Capacitance** C = A/(rho·g) (or simply A for height models); stores volume.
- **Resistance** R relates flow to pressure/head drop: q = (delta_P)/R (laminar/linearized).
- Mass balance: C·dh/dt = q_in - q_out, with q_out = h/R (linearized valve).
  → R·C·dh/dt + h = R·q_in  (first-order, time constant tau = R·C).

### 1.6 Thermal Systems

- **Thermal capacitance** C_t = m·c_p (J/K); stores heat.
- **Thermal resistance** R_t (K/W); q = (delta_T)/R_t.
- Energy balance: C_t·dT/dt = q_in - (T - T_ambient)/R_t.
  → R_t·C_t·dT/dt + T = T_ambient + R_t·q_in  (first-order, tau = R_t·C_t).

### 1.7 Linearization

Nonlinear element f(x) is linearized about an operating point x_0:
  f(x) ≈ f(x_0) + (df/dx)|_{x_0}·(x - x_0)
Work in **deviation variables** (delta_x = x - x_0). All control design here is on the
linearized model. Common nonlinearities: sqrt in orifice flow, x^4 in radiation, sin in
pendulum, products in bilinear terms.

### 1.8 Pitfalls

- Mixing absolute and deviation variables — pick one and be consistent.
- Forgetting a state (each independent energy storage = one state / one order).
- Sign conventions on damper/spring forces: spring force opposes displacement, damper opposes velocity.

---

## 2. The Laplace Transform

### 2.1 Definition

  L{f(t)} = F(s) = integral from 0 to infinity of f(t)·e^(-s·t) dt

The Laplace transform converts linear ODEs (with constant coefficients) into algebraic equations
in s. Solve algebraically, then invert.

### 2.2 Key Properties

| Property | Time domain | s-domain |
|---|---|---|
| Linearity | a·f(t) + b·g(t) | a·F(s) + b·G(s) |
| First derivative | f'(t) | s·F(s) - f(0) |
| Second derivative | f''(t) | s^2·F(s) - s·f(0) - f'(0) |
| Integration | integral of f from 0 to t | F(s)/s |
| Time delay | f(t - a)·u(t - a) | e^(-a·s)·F(s) |
| s-shift | e^(-a·t)·f(t) | F(s + a) |
| Time scaling | f(a·t) | (1/a)·F(s/a) |
| Multiply by t | t·f(t) | -dF/ds |
| Initial value theorem | f(0+) = lim s→infinity of s·F(s) | — |
| Final value theorem | f(infinity) = lim s→0 of s·F(s) | (only if stable) |
| Convolution | integral f(tau)·g(t-tau) dtau | F(s)·G(s) |

### 2.3 Laplace Transform Pairs Table

| f(t), t >= 0 | F(s) |
|---|---|
| delta(t) (unit impulse) | 1 |
| u(t) (unit step) | 1/s |
| t (unit ramp) | 1/s^2 |
| t^n / n! | 1/s^(n+1) |
| e^(-a·t) | 1/(s + a) |
| t·e^(-a·t) | 1/(s + a)^2 |
| 1 - e^(-a·t) | a/(s·(s + a)) |
| sin(w·t) | w/(s^2 + w^2) |
| cos(w·t) | s/(s^2 + w^2) |
| e^(-a·t)·sin(w·t) | w/((s + a)^2 + w^2) |
| e^(-a·t)·cos(w·t) | (s + a)/((s + a)^2 + w^2) |
| (1/w_n^2)(1 - cos(w_n·t)) | 1/(s·(s^2 + w_n^2)) |

### 2.4 Inverse Laplace by Partial Fractions — Procedure

1. Ensure F(s) is a **proper** rational function (degree of numerator < denominator). If not,
   do polynomial long division first.
2. Factor the denominator into real linear and irreducible quadratic factors.
3. Write the partial-fraction expansion with unknown constants:
   - Distinct real pole p: term A/(s - p), A = (s - p)·F(s)|_{s=p}  (residue / cover-up method).
   - Repeated pole p of order r: terms A_1/(s-p) + A_2/(s-p)^2 + ... + A_r/(s-p)^r.
     A_r = (s-p)^r·F(s)|_{s=p}; lower A_k via successive differentiation.
   - Complex-conjugate pair: keep a (B·s + C)/(s^2 + b·s + c) term, complete the square,
     match to e^(-a·t)·sin/cos pairs.
4. Invert each term using the transform table.
5. Sum the time-domain pieces.

### 2.5 Pitfalls

- Final value theorem is **invalid** if the system is unstable or marginally stable (poles on
  or right of the jw-axis, except a single pole at origin) — applying it then gives nonsense.
- Don't forget initial-condition terms when transforming derivatives (they vanish only for the
  transfer-function definition, which assumes zero ICs).
- Improper F(s) must be reduced by long division before partial fractions.

---

## 3. Transfer Functions

### 3.1 Definition

For an LTI system with zero initial conditions:
  **G(s) = Y(s) / U(s) = (output transform) / (input transform)**

Derived by Laplace-transforming the ODE (zero ICs) and solving for Y(s)/U(s).

Example — mass-spring-damper m·y_ddot + b·y_dot + k·y = f(t):
  (m·s^2 + b·s + k)·Y(s) = F(s)
  **G(s) = 1 / (m·s^2 + b·s + k)**

### 3.2 Poles and Zeros

  G(s) = K·(s - z_1)(s - z_2)... / ((s - p_1)(s - p_2)...)

- **Zeros** z_i: roots of the numerator; frequencies at which G(s) = 0.
- **Poles** p_i: roots of the denominator (= roots of the characteristic equation); they
  determine **stability** and the **natural modes** of the response.
- The characteristic equation is **denominator = 0**.

### 3.3 Pole Locations and Response Modes

| Pole location | Time-domain mode |
|---|---|
| Real, negative (-a) | Decaying exponential e^(-a·t) |
| Real, positive (+a) | Growing exponential — UNSTABLE |
| At origin (0) | Constant / integrator |
| Complex pair -sigma ± jw | Decaying oscillation e^(-sigma·t)·sin(w·t) |
| Pure imaginary ±jw | Sustained oscillation — marginally stable |
| Complex pair +sigma ± jw | Growing oscillation — UNSTABLE |

**Rule:** an LTI system is BIBO-stable iff **all poles lie strictly in the open left-half plane**
(Re(p) < 0).

### 3.4 DC Gain

Steady-state gain for a step input: G(0) = lim s→0 of G(s). (Only meaningful for stable systems.)

---

## 4. State-Space Models

### 4.1 Standard Form

  **x_dot = A·x + B·u**   (state equation)
  **y = C·x + D·u**       (output equation)

- x = state vector (n×1), n = system order
- u = input vector, y = output vector
- A = system matrix (n×n), B = input matrix, C = output matrix, D = feedthrough matrix

### 4.2 Building State-Space from an ODE

Choose states as physically meaningful energy-storage variables (position, velocity, current,
voltage, height, temperature). For an n-th order ODE, define x_1 = y, x_2 = y_dot, ...,
x_n = y^(n-1); the last state derivative comes from solving the ODE for y^(n).
This produces the **controllable canonical form**.

### 4.3 State-Space to Transfer Function

  **G(s) = C·(s·I - A)^(-1)·B + D**

The **poles of G(s) are the eigenvalues of A** (roots of det(s·I - A) = 0). System is stable iff
all eigenvalues of A have negative real parts.

### 4.4 Controllability and Observability

- **Controllability matrix**: P = [B, A·B, A^2·B, ..., A^(n-1)·B]. System is controllable iff
  rank(P) = n (every state can be driven by the input).
- **Observability matrix**: Q = [C; C·A; C·A^2; ...; C·A^(n-1)]. System is observable iff
  rank(Q) = n (every state can be inferred from the output).
- Controllability → can place all closed-loop poles via full-state feedback u = -K·x.
- Observability → can build a state estimator (observer).

### 4.5 Pitfalls

- State choice is not unique, but the eigenvalues of A (the poles) are invariant.
- D is usually 0 for physical systems (no direct input-to-output feedthrough).
- Transfer function loses information about uncontrollable/unobservable modes (pole-zero cancellations).

---

## 5. Time-Domain Response

### 5.1 First-Order Systems

Standard form: **G(s) = K / (tau·s + 1)**
- K = DC gain, tau = time constant.
- **Step response** (input magnitude A): y(t) = A·K·(1 - e^(-t/tau))
- **Impulse response**: y(t) = (A·K/tau)·e^(-t/tau)
- Characteristic times:
  - At t = tau: response has reached **63.2%** of final value.
  - At t = 3·tau: ~95%; at t = 4·tau: ~98%; at t = 5·tau: ~99%.
  - **Settling time** (2% criterion): t_s ≈ 4·tau
  - **Rise time** (10%–90%): t_r ≈ 2.2·tau
- Pole at s = -1/tau. Faster response ↔ smaller tau ↔ pole further left.

### 5.2 Second-Order Systems — Prototype

Standard form: **G(s) = (K·w_n^2) / (s^2 + 2·zeta·w_n·s + w_n^2)**
- w_n = undamped natural frequency, zeta = damping ratio.
- Characteristic equation: s^2 + 2·zeta·w_n·s + w_n^2 = 0
- Poles: **s = -zeta·w_n ± w_n·sqrt(zeta^2 - 1)**

### 5.3 Damping Cases

| zeta | Pole type | Behavior |
|---|---|---|
| zeta = 0 | ±j·w_n | Undamped — sustained oscillation |
| 0 < zeta < 1 | -zeta·w_n ± j·w_d | Underdamped — decaying oscillation |
| zeta = 1 | -w_n (double real) | Critically damped — fastest no-overshoot |
| zeta > 1 | two distinct real < 0 | Overdamped — sluggish, no overshoot |

**Damped natural frequency**: w_d = w_n·sqrt(1 - zeta^2)

### 5.4 Underdamped Step Response

  y(t) = A·K·[1 - (e^(-zeta·w_n·t)/sqrt(1 - zeta^2))·sin(w_d·t + phi)]
  where phi = acos(zeta)  (equivalently atan(sqrt(1-zeta^2)/zeta))

The pole's polar form: distance from origin = w_n, angle from negative real axis = acos(zeta).
So **zeta = cos(theta)**, where theta is the pole angle measured from the negative real axis.

### 5.5 Second-Order Step-Response Specifications (underdamped)

| Spec | Formula | Notes |
|---|---|---|
| Rise time t_r | ≈ (pi - phi)/w_d or approx (1.8/w_n) | 0→100% (or 10–90% approx) |
| Peak time t_p | t_p = pi / w_d | time of first peak |
| Percent overshoot %OS | %OS = 100·exp(-zeta·pi/sqrt(1-zeta^2)) | depends ONLY on zeta |
| Settling time t_s (2%) | t_s ≈ 4 / (zeta·w_n) | 4 time constants |
| Settling time t_s (5%) | t_s ≈ 3 / (zeta·w_n) | |
| Damped period | T_d = 2·pi / w_d | |
| Number of oscillations to settle | ≈ t_s / T_d | |

**Inverse relation (design)**: given desired %OS,
  zeta = -ln(%OS/100) / sqrt(pi^2 + ln^2(%OS/100))

Worked-pattern check (Iqbal prototype): G(s) = 25/(s^2 + 6s + 25) → poles -3 ± j4 →
w_n = 5, zeta = 0.6 → t_p ≈ 0.785 s, %OS ≈ 9.5%, t_s(2%) ≈ 1.33 s. Good design target:
%OS ≤ 10% needs zeta ≥ 0.6.

### 5.6 Pole-Location Geometry (s-plane design regions)

- **zeta = const** → radial lines from origin (constant overshoot).
- **w_n = const** → circles centered at origin (constant speed of oscillation).
- **zeta·w_n = const** (= sigma) → vertical lines (constant settling time / decay rate).
- **w_d = const** → horizontal lines.
Design specs (%OS, t_s, t_p) carve out an allowable region in the s-plane for the dominant poles.

### 5.7 Dominant Poles & Higher-Order Reduction

A higher-order system is approximated by its **dominant poles** — the pair closest to the
jw-axis (slowest). Rule of thumb: poles ≥ 5× further left than the dominant pair are negligible.
A nearby zero can significantly increase overshoot; a nearby pole slows the response.

### 5.8 Steady-State Error & System Type

For a unity-feedback system with open-loop G(s), **system type** = number of pure integrators
(poles at s = 0) in G(s). Static error constants:
- Position constant: K_p = lim s→0 G(s); step error e_ss = 1/(1 + K_p)
- Velocity constant: K_v = lim s→0 s·G(s); ramp error e_ss = 1/K_v
- Acceleration constant: K_a = lim s→0 s^2·G(s); parabola error e_ss = 1/K_a

| System type | Step e_ss | Ramp e_ss | Parabola e_ss |
|---|---|---|---|
| Type 0 | 1/(1+K_p) finite | infinity | infinity |
| Type 1 | 0 | 1/K_v finite | infinity |
| Type 2 | 0 | 0 | 1/K_a finite |

### 5.9 Pitfalls

- %OS depends **only** on zeta, not w_n — a very common exam trap.
- t_s and t_p use w_n and w_d respectively — don't swap them.
- Final value theorem for e_ss only valid if the closed-loop system is stable.
- "Dominant pole" approximation fails if a zero sits near the dominant poles.

---

## 6. Block Diagrams

### 6.1 Reduction Rules

| Configuration | Equivalent |
|---|---|
| Series (cascade) G_1, G_2 | G_1·G_2 |
| Parallel G_1, G_2 | G_1 + G_2 |
| Negative feedback: forward G, feedback H | G / (1 + G·H) |
| Positive feedback: forward G, feedback H | G / (1 - G·H) |
| Unity feedback | G / (1 + G) |

### 6.2 Closed-Loop Transfer Function

For forward path G(s), feedback path H(s):
  **T(s) = Y(s)/R(s) = G(s) / (1 + G(s)·H(s))**
- **Open-loop transfer function** = G(s)·H(s) (the "loop gain").
- **Characteristic equation**: 1 + G(s)·H(s) = 0 — its roots are the closed-loop poles.

### 6.3 Moving Summing Junctions & Pickoff Points

- Move a pickoff point past a block G: add a 1/G block on the branch.
- Move a pickoff point before a block G: add a G block on the branch.
- Move a summing junction past a block G: multiply the moved input by G.
- Move a summing junction before a block G: divide the moved input by G.

### 6.4 Mason's Gain Formula (for complex diagrams / signal-flow graphs)

  T = (1/Delta)·sum over k of (P_k·Delta_k)
- P_k = gain of the k-th forward path
- Delta = 1 - (sum of all loop gains) + (sum of products of 2 non-touching loops) - ...
- Delta_k = Delta computed with all loops touching path k removed

### 6.5 Pitfalls

- The sign in the denominator: negative feedback → (1 + GH), positive feedback → (1 - GH).
- Always reduce inner loops first.
- Disturbance inputs need their own transfer function Y/D — don't reuse Y/R.

---

## 7. Stability — Routh-Hurwitz Criterion

### 7.1 Necessary Condition

For characteristic polynomial Delta(s) = a_n·s^n + a_{n-1}·s^(n-1) + ... + a_1·s + a_0:
**all coefficients must be present and have the same sign** (conventionally all positive).
If any coefficient is zero or has opposite sign → system is **not stable** (stop here).
This is necessary but NOT sufficient for n >= 3.

### 7.2 Routh Array — Construction Procedure

For Delta(s) = s^n + a_1·s^(n-1) + a_2·s^(n-2) + ... :

1. **First two rows** — coefficients in alternating fashion:
   ```
   s^n   :  1    a_2   a_4   a_6 ...
   s^(n-1): a_1   a_3   a_5   ... 
   ```
2. **Subsequent rows** — each entry is a 2×2 determinant divided by the pivot of the row above:
   ```
   s^(n-2): b_1   b_2   b_3 ...
   ```
   b_1 = (a_1·a_2 - 1·a_3) / a_1
   b_2 = (a_1·a_4 - 1·a_5) / a_1   ... and so on.
   Then with b's as the new pivot row:
   c_1 = (b_1·a_3 - a_1·b_2) / b_1   ... continue down to the s^0 row.
3. Continue until you have n+1 rows (s^n down to s^0).

### 7.3 Stability Determination

**The number of closed-loop poles in the right-half plane = the number of sign changes in the
first column of the Routh array.** Zero sign changes → all poles in LHP → **stable**.

### 7.4 Special Case 1 — Zero in the First Column (rest of row nonzero)

Replace the zero with a small positive number **epsilon**, continue the array, then take the
limit epsilon → 0+. Count sign changes as usual. (A sign change through epsilon indicates RHP poles.)

### 7.5 Special Case 2 — Entire Row of Zeros

Indicates symmetrically placed roots (e.g., a pair ±jw, or ±sigma, or quadruplets) — often
**marginal stability** or roots on the jw-axis.
Procedure:
1. Form the **auxiliary polynomial** A(s) from the row **above** the zero row (coefficients are
   that row's entries; powers descend by 2).
2. Differentiate A(s) with respect to s: dA/ds.
3. Replace the zero row with the coefficients of dA/ds, then continue the array.
4. The roots of the auxiliary polynomial are themselves roots of the characteristic equation —
   solve A(s) = 0 to find the jw-axis (or symmetric) roots.

### 7.6 Low-Order Shortcuts

- **2nd order** s^2 + a_1·s + a_0: stable iff a_1 > 0 AND a_0 > 0.
- **3rd order** s^3 + a_1·s^2 + a_2·s + a_3: stable iff a_1, a_2, a_3 > 0 **AND a_1·a_2 > a_3**.
- **4th order** s^4 + a_1·s^3 + a_2·s^2 + a_3·s + a_4: all coeffs > 0 AND
  a_1·a_2·a_3 > a_3^2 + a_1^2·a_4.

### 7.7 Finding the Critical Gain (range of K for stability)

When the characteristic equation contains a gain K, build the Routh array symbolically in K.
Each first-column entry must be > 0 → a set of inequalities on K → the **stable range of K**.
The boundary value (where an entry = 0) is the **marginal stability gain** K_crit. At K_crit, a
row of zeros appears; the auxiliary polynomial gives the **frequency of oscillation** at that gain.

Worked pattern (Iqbal): Delta(s,K) = s^3 + 3s^2 + 2s + K. Stable iff K > 0 and (3·2 - K) > 0
→ **0 < K < 6**; K_crit = 6, and the auxiliary polynomial 3s^2 + 6 = 0 → s = ±j·sqrt(2) →
oscillation frequency w = sqrt(2) rad/s at K = 6.

### 7.8 Pitfalls

- Routh-Hurwitz tells you HOW MANY RHP poles, not WHERE they are.
- A missing coefficient (e.g., no s^1 term) means coefficient = 0 → already not stable
  (or marginal) — but still build the array to count.
- Don't forget: the necessary condition (all coeffs same sign) must be checked first.
- The auxiliary polynomial always has **even** powers only.

---

## 8. Root Locus

### 8.1 Definition

The **root locus** is the locus of closed-loop pole locations as a parameter (usually the gain
K >= 0) varies from 0 to infinity. The open-loop transfer function is K·G(s)·H(s) with
G·H having n poles and m finite zeros.

### 8.2 The Two Conditions

A point s_1 is on the root locus iff:
- **Angle condition** (defines the locus): sum of angles from zeros − sum of angles from poles
  = ±180°·(2k+1) for K > 0.
  ```
  sum(angle(s_1 - z_i)) - sum(angle(s_1 - p_i)) = ±180° (odd multiples)
  ```
- **Magnitude condition** (gives K at that point):
  ```
  K = (product of |s_1 - p_i|) / (product of |s_1 - z_i|)
    = (product of distances from s_1 to poles) / (product of distances to zeros)
  ```

### 8.3 Construction Rules — Step-by-Step

1. **Plot** the open-loop poles (×) and zeros (○) on the s-plane.
2. **Number of branches** = n (number of open-loop poles). Each branch starts (K=0) at a pole.
3. **Termination**: m branches end (K→∞) at the m finite zeros; the remaining **n − m** branches
   go to infinity along asymptotes.
4. **Symmetry**: the locus is symmetric about the real axis (complex poles come in conjugate pairs).
5. **Real-axis segments**: a point on the real axis is on the locus iff there is an **odd number**
   of real poles + real zeros to its **right**.
6. **Asymptotes** (the n − m branches going to infinity):
   - **Angles**: phi_a = (2k+1)·180° / (n − m), for k = 0, 1, ..., n−m−1.
   - **Centroid** (where asymptotes radiate from, on the real axis):
     sigma_a = (sum of poles − sum of zeros) / (n − m).
7. **Breakaway / break-in points** (where branches leave or join the real axis): solutions of
   dK/ds = 0, equivalently
   ```
   sum 1/(s - p_i) = sum 1/(s - z_i)
   ```
   Keep only roots that lie on a valid real-axis segment.
8. **Angle of departure** from a complex pole p:
   theta_dep = 180° + (sum of angles from zeros to p) − (sum of angles from other poles to p).
   **Angle of arrival** at a complex zero z:
   theta_arr = 180° − (sum of angles from other zeros to z) + (sum of angles from poles to z).
9. **jw-axis crossings**: substitute s = jw into the characteristic equation 1 + K·G·H = 0,
   set real and imaginary parts to zero, solve for w and K. (Equivalent to the Routh marginal-gain
   computation.) This gives the gain at which the system becomes unstable.

### 8.4 Reading the Root Locus for Design

- Pick a desired dominant-pole location (from %OS → zeta line, t_s → vertical line).
- Find where that location intersects the locus.
- Use the magnitude condition to read off the required gain K.
- Check that the other (non-dominant) closed-loop poles are far enough left.

### 8.5 Compensators (shaping the locus)

- **Lead compensator** C(s) = K·(s + z)/(s + p), z < p: adds positive angle, pulls the locus
  **left** → faster response, more stable, improves transient.
- **Lag compensator** C(s) = K·(s + z)/(s + p), z > p (both near origin): boosts low-frequency
  gain → reduces steady-state error with little effect on transient.
- **Lag-lead**: combines both.
- **PID** can be viewed as adding a pole at the origin (integral) and zeros (proportional + derivative).

### 8.6 Pitfalls

- Real-axis rule counts poles/zeros to the **right**, and counts **odd** total.
- Asymptote angles use (2k+1)·180°/(n−m) — don't forget the odd-multiple structure.
- Breakaway points: solve dK/ds = 0 but **discard** solutions not on a valid locus segment.
- Branches **start** at poles, **end** at zeros — never the reverse.
- A zero at infinity counts toward asymptote behavior, not toward finite-zero termination.

---

## 9. Frequency Response

### 9.1 Concept

For a stable LTI system, a sinusoidal input of frequency w produces a sinusoidal steady-state
output of the same frequency, scaled by |G(jw)| and phase-shifted by angle(G(jw)).
The **frequency response** is G(jw): substitute s = jw into G(s).

### 9.2 Bode Plots

Two plots vs. log10(w):
- **Magnitude**: 20·log10|G(jw)| in decibels (dB).
- **Phase**: angle(G(jw)) in degrees.

**Asymptotic (straight-line) rules** — each factor contributes additively:
| Factor | Magnitude slope | Phase contribution |
|---|---|---|
| Constant K | 20·log10|K| (flat) | 0° (or 180° if K<0) |
| Pole at origin 1/s | −20 dB/decade | −90° |
| Zero at origin s | +20 dB/decade | +90° |
| Real pole 1/(1 + s/w_c) | 0 then −20 dB/dec after w_c | 0° → −90° (−45° at w_c) |
| Real zero (1 + s/w_c) | 0 then +20 dB/dec after w_c | 0° → +90° (+45° at w_c) |
| Complex pole pair | 0 then −40 dB/dec after w_n | 0° → −180° (−90° at w_n) |

Corner (break) frequency = w_c. Underdamped complex poles produce a resonant **peak** of
height ≈ 1/(2·zeta) (in linear terms) near w_n if zeta < 0.707.

### 9.3 Stability Margins (from Bode plot of open-loop G·H)

- **Gain crossover frequency** w_gc: where |G·H| = 0 dB (magnitude = 1).
- **Phase crossover frequency** w_pc: where phase = −180°.
- **Phase margin** PM = 180° + angle(G·H(jw_gc)) — how much extra phase lag before instability.
- **Gain margin** GM = −20·log10|G·H(jw_pc)| dB — how much extra gain before instability.
- **Stable** (for typical minimum-phase systems): PM > 0 AND GM > 0.
- Rule of thumb: PM ≈ 100·zeta (for PM up to ~70°); good designs target PM = 45°–60°.

### 9.4 Nyquist Criterion

Plot G(jw)·H(jw) in the complex plane as w goes from −∞ to +∞ (the **Nyquist contour**).
**Nyquist stability criterion**:
  Z = N + P
- Z = number of closed-loop poles in the RHP (want Z = 0 for stability)
- P = number of open-loop poles of G·H in the RHP
- N = number of **clockwise** encirclements of the critical point **−1 + j0** by the G·H plot
For an open-loop-stable system (P = 0): stable iff the plot does **not encircle −1**.
The closeness of the plot to −1 quantifies the gain and phase margins.

### 9.5 Pitfalls

- Bode magnitude is in dB: 20·log10, not 10·log10 (that's power).
- A "decade" is ×10 in frequency; an "octave" is ×2.
- Phase margin is measured at the **gain** crossover; gain margin at the **phase** crossover —
  don't swap them.
- Nyquist counts encirclements of −1, not of the origin.
- Non-minimum-phase systems (RHP zeros) have extra phase lag — Bode magnitude alone can mislead.

---

## 10. PID Control Design & Tuning

### 10.1 The PID Controller

  **u(t) = K_p·e(t) + K_i·integral(e dt) + K_d·de/dt**
  Transfer function: **C(s) = K_p + K_i/s + K_d·s = K_p·(1 + 1/(T_i·s) + T_d·s)**
  where T_i = K_p/K_i (integral time), T_d = K_d/K_p (derivative time).

### 10.2 Role of Each Term

| Term | Effect on rise time | Overshoot | Settling time | Steady-state error | Stability |
|---|---|---|---|---|---|
| Increase K_p | Decrease | Increase | Small change | Decrease | Degrade |
| Increase K_i | Decrease | Increase | Increase | **Eliminate** | Degrade |
| Increase K_d | Small change | Decrease | Decrease | No effect | Improve (damping) |

- **P**: proportional action; faster but leaves steady-state error (for type-0 plants) and can oscillate.
- **I**: drives steady-state error to zero (adds a pole at origin → raises system type) but
  adds phase lag → can destabilize; risk of **integral windup**.
- **D**: anticipatory; adds damping and phase lead, improves transient — but amplifies
  high-frequency noise; usually filtered: K_d·s/(tau_f·s + 1).

### 10.3 Design Procedure (pole placement / root locus)

1. From specs (%OS → zeta, t_s → sigma) locate the desired dominant closed-loop poles.
2. Use the **angle condition** at the desired pole to find what angle the compensator must add.
3. Choose PID zeros (and the integrator pole) to satisfy the angle condition.
4. Use the **magnitude condition** at the desired pole to set the overall gain.
5. Verify with the full closed-loop response (other poles, actuator limits, robustness).

### 10.4 Ziegler-Nichols Tuning

**Method 1 — Ultimate Gain (closed-loop):**
1. Set K_i = K_d = 0. Increase K_p until the output shows **sustained oscillation**.
2. Record the **ultimate gain** K_u and **ultimate period** P_u.
3. Apply the table:

| Controller | K_p | T_i | T_d |
|---|---|---|---|
| P | 0.5·K_u | — | — |
| PI | 0.45·K_u | P_u/1.2 | — |
| PID | 0.6·K_u | P_u/2 | P_u/8 |

**Method 2 — Reaction Curve (open-loop step test):**
1. Apply a step to the open-loop plant; record the S-shaped response.
2. Extract delay L (dead time) and time constant T from the inflection-point tangent.
3. Apply the reaction-curve table:

| Controller | K_p | T_i | T_d |
|---|---|---|---|
| P | T/L | — | — |
| PI | 0.9·T/L | L/0.3 | — |
| PID | 1.2·T/L | 2·L | 0.5·L |

Ziegler-Nichols gives a starting point — typically ~25% overshoot; manual fine-tuning follows.

### 10.5 Practical Tuning Heuristics

1. Start with P only; increase K_p until response is fast but overshoot is acceptable (~10–20%).
2. Add I to remove steady-state error; increase K_i until error vanishes without excessive
   oscillation. Reduce K_p slightly if needed.
3. Add D to damp overshoot and speed settling; increase K_d until transient is clean. Filter D
   if noise is amplified.
4. Iterate. Watch for actuator saturation and integral windup (use anti-windup clamping).

### 10.6 Pitfalls

- **Integral windup**: when the actuator saturates, the integral term keeps accumulating →
  huge overshoot. Use anti-windup (clamp or back-calculation).
- Pure derivative on the measured output ("derivative kick") spikes on setpoint changes — apply
  D to the measurement, not the error, and always filter it.
- More integral gain is not "more accurate" — it trades stability for error rejection speed.
- Ziegler-Nichols is aggressive; don't treat its output as a final design.
- A faster controller is limited by actuator bandwidth and unmodeled high-frequency dynamics.

---

## 11. Quick-Reference Tables

### 11.1 First- vs. Second-Order Step Response

| Quantity | First order | Second order (underdamped) |
|---|---|---|
| Standard form | K/(tau·s+1) | K·w_n^2/(s^2+2·zeta·w_n·s+w_n^2) |
| Poles | −1/tau | −zeta·w_n ± j·w_d |
| Settling time (2%) | 4·tau | 4/(zeta·w_n) |
| Rise time | 2.2·tau | ≈1.8/w_n |
| Overshoot | none | 100·exp(−zeta·pi/sqrt(1−zeta^2)) |
| Peak time | none | pi/w_d |

### 11.2 Stability Tests Summary

| Method | Domain | Tells you |
|---|---|---|
| Pole locations | s-plane | Exact: all poles Re < 0 → stable |
| Routh-Hurwitz | s-plane (algebraic) | Number of RHP poles; stable gain range |
| Root locus | s-plane (graphical) | Pole paths vs. K; gain for desired poles |
| Bode (PM/GM) | frequency | Relative stability; margins |
| Nyquist | frequency (complex) | Stability via encirclements of −1 |

### 11.3 System Type vs. Steady-State Error (unity feedback)

| Type | # integrators | Step e_ss | Ramp e_ss | Parabola e_ss |
|---|---|---|---|---|
| 0 | 0 | 1/(1+K_p) | ∞ | ∞ |
| 1 | 1 | 0 | 1/K_v | ∞ |
| 2 | 2 | 0 | 0 | 1/K_a |

---

## Open-source sources used

- Kamran Iqbal, *Introduction to Control Systems*, Engineering LibreTexts — Transfer Function Models (Ch. 2), Control System Design Objectives incl. Routh-Hurwitz stability & transient response (Ch. 4), Control System Design with Root Locus (Ch. 5), Design of Sampled-Data Systems (Ch. 7) — `https://eng.libretexts.org/Bookshelves/Industrial_and_Systems_Engineering/Introduction_to_Control_Systems_(Iqbal)`
- R.L. Hallauer, *Introduction to Linear Time-Invariant Dynamic Systems for Students of Engineering*, Engineering LibreTexts — Damped Second Order Systems (Ch. 9), step-response specifications for underdamped systems — `https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Signal_Processing_and_Modeling/Introduction_to_Linear_Time-Invariant_Dynamic_Systems_for_Students_of_Engineering_(Hallauer)`
- *Chemical Process Dynamics and Controls* (Woolf et al.), Engineering LibreTexts — Dynamical Systems Analysis, root locus plots & controller tuning — `https://eng.libretexts.org/Bookshelves/Industrial_and_Systems_Engineering/Chemical_Process_Dynamics_and_Controls_(Woolf)`
- J.G. Roberge, *Operational Amplifiers: Theory and Practice*, Engineering LibreTexts — Stability and root-locus techniques (Ch. 4) — `https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/Operational_Amplifiers:_Theory_and_Practice_(Roberge)`
- MIT OpenCourseWare — Signals and Systems / Feedback Control Systems course materials — `https://ocw.mit.edu/`
