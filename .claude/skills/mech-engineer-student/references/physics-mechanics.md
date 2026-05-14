# Physics I — Calculus-Based Mechanics Reference

> PHYS 2211 (Kennesaw State University). Graduate-level study companion: precise definitions, governing laws, derivations, problem-solving procedures, worked-example patterns, constants, and common student pitfalls. Plain-text math notation throughout (`^` = power, `*` = multiply, `d/dt` = derivative, `∫` = integral, vectors in **bold** or with explicit components).

---

## 0. Foundations: Units, Vectors, Calculus Tools

### SI Base Units & Key Constants

| Quantity | Symbol | Value / Unit |
|---|---|---|
| Standard gravity (Earth surface) | g | 9.80 m/s^2 (use 9.81 unless told otherwise) |
| Gravitational constant | G | 6.674 x 10^-11 N·m^2/kg^2 |
| Speed of light (vacuum) | c | 2.998 x 10^8 m/s |
| Avogadro number (used in mechanics of gases) | N_A | 6.022 x 10^23 /mol |
| Force unit | newton | 1 N = 1 kg·m/s^2 |
| Energy unit | joule | 1 J = 1 N·m = 1 kg·m^2/s^2 |
| Power unit | watt | 1 W = 1 J/s |

### Vectors

A vector has magnitude and direction. In 2D: **A** = A_x x̂ + A_y ŷ, with A_x = A cos θ, A_y = A sin θ, magnitude A = sqrt(A_x^2 + A_y^2), direction θ = atan2(A_y, A_x).

- **Addition:** component-wise. **C** = **A** + **B** → C_x = A_x + B_x, etc.
- **Dot product (scalar):** **A**·**B** = A_x B_x + A_y B_y + A_z B_z = A B cos θ. Result is a scalar. Used for work, flux, projections.
- **Cross product (vector):** |**A** x **B**| = A B sin θ; direction by right-hand rule. Used for torque, angular momentum, magnetic force. **A** x **B** = -(**B** x **A**).
- **Unit vector:** Â = **A**/|**A**|.

**Pitfall:** Students add magnitudes of perpendicular vectors directly. Always resolve into components first.

### Calculus toolkit

- Velocity is the time-derivative of position; acceleration is the time-derivative of velocity. Conversely, position is the time-integral of velocity.
- d/dt(x^n) = n x^(n-1); d/dt(sin ωt) = ω cos ωt; d/dt(cos ωt) = -ω sin ωt; d/dt(e^(kt)) = k e^(kt).
- Chain rule trick (eliminates time): a = dv/dt = (dv/dx)(dx/dt) = v dv/dx. Integrating v dv = a dx gives the work-energy / "timeless" kinematic relation.

---

## 1. Kinematics in One and Two Dimensions

### 1.1 Definitions (precise)

- **Position** x(t): location relative to a chosen origin. Frame-dependent.
- **Displacement** Δx = x_f - x_i: change in position; a vector; path-independent.
- **Distance**: total path length traveled; a scalar; path-dependent; always ≥ |displacement|.
- **Average velocity:** v_avg = Δx/Δt (vector). **Average speed:** total distance / total time (scalar).
- **Instantaneous velocity:** v(t) = dx/dt = lim(Δt→0) Δx/Δt. The slope of the x-t curve.
- **Instantaneous speed:** |v(t)|.
- **Average acceleration:** a_avg = Δv/Δt.
- **Instantaneous acceleration:** a(t) = dv/dt = d^2x/dt^2. The slope of the v-t curve.

### 1.2 Constant-acceleration kinematic equations (1D)

Valid ONLY when a = constant. Let v_0 = initial velocity, x_0 = initial position.

```
(1)  v   = v_0 + a t
(2)  x   = x_0 + v_0 t + (1/2) a t^2
(3)  v^2 = v_0^2 + 2 a (x - x_0)        [time-eliminated]
(4)  x   = x_0 + (1/2)(v_0 + v) t       [acceleration-eliminated]
```

**Derivation of (2) and (3):** From a = dv/dt constant, integrate: v = v_0 + a t. Then v = dx/dt, integrate again: x = x_0 + v_0 t + (1/2) a t^2. For (3), use a = v dv/dx → ∫v dv = ∫a dx → (v^2 - v_0^2)/2 = a(x - x_0).

### 1.3 Free fall

Object under gravity alone (neglect air resistance): a = -g (taking up as positive), g = 9.81 m/s^2. All four kinematic equations apply with a → -g. At the peak of trajectory v = 0 (but a is still -g). Time up = time down for symmetric flight.

### 1.4 Projectile motion (2D)

Horizontal and vertical motions are **independent**, coupled only by shared time t.

- Horizontal: a_x = 0 → x = x_0 + v_0x t, v_x = v_0x = constant.
- Vertical: a_y = -g → y = y_0 + v_0y t - (1/2) g t^2, v_y = v_0y - g t.
- Launch components: v_0x = v_0 cos θ, v_0y = v_0 sin θ.
- Trajectory equation (eliminate t): y = (tan θ) x - [g / (2 v_0^2 cos^2 θ)] x^2  → a parabola.
- Range (level ground): R = v_0^2 sin(2θ) / g. Maximum range at θ = 45°.
- Max height: H = v_0^2 sin^2 θ / (2g). Time of flight (level): T = 2 v_0 sin θ / g.

**Pitfall:** Using the range formula when landing height ≠ launch height. In that case solve the vertical equation for t first, then get x.

### 1.5 Relative motion

v_(A/C) = v_(A/B) + v_(B/C) (velocity of A relative to C). Subtract observer velocity vectorially. Classic: boat crossing river, plane in wind.

### 1.6 Problem-solving procedure (kinematics)

1. Sketch; choose origin and positive direction(s).
2. List knowns/unknowns with signs.
3. Pick the equation containing exactly your unknown and known quantities.
4. For 2D, split into x and y; t is the bridge.
5. Solve algebraically, then substitute numbers; check units and sign.

---

## 2. Newton's Laws of Motion (Dynamics)

### 2.1 The three laws (formal statements)

- **First Law (Inertia):** A body remains at rest or in uniform straight-line motion unless acted on by a net external force. Defines inertial reference frames.
- **Second Law:** The net external force on a body equals the time rate of change of its momentum: **F**_net = d**p**/dt. For constant mass: **F**_net = m **a**. Component form: ΣF_x = m a_x, ΣF_y = m a_y.
- **Third Law:** For every force **F**_(A on B) there is an equal-magnitude, opposite-direction force **F**_(B on A). Action–reaction pairs act on **different bodies** and never cancel on the same free-body diagram.

### 2.2 Common forces

| Force | Formula / behavior | Notes |
|---|---|---|
| Weight | W = m g, directed toward Earth's center | mass invariant, weight depends on g |
| Normal force N | perpendicular to contact surface | a constraint force — solve for it, never assume N = mg |
| Tension T | along a rope/cable, pulls away from object | massless ideal rope: same T throughout, even over an ideal pulley |
| Static friction | f_s ≤ μ_s N | adjusts up to a maximum to prevent sliding |
| Kinetic friction | f_k = μ_k N, opposes relative sliding | μ_k usually < μ_s |
| Spring (Hooke's law) | F = -k x | restoring; x measured from natural length |
| Drag (low speed) | F = -b v | linear in velocity |
| Drag (high speed) | F = (1/2) C ρ A v^2 | quadratic; opposes motion |

### 2.3 Free-body diagram (FBD) procedure

1. Isolate ONE object; represent it as a point/box.
2. Draw every external force acting ON it (gravity, normal, tension, friction, applied, spring, drag). Do NOT draw forces the object exerts on others.
3. Choose axes — tilt them along the acceleration direction (e.g. along an incline).
4. Resolve each force into components.
5. Write ΣF_x = m a_x and ΣF_y = m a_y.
6. Apply constraints (e.g. connected masses share |a|; surface contact gives a_perp = 0).
7. Solve the system.

### 2.4 Worked-example patterns

- **Inclined plane (angle θ, frictionless):** axes along/perpendicular to surface. Along: m g sin θ = m a → a = g sin θ. Perp: N = m g cos θ.
- **Incline with kinetic friction (sliding down):** m g sin θ - μ_k m g cos θ = m a.
- **Atwood machine (masses m1 > m2 over ideal pulley):** a = (m1 - m2) g / (m1 + m2); T = 2 m1 m2 g / (m1 + m2).
- **Connected blocks (one on table, one hanging):** treat as system for a, then isolate one block for T.
- **Elevator / apparent weight:** N = m(g + a). a up → feel heavier; a down → lighter; free fall → N = 0.

### 2.5 Uniform circular motion

A body moving in a circle at constant speed has centripetal acceleration directed toward the center:
```
a_c = v^2 / r = ω^2 r        →    F_net (radial) = m v^2 / r
```
The net inward force is supplied by some real force (tension, gravity, friction, normal). "Centripetal force" is a role, not a new force.

- **Banked curve (frictionless):** tan θ = v^2 / (r g).
- **Car on flat curve:** f_s = m v^2 / r ≤ μ_s m g → v_max = sqrt(μ_s r g).
- **Vertical loop, top:** minimum speed when N = 0: v_min = sqrt(g r).

**Pitfall:** Treating "centrifugal force" as real in an inertial frame. There is no outward force; the inward net force causes the curved path.

---

## 3. Work, Energy, and Power

### 3.1 Work

Work done by a constant force: W = **F**·**d** = F d cos θ. For a varying force along a path:
```
W = ∫ F·dr   (line integral);   1D:  W = ∫ F(x) dx
```
- Work is a scalar; positive if force has a component along displacement, negative if opposed, zero if perpendicular (e.g. normal force, centripetal force on circular path do no work).
- Work by a spring from x1 to x2: W_spring = -(1/2)k(x2^2 - x1^2).
- Work by gravity (near Earth): W_grav = -m g (y_f - y_i) = -ΔU_grav.

### 3.2 Kinetic energy and the Work–Energy Theorem

Kinetic energy: KE = (1/2) m v^2.

**Work–Energy Theorem:** W_net = ΔKE = (1/2)m v_f^2 - (1/2)m v_i^2.

**Derivation:** W_net = ∫F dx = ∫m a dx = ∫m (v dv/dx) dx = ∫m v dv = (1/2)m v_f^2 - (1/2)m v_i^2.

### 3.3 Potential energy

Defined for **conservative forces** (work is path-independent; equals zero around any closed loop). F_x = -dU/dx.

| Type | U | Reference |
|---|---|---|
| Gravity (near surface) | U = m g y | y = 0 chosen freely |
| Spring | U = (1/2) k x^2 | x = natural length |
| Gravitation (general) | U = -G M m / r | U → 0 as r → ∞ |

### 3.4 Conservation of mechanical energy

If only conservative forces do work: E_mech = KE + U = constant.
```
(1/2)m v_i^2 + U_i = (1/2)m v_f^2 + U_f
```
With non-conservative forces (friction, applied, drag):
```
KE_i + U_i + W_nc = KE_f + U_f
```
Energy lost to kinetic friction: |W_friction| = f_k * d (d = path length).

### 3.5 Power

- Average power: P_avg = W / Δt = ΔE / Δt.
- Instantaneous power: P = dW/dt = **F**·**v** = F v cos θ.
- 1 horsepower ≈ 746 W.

### 3.6 Problem-solving procedure (energy)

1. Define system and choose U = 0 reference.
2. Identify initial and final states (snapshots).
3. List forces; classify conservative vs non-conservative.
4. If only conservative → conservation of mechanical energy. Else use KE_i + U_i + W_nc = KE_f + U_f.
5. Solve for the unknown (often v_f or height). Energy methods avoid needing acceleration or time.

**Pitfall:** Double-counting gravity — either include W_grav as work OR include U_grav, never both. Same for springs.

---

## 4. Linear Momentum and Collisions

### 4.1 Momentum and impulse

- Linear momentum: **p** = m **v** (vector).
- Newton's 2nd law (general form): **F**_net = d**p**/dt.
- **Impulse:** **J** = ∫**F** dt = Δ**p** = F_avg Δt. The Impulse–Momentum Theorem.

### 4.2 Conservation of momentum

If the net **external** force on a system is zero, total momentum is conserved:
```
Σ p_i (before) = Σ p_f (after)
m1 v1i + m2 v2i = m1 v1f + m2 v2f
```
Internal forces (collision forces) cancel by Newton's 3rd law. Momentum can be conserved in one direction even if not in another (e.g. horizontal momentum conserved during a projectile explosion).

### 4.3 Collision types

| Type | Momentum | Kinetic energy | Signature |
|---|---|---|---|
| Elastic | conserved | conserved | objects bounce; KE_i = KE_f |
| Inelastic | conserved | NOT conserved | some KE → heat/deformation |
| Perfectly inelastic | conserved | maximum KE loss | objects stick together, common v_f |

- **Perfectly inelastic:** v_f = (m1 v1i + m2 v2i) / (m1 + m2).
- **1D elastic collision** (solving momentum + KE together):
  ```
  v1f = ((m1 - m2)/(m1 + m2)) v1i + (2 m2/(m1 + m2)) v2i
  v2f = (2 m1/(m1 + m2)) v1i + ((m2 - m1)/(m1 + m2)) v2i
  ```
  Useful identity for elastic collisions: relative velocity reverses → v1i - v2i = -(v1f - v2f).
- Equal masses, elastic, target at rest: velocities simply exchange.

### 4.4 Center of mass

```
r_cm = (Σ m_i r_i) / (Σ m_i)        (discrete)
r_cm = (1/M) ∫ r dm                  (continuous)
```
- v_cm = (Σ m_i v_i)/M. The CM moves as if all mass and all external force acted there: **F**_ext = M **a**_cm.
- In an explosion with no external force, the CM continues on its original trajectory.

### 4.5 Problem-solving procedure (momentum)

1. Define system; check that net external force ≈ 0 during the interaction (collisions are brief → external impulses negligible).
2. Set up "before" and "after" momentum, by component.
3. Choose the right conservation laws: momentum always (if isolated); KE only if elastic.
4. Solve. For 2D, write x and y momentum equations separately.

**Pitfall:** Assuming KE is conserved in every collision. Only elastic collisions conserve KE.

---

## 5. Rotational Motion (Fixed-Axis)

### 5.1 Rotational kinematics

Angular position θ (rad), angular velocity ω = dθ/dt, angular acceleration α = dω/dt.
Constant-α equations (direct analogs of linear):
```
ω   = ω_0 + α t
θ   = θ_0 + ω_0 t + (1/2) α t^2
ω^2 = ω_0^2 + 2 α (θ - θ_0)
```
Linear–angular links (radius r): s = r θ, v = r ω (tangential speed), a_t = r α (tangential acceleration), a_c = r ω^2 = v^2/r (centripetal).

### 5.2 Moment of inertia

Rotational analog of mass — resistance to angular acceleration:
```
I = Σ m_i r_i^2   (discrete);    I = ∫ r^2 dm   (continuous)
```
**Parallel-axis theorem:** I = I_cm + M d^2, where d is the distance from the CM axis to the parallel axis.

Common moments of inertia (mass M):

| Body (axis) | I |
|---|---|
| Point mass, radius r | M r^2 |
| Thin rod, center | (1/12) M L^2 |
| Thin rod, end | (1/3) M L^2 |
| Solid disk/cylinder, central axis | (1/2) M R^2 |
| Hollow cylinder / ring | M R^2 |
| Solid sphere, diameter | (2/5) M R^2 |
| Thin spherical shell, diameter | (2/3) M R^2 |

### 5.3 Torque and Newton's 2nd law for rotation

Torque: **τ** = **r** x **F**, magnitude τ = r F sin φ = (lever arm) x F. Sign by right-hand rule (CCW positive by convention).
```
Σ τ = I α        (Newton's 2nd law for rotation)
```

### 5.4 Rotational kinetic energy and rolling

- Rotational KE: KE_rot = (1/2) I ω^2.
- Work by a torque: W = ∫ τ dθ; Power: P = τ ω.
- **Rolling without slipping:** v_cm = R ω, a_cm = R α. Total KE = (1/2)M v_cm^2 + (1/2)I_cm ω^2.
- Object rolling down incline (height h): v_cm = sqrt(2 g h / (1 + I_cm/(M R^2))). Smaller I/MR^2 → faster (solid sphere beats disk beats hoop).

### 5.5 Angular momentum

- Particle: **L** = **r** x **p**, magnitude L = r p sin φ.
- Rigid body about fixed axis: L = I ω.
- **Conservation:** if Σ τ_ext = 0, then **L** is conserved → I_i ω_i = I_f ω_f. (Spinning skater pulls arms in: I decreases, ω increases.)
- Newton's 2nd law (rotational, general): Σ**τ**_ext = d**L**/dt.

### 5.6 Static equilibrium

A rigid body is in equilibrium when:
```
Σ F = 0   AND   Σ τ = 0   (torque about ANY point)
```
Procedure: FBD with forces at their actual application points; pick a pivot that eliminates an unknown (place pivot at an unknown force); write ΣF_x, ΣF_y, Στ; solve. Classic: ladder against wall, beam with supports, see-saw.

**Pitfall:** Forgetting that torque depends on the choice of pivot for individual terms (though Στ = 0 holds about every point in equilibrium). Also: using full force instead of the perpendicular component / lever arm.

---

## 6. Newton's Law of Universal Gravitation

### 6.1 The law

Every two point masses attract along the line joining them:
```
F = G m1 m2 / r^2          G = 6.674 x 10^-11 N·m^2/kg^2
```
A spherically symmetric body acts gravitationally as if all its mass were at its center (shell theorem). Surface gravity: g = G M / R^2.

### 6.2 Gravitational potential energy (general)

U(r) = -G M m / r, with U → 0 at r → ∞. (Reduces to m g y near a surface for small height changes.)

### 6.3 Orbits

- **Circular orbit:** gravity supplies centripetal force: G M m / r^2 = m v^2 / r → v_orbit = sqrt(G M / r).
- **Orbital period (Kepler's 3rd, circular):** T^2 = (4 π^2 / (G M)) r^3.
- **Total orbital energy:** E = KE + U = -G M m / (2 r) (bound orbit → E < 0).
- **Escape speed:** set E = 0 → v_esc = sqrt(2 G M / r) = sqrt(2) * v_orbit.

### 6.4 Kepler's Laws

1. Planets move in ellipses with the Sun at one focus.
2. The line from Sun to planet sweeps equal areas in equal times (consequence of angular-momentum conservation).
3. T^2 ∝ a^3 (a = semi-major axis).

---

## 7. Oscillations (Simple Harmonic Motion)

### 7.1 Definition and the SHM equation

SHM occurs when the restoring force is proportional to displacement: F = -k x. Newton's law gives:
```
m d^2x/dt^2 = -k x   →   d^2x/dt^2 + ω^2 x = 0,   ω = sqrt(k/m)
```
General solution: x(t) = A cos(ω t + φ).
- A = amplitude, ω = angular frequency, φ = phase constant.
- v(t) = -A ω sin(ω t + φ); a(t) = -A ω^2 cos(ω t + φ) = -ω^2 x.
- Period T = 2π/ω = 2π sqrt(m/k); frequency f = 1/T = ω/(2π).
- **Key fact:** period is independent of amplitude (for ideal SHM).

### 7.2 Energy in SHM

E = (1/2) k A^2 = (1/2) m v_max^2 = constant. v_max = A ω; a_max = A ω^2.
At any x: (1/2)m v^2 + (1/2)k x^2 = (1/2)k A^2 → v = ω sqrt(A^2 - x^2).

### 7.3 Pendulums

- **Simple pendulum (small angle θ < ~15°):** restoring torque gives d^2θ/dt^2 + (g/L)θ = 0 → ω = sqrt(g/L), T = 2π sqrt(L/g). Independent of mass and amplitude (small-angle approximation sin θ ≈ θ).
- **Physical pendulum:** T = 2π sqrt(I / (m g d)), d = pivot-to-CM distance.
- **Torsional pendulum:** T = 2π sqrt(I/κ), κ = torsion constant.

### 7.4 Damped and driven oscillations

- **Damped:** m x'' + b x' + k x = 0. Underdamped → oscillation with decaying amplitude A(t) = A_0 e^(-bt/2m). Critically damped → fastest return without oscillation. Overdamped → slow non-oscillatory return.
- **Driven / resonance:** a periodic driving force at frequency near the natural frequency ω_0 produces large-amplitude response (resonance). Sharpness of resonance set by damping.

**Pitfall:** Using T = 2π sqrt(L/g) for large-amplitude pendulums — the small-angle approximation fails and the true period grows with amplitude.

---

## 8. Mechanical Waves

### 8.1 Wave basics

A wave transfers energy and momentum without transporting matter. Transverse (medium displaces perpendicular to propagation, e.g. string) vs longitudinal (parallel, e.g. sound).

Key relations:
```
v = f λ = λ / T          (wave speed = frequency x wavelength)
k = 2π/λ  (wave number),   ω = 2π f  (angular frequency),   v = ω/k
```
Wave on a string: v = sqrt(F_T / μ), μ = mass per unit length, F_T = tension.
Sound speed in air ≈ 343 m/s at 20 °C (scales as sqrt(T)).

### 8.2 Traveling wave function

y(x,t) = A sin(k x - ω t + φ) describes a wave moving in +x. (k x + ω t → moving in -x.)
- Transverse velocity of a string element: ∂y/∂t (NOT the wave speed v).
- The wave equation: ∂^2y/∂x^2 = (1/v^2) ∂^2y/∂t^2.

### 8.3 Superposition and interference

Waves add linearly (superposition principle).
- **Constructive interference:** path difference = n λ (in phase) → amplitude adds.
- **Destructive interference:** path difference = (n + 1/2) λ (out of phase) → amplitudes subtract.

### 8.4 Standing waves and resonance

Two identical waves traveling in opposite directions form a standing wave with fixed nodes and antinodes.
- **String fixed at both ends (length L):** λ_n = 2L/n, f_n = n v / (2L), n = 1, 2, 3, ... (n = 1 is the fundamental; higher n are harmonics).
- **Pipe open at both ends:** f_n = n v/(2L), n = 1, 2, 3, ...
- **Pipe closed at one end:** f_n = n v/(4L), n = 1, 3, 5, ... (odd harmonics only).

### 8.5 Sound phenomena

- **Intensity:** I = P / A; for a point source I ∝ 1/r^2. Sound level β = 10 log10(I / I_0) dB, I_0 = 10^-12 W/m^2.
- **Beats:** two close frequencies give beat frequency f_beat = |f1 - f2|.
- **Doppler effect:** f_observed = f_source (v ± v_observer) / (v ∓ v_source). Signs: choose so that approach raises pitch, recession lowers it.

**Pitfall:** Confusing wave speed v (set by the medium) with the transverse speed of a particle in the medium (depends on amplitude and frequency). Also: when a wave changes medium, frequency stays fixed; speed and wavelength change.

---

## 9. General Problem-Solving Heuristics

1. **Read & sketch.** Diagram, coordinate system, label every quantity with symbol and sign.
2. **Classify.** Which model applies? Kinematics (no forces needed), Newton's laws (forces & acceleration), energy (initial/final states, no time needed), momentum (collisions/explosions, brief interactions), rotational analog, SHM, waves.
3. **Choose conservation laws when possible.** Energy and momentum methods sidestep messy force integrals.
4. **Set up before substituting.** Solve symbolically; check limiting cases (m2 → 0, θ → 0, friction → 0).
5. **Check units and magnitude.** Does the answer have correct dimensions and a physically sensible size and sign?

### Recurring student pitfalls (master list)

- Mixing scalar and vector reasoning; adding perpendicular magnitudes.
- Assuming N = m g always (it is a constraint force — solve for it).
- Treating action–reaction pairs as canceling on one FBD.
- Forgetting friction direction opposes *relative motion/tendency*, not necessarily the velocity.
- Double-counting a conservative force as both work and potential energy.
- Assuming KE conserved in all collisions (only elastic).
- Using constant-a kinematics when a is not constant.
- Using small-angle pendulum period at large amplitude.
- Confusing angular quantities' units (radians vs degrees) — calculus formulas require radians.
- Sign errors in Doppler and in incline coordinate choices.

---

## Open-source sources used

- OpenStax, *University Physics Volume 1* (Mechanics, Sound, Oscillations, and Waves) — openstax.org/books/university-physics-volume-1 — chapter summaries, key equations, and key terms for Chapters 3–17.
- OpenStax, *University Physics Volume 2* (Thermodynamics; introductory framing of energy concepts) — openstax.org/books/university-physics-volume-2.
- LibreTexts Physics, *University Physics I – Mechanics, Sound, Oscillations, and Waves (OpenStax)* — phys.libretexts.org — derivations and worked treatments (e.g., Newton's second law for rotation, rolling motion).
- MIT OpenCourseWare 8.01 *Physics I: Classical Mechanics* — ocw.mit.edu — problem-solving methodology and lecture notes.
- OpenStax, *College Physics 2e* — openstax.org/books/college-physics-2e — supplementary algebra-based treatment of the same topics.
