# Machine Dynamics & Vibrations Reference

> PhD-level study companion for ENGR 3125 — Machine Dynamics & Vibrations.
> Covers free/forced vibration of SDOF systems (undamped & damped), harmonic and base
> excitation, transmissibility, rotating unbalance, vibration isolation, multi-DOF systems,
> natural frequencies & mode shapes, continuous systems, and kinematics/dynamics of mechanisms.
> Plain-text math notation: `x_dot` = first time derivative, `x_ddot` = second, `^` = power,
> `sqrt()` = square root, `w_n` = omega_n (natural frequency).

---

## 1. Fundamentals & Modeling

### 1.1 Definitions

- **Vibration**: oscillatory motion of a system about an equilibrium position; an exchange of kinetic and potential (or strain) energy.
- **Degree of freedom (DOF)**: the minimum number of independent coordinates required to fully specify the configuration of a system at any instant.
- **Discrete (lumped) system**: finite number of DOF; described by ODEs.
- **Continuous (distributed) system**: infinite DOF; described by PDEs (e.g., a beam, string, shaft).
- **Free vibration**: motion under initial conditions only, no external force after t = 0.
- **Forced vibration**: motion under a sustained external excitation.
- **Damped vs. undamped**: damped systems dissipate energy (amplitude decays); undamped systems conserve it (idealization).
- **Linear vs. nonlinear**: linear systems obey superposition; coefficients m, c, k are constants.
- **Deterministic vs. random**: excitation is a known function of time vs. described statistically.

### 1.2 The Three Elemental Properties

| Element | Symbol | Constitutive law | Stores/dissipates | Units (SI) |
|---|---|---|---|---|
| Mass / inertia | m, J | F = m·a ; T = J·alpha | Kinetic energy | kg ; kg·m^2 |
| Spring (stiffness) | k, k_t | F = k·x ; T = k_t·theta | Potential (strain) energy | N/m ; N·m/rad |
| Damper (viscous) | c, c_t | F = c·x_dot | Dissipates energy | N·s/m ; N·m·s/rad |

### 1.3 Equivalent Stiffness

- **Springs in parallel** (same displacement): k_eq = k_1 + k_2 + ...
- **Springs in series** (same force): 1/k_eq = 1/k_1 + 1/k_2 + ...
- **Cantilever beam, end load**: k = 3·E·I / L^3
- **Simply supported beam, center load**: k = 48·E·I / L^3
- **Fixed-fixed beam, center load**: k = 192·E·I / L^3
- **Axial rod**: k = E·A / L
- **Torsional shaft**: k_t = G·J / L  (J = polar moment of area)
- **Helical spring**: k = G·d^4 / (8·D^3·N)

### 1.4 Equivalent Mass (energy method)

When a coordinate x is chosen, lump all kinetic energy into (1/2)·m_eq·x_dot^2.
Example — spring of mass m_s vibrating with end mass m: m_eq = m + m_s/3.
For a rolling/translating body, include both translational and rotational KE:
m_eq = m + J/r^2 (mass rolling without slip, radius r).

---

## 2. Undamped Free Vibration of SDOF Systems

### 2.1 Equation of Motion — Newton's Second Law Derivation

Consider mass m on a spring k, displacement x measured from static equilibrium.
Free body diagram (vertical): spring force k·x (restoring), gravity mg, static spring stretch delta_st where k·delta_st = mg.

Sum of forces = m·x_ddot:
  -k·(x + delta_st) + mg = m·x_ddot
Since k·delta_st = mg, the static terms cancel:
  **m·x_ddot + k·x = 0**

**Key takeaway:** measuring x from static equilibrium removes gravity from the EOM. Always do this.

### 2.2 Energy Method (Rayleigh) Derivation

Total energy E = T + U = (1/2)·m·x_dot^2 + (1/2)·k·x^2 = constant.
Differentiate w.r.t. time: m·x_dot·x_ddot + k·x·x_dot = 0.
Divide by x_dot: m·x_ddot + k·x = 0. Same EOM.

Rayleigh's method for w_n directly: equate T_max and U_max for assumed harmonic motion:
  (1/2)·m·(w_n·X)^2 = (1/2)·k·X^2  =>  **w_n = sqrt(k/m)**

### 2.3 Solution

General solution: x(t) = A·cos(w_n·t) + B·sin(w_n·t) = C·sin(w_n·t + phi)

- **Natural frequency**: w_n = sqrt(k/m)  [rad/s]
- **Natural frequency (Hz)**: f_n = w_n / (2·pi)
- **Period**: T_n = 2·pi / w_n = 1 / f_n

Apply initial conditions x(0) = x_0, x_dot(0) = v_0:
  A = x_0,  B = v_0 / w_n
  Amplitude: C = sqrt(x_0^2 + (v_0/w_n)^2)
  Phase: phi = atan2(x_0·w_n, v_0)   [so that x = C·sin(w_n·t + phi)]

### 2.4 Torsional Version

J·theta_ddot + k_t·theta = 0  =>  w_n = sqrt(k_t / J)

### 2.5 Pitfalls

- Forgetting to measure displacement from **static equilibrium** (gravity then wrongly appears).
- Mixing up f_n (Hz) and w_n (rad/s) — factor of 2·pi.
- Using mass m instead of mass moment of inertia J in torsional/pendulum problems.
- Equivalent stiffness: confusing series vs. parallel. Parallel = stiffer (k adds); series = softer.

---

## 3. Damped Free Vibration of SDOF Systems

### 3.1 Equation of Motion

Add a viscous damper c in parallel with the spring:
  **m·x_ddot + c·x_dot + k·x = 0**

Divide by m and define standard parameters:
  **x_ddot + 2·zeta·w_n·x_dot + w_n^2·x = 0**

- **Natural frequency**: w_n = sqrt(k/m)
- **Damping ratio**: zeta = c / c_c = c / (2·sqrt(k·m)) = c / (2·m·w_n)
- **Critical damping coefficient**: c_c = 2·sqrt(k·m) = 2·m·w_n

### 3.2 Characteristic Equation & Roots

Assume x = e^(s·t):  m·s^2 + c·s + k = 0
  s = (-c ± sqrt(c^2 - 4·m·k)) / (2·m) = -zeta·w_n ± w_n·sqrt(zeta^2 - 1)

The discriminant sign (c^2 - 4·m·k, equivalently zeta vs. 1) classifies the response.

### 3.3 Three Cases

**Underdamped (0 < zeta < 1)** — most common in practice:
  s_{1,2} = -zeta·w_n ± j·w_d
  **Damped natural frequency**: w_d = w_n·sqrt(1 - zeta^2)
  Solution: x(t) = e^(-zeta·w_n·t)·[A·cos(w_d·t) + B·sin(w_d·t)]
          = X·e^(-zeta·w_n·t)·sin(w_d·t + phi)
  With ICs x_0, v_0:
    A = x_0,  B = (v_0 + zeta·w_n·x_0) / w_d
    X = sqrt(x_0^2 + ((v_0 + zeta·w_n·x_0)/w_d)^2)
  The envelope is ±X·e^(-zeta·w_n·t). The decay rate is sigma = zeta·w_n.

**Critically damped (zeta = 1)**: repeated real root s = -w_n.
  x(t) = (A + B·t)·e^(-w_n·t),  A = x_0,  B = v_0 + w_n·x_0
  Fastest return to equilibrium without oscillation.

**Overdamped (zeta > 1)**: two distinct negative real roots.
  x(t) = A·e^(s_1·t) + B·e^(s_2·t),  s_{1,2} = -zeta·w_n ± w_n·sqrt(zeta^2 - 1)
  No oscillation; slower return than critical.

### 3.4 Logarithmic Decrement (experimental damping measurement)

Ratio of two successive peaks one period T_d = 2·pi/w_d apart:
  **delta = ln(x_n / x_{n+1}) = zeta·w_n·T_d = 2·pi·zeta / sqrt(1 - zeta^2)**

Over N cycles: delta = (1/N)·ln(x_0 / x_N)

Solve for damping ratio:
  **zeta = delta / sqrt((2·pi)^2 + delta^2)**

For light damping (zeta < ~0.1): delta ≈ 2·pi·zeta, so zeta ≈ delta / (2·pi).

### 3.5 Pitfalls

- zeta is dimensionless; c is not. Don't conflate them.
- w_d < w_n always (damping lowers the oscillation frequency).
- Log decrement assumes **successive peaks of the same sign** — peaks one full period apart, not half.
- For overdamped systems there is no w_d; do not compute it.
- The "decay rate" zeta·w_n equals -Re(s), the real part of the pole.

---

## 4. Forced Harmonic Vibration of SDOF Systems

### 4.1 Equation of Motion

Harmonic force F(t) = F_0·cos(w·t) applied to the mass:
  **m·x_ddot + c·x_dot + k·x = F_0·cos(w·t)**

w = forcing (driving) frequency; w_n = natural frequency. Define **frequency ratio r = w / w_n**.

Total response = transient (homogeneous) + steady-state (particular):
  x(t) = x_h(t) + x_p(t)
The transient x_h decays as e^(-zeta·w_n·t); after a few time constants only x_p remains.

### 4.2 Steady-State Solution Derivation (complex/phasor method)

Let F(t) = Re(F_0·e^(j·w·t)). Assume x_p = Re(X·e^(j·w·t)) with complex amplitude X.
Substituting: (-m·w^2 + j·c·w + k)·X = F_0
  X = F_0 / (k - m·w^2 + j·c·w)
Magnitude and phase:
  |X| = F_0 / sqrt((k - m·w^2)^2 + (c·w)^2)
  phase lag: phi = atan( (c·w) / (k - m·w^2) )

Steady-state response: x_p(t) = |X|·cos(w·t - phi). The response **lags** the force by phi.

### 4.3 Nondimensional Form — Magnification Factor

Divide numerator and denominator by k. Let X_st = F_0/k (static deflection), r = w/w_n:
  **Magnification factor M = |X| / X_st = 1 / sqrt((1 - r^2)^2 + (2·zeta·r)^2)**
  **Phase: phi = atan( 2·zeta·r / (1 - r^2) )**

Behavior:
- r << 1 (low frequency): M ≈ 1, phi ≈ 0° — stiffness-controlled, mass moves with force.
- r ≈ 1 (resonance region): M large, phi ≈ 90° — damping-controlled.
- r >> 1 (high frequency): M → 0 (as 1/r^2), phi → 180° — mass-controlled, mass can't keep up.

### 4.4 Resonance

- **Undamped (zeta = 0)**: M → infinity at r = 1. Response grows without bound:
  x_p(t) = (F_0/(2·m·w_n))·t·sin(w_n·t)  — linear growth in amplitude.
- **Damped peak**: M is maximized not exactly at r = 1 but at
  **r_peak = sqrt(1 - 2·zeta^2)**  (exists only for zeta < 1/sqrt(2) ≈ 0.707)
  Peak value: **M_max = 1 / (2·zeta·sqrt(1 - zeta^2))**
- At r = 1 exactly: M = 1/(2·zeta), phi = 90° regardless of zeta.

### 4.5 Quality Factor & Half-Power Bandwidth

- **Quality factor**: Q = M_max ≈ 1/(2·zeta) for light damping.
- **Half-power bandwidth**: the frequencies r_1, r_2 where M = M_max/sqrt(2).
  **Q = w_n / (w_2 - w_1) ≈ 1 / (2·zeta)**
  This is the standard experimental method to extract zeta from a frequency-response plot.

### 4.6 Pitfalls

- Resonance peak is at r_peak = sqrt(1 - 2·zeta^2), **not** r = 1 (only equal when zeta = 0).
- For zeta >= 0.707 there is **no peak** — M decreases monotonically from 1.
- Phase is always 90° at r = 1 — useful checkpoint.
- Don't forget the transient: "steady-state" only after transient decays (~4/(zeta·w_n) seconds).
- The response lags the force; sign of phase matters.

---

## 5. Base (Support) Excitation

### 5.1 Equation of Motion

Base moves y(t) = Y·sin(w·t); mass position x(t). Spring and damper feel relative motion:
  m·x_ddot = -k·(x - y) - c·(x_dot - y_dot)
  **m·x_ddot + c·x_dot + k·x = k·y + c·y_dot = c·w·Y·cos(w·t) + k·Y·sin(w·t)**

### 5.2 Displacement Transmissibility

The steady-state amplitude ratio X/Y (how much base motion reaches the mass):
  **T_d = X/Y = sqrt( (1 + (2·zeta·r)^2) / ((1 - r^2)^2 + (2·zeta·r)^2) )**

Same formula gives **force transmissibility** F_T/F_0 for a force-excited mass on an isolator.

### 5.3 Key Properties of Transmissibility

- At r = 0: T_d = 1.
- At r = sqrt(2): **T_d = 1 for ALL damping values** — universal crossover point.
- For r < sqrt(2): increasing damping **reduces** transmissibility (good).
- For r > sqrt(2): increasing damping **increases** transmissibility (bad — isolation region).
- Isolation (T_d < 1) requires **r > sqrt(2)**, i.e., w > sqrt(2)·w_n — the isolator must be soft.

### 5.4 Relative Motion (z = x - y)

  m·z_ddot + c·z_dot + k·z = -m·y_ddot = m·w^2·Y·sin(w·t)
  Z/Y = r^2 / sqrt((1 - r^2)^2 + (2·zeta·r)^2)
This is the basis of seismometers (large r → Z/Y ≈ 1 measures base displacement) and
accelerometers (small r → Z ∝ base acceleration).

---

## 6. Rotating Unbalance

### 6.1 Equation of Motion

Machine of total mass M with an unbalanced mass m at eccentricity e rotating at w.
The rotating mass contributes a vertical force m·e·w^2·sin(w·t):
  **M·x_ddot + c·x_dot + k·x = m·e·w^2·sin(w·t)**

This is harmonic forcing with **frequency-dependent amplitude** F_0 = m·e·w^2.

### 6.2 Steady-State Amplitude

  **X = (m·e/M)·r^2 / sqrt((1 - r^2)^2 + (2·zeta·r)^2)**

Equivalently: M·X / (m·e) = r^2 · M, the nondimensional group M·X/(m·e) plotted vs. r.

Behavior:
- r → 0: X → 0 (slow rotation, negligible centrifugal force).
- r ≈ 1: peak (near resonance).
- r → infinity: **M·X/(m·e) → 1**, so X → m·e/M (a finite limit, unlike constant-force forcing where X → 0).

The peak of M·X/(m·e) occurs at **r_peak = 1 / sqrt(1 - 2·zeta^2)** (note: reciprocal of the constant-force case).

### 6.3 Pitfalls

- The forcing amplitude is **not constant** — it scales with w^2. This flips the high-frequency asymptote.
- Use total mass M in the inertia term; m is only the unbalanced portion.
- Two-plane balancing vs. single-plane: this section is single-plane (static) unbalance.

---

## 7. Vibration Isolation & Damping Models

### 7.1 Isolation Design

Goal: minimize transmitted force/motion. From transmissibility:
- Choose mounts so the system operates at **r > sqrt(2)** (preferably r > 3).
- Soft mounts (low k) → low w_n → high r → good isolation, but large static deflection.
- Percent isolation = (1 - T_d)·100%.
- **Tradeoff**: high damping helps during startup/shutdown passage through resonance but
  worsens steady-state isolation at high r. Practical designs use moderate zeta (0.05–0.2).

### 7.2 Other Damping Models

- **Coulomb (dry friction)**: F_d = mu·N·sign(x_dot). Amplitude decays **linearly** (not exponentially);
  decay per cycle = 4·mu·N/k. Frequency stays w_n.
- **Hysteretic (structural) damping**: damping force proportional to displacement, in phase with velocity.
  Complex stiffness k(1 + j·eta), eta = loss factor. Energy/cycle independent of frequency.
- **Equivalent viscous damping**: replace a nonlinear damper with c_eq that dissipates the same
  energy per cycle: c_eq = (energy dissipated per cycle) / (pi·w·X^2).

---

## 8. Multi-Degree-of-Freedom (MDOF) Systems

### 8.1 Matrix Equation of Motion

For n DOF, coordinates collected in vector {x}:
  **[M]{x_ddot} + [C]{x_dot} + [K]{x} = {F(t)}**
- [M] mass matrix (symmetric, positive definite)
- [K] stiffness matrix (symmetric, positive semidefinite)
- [C] damping matrix
Off-diagonal terms represent coupling.

### 8.2 Building the Matrices

- **Newton's method**: FBD each mass, write m_i·x_i_ddot = sum of forces. Collect coefficients.
- **Lagrange's equations**: d/dt(dL/dx_dot_i) - dL/dx_i + dD/dx_dot_i = Q_i, where L = T - U,
  D = Rayleigh dissipation function. Systematic for complex systems.
- **Stiffness influence coefficients**: k_ij = force at i to produce unit displacement at j (others fixed).

### 8.3 Undamped Free Vibration — Eigenvalue Problem

Set [C] = 0, {F} = 0. Assume synchronous harmonic motion {x} = {phi}·e^(j·w·t):
  **([K] - w^2·[M]){phi} = {0}**
Nontrivial solution requires:
  **det([K] - w^2·[M]) = 0**   ← characteristic (frequency) equation
This polynomial in w^2 has n roots: the **natural frequencies** w_1^2, w_2^2, ..., w_n^2
(ordered w_1 <= w_2 <= ...). The fundamental frequency is w_1.

### 8.4 Mode Shapes

For each w_i, solve ([K] - w_i^2·[M]){phi_i} = {0} for the **eigenvector (mode shape) {phi_i}**.
A mode shape gives the relative amplitudes of all DOF when the system vibrates purely at w_i.
Mode shapes are determined only up to a scale factor (normalize as convenient).

### 8.5 Orthogonality of Modes

For distinct natural frequencies:
  {phi_i}^T·[M]·{phi_j} = 0   and   {phi_i}^T·[K]·{phi_j} = 0   for i ≠ j
Normalize mass: {phi_i}^T·[M]·{phi_i} = 1 (mass-normalized). Then {phi_i}^T·[K]·{phi_i} = w_i^2.

### 8.6 Modal (Principal Coordinate) Analysis — Solution Procedure

1. Solve eigenvalue problem for all w_i and {phi_i}.
2. Form modal matrix [Phi] = [{phi_1} {phi_2} ... {phi_n}].
3. Transform: {x} = [Phi]{q}, where {q} = modal coordinates.
4. Pre-multiply EOM by [Phi]^T → **decouples** into n independent SDOF equations:
     q_i_ddot + 2·zeta_i·w_i·q_i_dot + w_i^2·q_i = N_i(t)   (if damping is proportional)
5. Solve each SDOF equation, then recombine {x} = [Phi]{q}.

**Proportional (Rayleigh) damping**: [C] = alpha·[M] + beta·[K] guarantees [C] is also diagonalized
by the same modes; otherwise the system has complex modes.

### 8.7 Vibration Absorber (Tuned Mass Damper)

Adding a secondary mass-spring (m_2, k_2) to a primary system. Tuned so w_2 = sqrt(k_2/m_2) = w
(forcing frequency). At that frequency the primary mass amplitude → 0 (undamped absorber).
The single resonance splits into two new resonances straddling the original; adding damping to
the absorber broadens the effective operating band.

### 8.8 Pitfalls

- det([K] - w^2[M]) = 0, **not** det([K] - w[M]) — the eigenvalue is w^2.
- Mode shapes are relative; never report absolute numbers without stating normalization.
- Modal decoupling requires proportional damping (or undamped). General [C] does not decouple.
- A 2-DOF system has 2 natural frequencies and 2 mode shapes — count them.
- The lowest natural frequency (fundamental) usually dominates the dynamic response.

---

## 9. Continuous (Distributed-Parameter) Systems

### 9.1 Longitudinal Vibration of a Bar

PDE:  d^2u/dx^2 = (1/c^2)·d^2u/dt^2,   wave speed c = sqrt(E/rho)
Separation of variables u(x,t) = U(x)·T(t) → spatial ODE U'' + (w/c)^2·U = 0.
Natural frequencies depend on boundary conditions:
- Fixed-free: w_n = (2n-1)·pi·c / (2·L),  n = 1, 2, 3, ...
- Fixed-fixed / free-free: w_n = n·pi·c / L

### 9.2 Torsional Vibration of a Shaft

Same form: d^2theta/dx^2 = (1/c^2)·d^2theta/dt^2,  c = sqrt(G/rho)

### 9.3 Transverse Vibration of a String

d^2w/dx^2 = (1/c^2)·d^2w/dt^2,  c = sqrt(T/rho_L)  (T = tension, rho_L = mass per length)
Fixed-fixed string: w_n = n·pi·c / L.

### 9.4 Transverse Vibration of an Euler-Bernoulli Beam

PDE:  E·I·d^4w/dx^4 + rho·A·d^2w/dt^2 = 0
Spatial solution involves sin, cos, sinh, cosh of beta·x where beta^4 = rho·A·w^2/(E·I).
**Natural frequencies**: w_n = (beta_n·L)^2 · sqrt(E·I / (rho·A·L^4))
The values (beta_n·L) come from the boundary-condition frequency equation:
- Simply supported: beta_n·L = n·pi  → w_n = (n·pi)^2·sqrt(EI/(rho·A·L^4))
- Cantilever (fixed-free): beta_n·L ≈ 1.875, 4.694, 7.855, ...
- Fixed-fixed / free-free: beta_n·L ≈ 4.730, 7.853, 10.996, ...

Each w_n has an associated **mode shape** W_n(x); continuous systems have infinitely many.

### 9.5 Pitfalls

- Continuous systems have infinitely many natural frequencies and modes.
- Beam frequency scales with (beta·L)^2, not (beta·L) — the fourth-order PDE.
- Euler-Bernoulli ignores shear deformation and rotary inertia (good for slender beams only;
  use Timoshenko for stubby beams or high modes).

---

## 10. Kinematics & Dynamics of Mechanisms and Linkages

### 10.1 Mobility (Kutzbach / Gruebler Criterion)

Planar mechanism degrees of freedom:
  **M = 3·(N - 1) - 2·J_1 - J_2**
- N = number of links (including ground)
- J_1 = number of full (1-DOF) joints: pins, sliders
- J_2 = number of half (2-DOF) joints: cam/gear contacts
M = 1 means a single input fully determines the motion (a "mechanism"). M = 0 is a structure;
M < 0 is a preloaded/redundant structure.

### 10.2 Four-Bar Linkage & Grashof's Law

Let S = shortest link, L = longest, P, Q = other two.
**Grashof condition**: S + L <= P + Q  → at least one link can fully rotate.
- Shortest is the crank (adjacent to ground): crank-rocker.
- Shortest is the ground link: double-crank (drag-link).
- Shortest is the coupler: double-rocker.
Non-Grashof (S + L > P + Q): triple-rocker, no link makes a full revolution.

### 10.3 Position, Velocity, Acceleration Analysis

**Vector loop equation** (closed kinematic chain): sum of position vectors around the loop = 0.
  r_1 + r_2 + r_3 + r_4 = 0  (complex-number or vector form)
Differentiate once → velocity loop equation; twice → acceleration loop equation. Solve the
two scalar component equations for the two unknowns at each level.

**Relative velocity**: v_B = v_A + v_{B/A}, where v_{B/A} = omega × r_{B/A} (magnitude omega·r).
**Relative acceleration**: a_B = a_A + a_{B/A,normal} + a_{B/A,tangential}
- Normal (centripetal): magnitude omega^2·r, directed A → B... wait, directed from B toward A (toward center).
- Tangential: magnitude alpha·r, perpendicular to r_{B/A}.
**Coriolis acceleration**: appears when a point moves along a rotating link:
  a_cor = 2·omega × v_rel,  magnitude 2·omega·v_rel.

### 10.4 Instant Center of Velocity

A point (possibly off the body) with zero instantaneous velocity. For a body, v = omega × r
measured from the instant center. **Kennedy's theorem**: the three instant centers of any three
bodies in relative motion are collinear. Number of instant centers = N·(N-1)/2.

### 10.5 Dynamic Force Analysis

For each link apply Newton-Euler:
  Sum F = m·a_G   (a_G = acceleration of mass center)
  Sum M_G = I_G·alpha   (about mass center)
**D'Alembert's principle**: treat -m·a_G as an "inertia force" and -I_G·alpha as an "inertia
torque", then solve as a statics problem (dynamic equilibrium).
Solution procedure: do full kinematics first (get all a_G and alpha), then write force/moment
equations link-by-link and solve the linear system for joint reactions and input torque.

### 10.6 Cam Dynamics & Mechanism Balancing

- **Cam follower motion**: displacement s(theta), velocity s'·omega, acceleration s''·omega^2 +
  s'·alpha. Avoid discontinuities in acceleration (jerk) — use cycloidal or polynomial profiles.
- **Rotating balance**: for shafts, sum(m_i·r_i) = 0 (static) and sum(m_i·r_i·a_i) = 0 (dynamic,
  for couples) — generally needs correction masses in two planes.
- **Reciprocating balance** (slider-crank): primary inertia force ∝ cos(theta), secondary ∝
  cos(2·theta). Counterweights cancel primary but introduce transverse forces — partial balance.

### 10.7 Pitfalls

- Gruebler's criterion can give wrong M for special geometries (parallel links, redundant
  constraints) — always sanity-check physically.
- Coriolis term is the most-forgotten acceleration component — include it whenever a slider
  moves along a rotating link.
- Normal acceleration always points toward the center of rotation; tangential is perpendicular.
- In dynamic force analysis, do **all** kinematics before any kinetics.
- Balancing reduces shaking forces but rarely eliminates all of them in reciprocating machines.

---

## 11. Quick-Reference Formula Tables

### 11.1 SDOF Core Parameters

| Quantity | Formula |
|---|---|
| Natural frequency | w_n = sqrt(k/m) |
| Damped natural frequency | w_d = w_n·sqrt(1 - zeta^2) |
| Damping ratio | zeta = c/(2·sqrt(k·m)) = c/(2·m·w_n) |
| Critical damping | c_c = 2·sqrt(k·m) = 2·m·w_n |
| Period (undamped) | T_n = 2·pi/w_n |
| Frequency ratio | r = w/w_n |
| Static deflection | X_st = F_0/k |
| Log decrement | delta = 2·pi·zeta/sqrt(1-zeta^2) |
| zeta from delta | zeta = delta/sqrt(4·pi^2 + delta^2) |

### 11.2 Forced-Response Functions (r = w/w_n)

| Quantity | Formula |
|---|---|
| Magnification factor M | 1/sqrt((1-r^2)^2 + (2·zeta·r)^2) |
| Phase lag phi | atan(2·zeta·r/(1-r^2)) |
| Peak frequency ratio | r_peak = sqrt(1 - 2·zeta^2) |
| Peak magnification | M_max = 1/(2·zeta·sqrt(1-zeta^2)) |
| Transmissibility T_d | sqrt((1+(2·zeta·r)^2)/((1-r^2)^2+(2·zeta·r)^2)) |
| Rotating unbalance | M·X/(m·e) = r^2/sqrt((1-r^2)^2+(2·zeta·r)^2) |
| Quality factor | Q ≈ 1/(2·zeta) = w_n/(w_2-w_1) |

### 11.3 Damping Regimes

| zeta | Name | Roots | Behavior |
|---|---|---|---|
| 0 | Undamped | ±j·w_n | Sustained oscillation |
| 0 < zeta < 1 | Underdamped | -zeta·w_n ± j·w_d | Decaying oscillation |
| zeta = 1 | Critically damped | -w_n (double) | Fastest non-oscillatory return |
| zeta > 1 | Overdamped | two real < 0 | Slow non-oscillatory return |

### 11.4 Special Frequency Ratios

| r value | Significance |
|---|---|
| r = 0 | M = 1, T_d = 1, phi = 0 |
| r = 1 | phi = 90° always; M = 1/(2·zeta) |
| r = sqrt(2) | T_d = 1 for all zeta (isolation crossover) |
| r > sqrt(2) | Isolation region (T_d < 1) |

---

## Open-source sources used

- James M. Fiore / contributors, *Vibration Mechanics* (open-source vibrations textbook, University of South Carolina mirror) — `https://cse.sc.edu/~adowney2/publications/textbooks/Vibration-Mechanics/Vibration_Mechanics.pdf`
- *Mechanical Engineering Vibrations*, Engineering LibreTexts (California State Polytechnic University, Humboldt) — Topic 08, Forced Vibration of Single DOF: Damped System Under Harmonic Excitation — `https://eng.libretexts.org/Courses/California_State_Polytechnic_University_Humboldt/Mechanical_Engineering_Vibrations`
- *Introductory Dynamics: 2D Kinematics and Kinetics of Point Masses and Rigid Bodies* (Steeneken), Engineering LibreTexts — Ch. 13 Vibrations / 13.4 Forced Vibrations — `https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Introductory_Dynamics:_2D_Kinematics_and_Kinetics_of_Point_Masses_and_Rigid_Bodies_(Steeneken)`
- Mechanics Map open textbook (Pennsylvania State University) — One-DOF Vibrations chapter — `https://mechanicsmap.psu.edu/websites/16_one_dof_vibrations/`
- Istanbul Technical University open lecture notes — *Vibration of Single Degree of Freedom Systems* and *Two Degree of Freedom Systems* — `https://web.itu.edu.tr/~gundes/sdof.pdf`, `https://web.itu.edu.tr/~gundes/2dof.pdf`
- MIT OpenCourseWare — Mechanical Engineering, Vibrations and Dynamics course materials — `https://ocw.mit.edu/`
