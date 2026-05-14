# Physics II — Calculus-Based Electricity & Magnetism Reference

> PHYS 2212. Graduate-level study companion: precise definitions, governing laws (Maxwell's equations in integral form), derivations, problem-solving procedures, worked-example patterns, constants, and common student pitfalls. Plain-text math notation (`^` = power, `∫` = integral, `∮` = closed-loop/closed-surface integral, vectors in **bold**).

---

## 0. Constants and Conventions

| Quantity | Symbol | Value |
|---|---|---|
| Elementary charge | e | 1.602 x 10^-19 C |
| Coulomb constant | k = 1/(4πε_0) | 8.99 x 10^9 N·m^2/C^2 |
| Permittivity of free space | ε_0 | 8.854 x 10^-12 C^2/(N·m^2) |
| Permeability of free space | μ_0 | 4π x 10^-7 T·m/A = 1.257 x 10^-6 T·m/A |
| Speed of light | c = 1/sqrt(μ_0 ε_0) | 2.998 x 10^8 m/s |
| Electron mass | m_e | 9.109 x 10^-31 kg |
| Proton mass | m_p | 1.673 x 10^-27 kg |

Units: charge = coulomb (C); E-field = N/C = V/m; potential = volt (V) = J/C; capacitance = farad (F) = C/V; current = ampere (A) = C/s; resistance = ohm (Ω) = V/A; magnetic field = tesla (T) = kg/(A·s^2) = Wb/m^2; magnetic flux = weber (Wb) = T·m^2; inductance = henry (H) = Wb/A = V·s/A.

---

## 1. Electric Charge and Coulomb's Law

### 1.1 Charge

- Two kinds: positive and negative. Like charges repel, unlike attract.
- **Quantized:** q = N e, integer multiples of e.
- **Conserved:** total charge of an isolated system is constant.
- Conductors: charge moves freely. Insulators (dielectrics): charge is bound. Charging by friction, conduction, and induction.

### 1.2 Coulomb's Law

Force between two point charges q1, q2 separated by r:
```
F = k q1 q2 / r^2 = (1/(4πε_0)) q1 q2 / r^2
```
Vector form: **F**_(12) = k q1 q2 / r^2 * r̂_(12), directed along the line joining them. Attractive for opposite signs, repulsive for like signs.

**Superposition principle:** the net force on a charge is the vector sum of the Coulomb forces from every other charge: **F**_net = Σ **F**_i.

**Pitfall:** Plugging signed charges into the magnitude formula and then also assigning a direction — pick one. Best practice: use magnitudes for |F|, then set direction by inspection (repel/attract).

---

## 2. The Electric Field

### 2.1 Definition

The electric field is the force per unit positive test charge:
```
E = F / q_0        (units N/C = V/m)
```
Field of a point charge: **E** = k q / r^2 * r̂ (points away from + charge, toward - charge).

### 2.2 Superposition and continuous distributions

- Discrete: **E** = Σ k q_i / r_i^2 * r̂_i.
- Continuous: **E** = ∫ k dq / r^2 * r̂, with dq = λ dl (line), σ dA (surface), or ρ dV (volume).

Standard results (memorize the functional forms):

| Source | Field | Notes |
|---|---|---|
| Point charge | E = k q / r^2 | radial |
| Infinite line charge (linear density λ) | E = λ / (2π ε_0 r) = 2kλ/r | radial, ∝ 1/r |
| Infinite sheet (surface density σ) | E = σ / (2 ε_0) | uniform, independent of distance |
| Two parallel sheets (capacitor) | E = σ / ε_0 between, 0 outside | uniform |
| Ring of charge on axis | E = k Q x / (x^2 + R^2)^(3/2) | zero at center |
| Dipole on axis (far field) | E ≈ 2 k p / r^3 | p = q d, dipole moment |
| Dipole on perpendicular bisector | E ≈ k p / r^3 | |

### 2.3 Electric field lines

Start on + charges, end on - charges (or infinity). Density ∝ field strength. Never cross. Tangent gives direction of **E**.

### 2.4 Dipole in a uniform field

- Dipole moment **p** = q **d** (points from - to +).
- Torque: **τ** = **p** x **E**, magnitude τ = p E sin θ.
- Potential energy: U = -**p**·**E** = -p E cos θ (minimum when aligned).

### 2.5 Motion of charges in fields

A charge q in field **E** feels **F** = q **E**, acceleration **a** = q**E**/m. In a uniform field this is the projectile-motion analog (e.g., electron deflected between capacitor plates).

---

## 3. Gauss's Law

### 3.1 Electric flux

Flux through a surface: Φ_E = ∫ **E**·d**A**. For a closed surface, d**A** points outward.

### 3.2 Gauss's Law (Maxwell equation #1)

```
∮ E·dA = Q_enclosed / ε_0
```
The net electric flux through any closed (Gaussian) surface equals the enclosed charge divided by ε_0. It is always true; it is *useful* for finding **E** only when symmetry makes E constant and either parallel or perpendicular over each surface patch.

### 3.3 Symmetry → Gaussian surface choice

| Symmetry | Gaussian surface | Result |
|---|---|---|
| Spherical (point charge, sphere) | concentric sphere | E = k Q_enc / r^2 |
| Cylindrical (line, long cylinder) | coaxial cylinder | E = λ / (2π ε_0 r) |
| Planar (sheet, slab) | "pillbox" straddling the sheet | E = σ / (2 ε_0) |

### 3.4 Procedure

1. Identify symmetry; choose a Gaussian surface so **E** is constant in magnitude and either ⊥ or ∥ to each face.
2. Compute flux: Φ = E A over the faces where E is perpendicular and constant.
3. Find Q_enclosed (integrate the density over the volume inside the surface).
4. Solve E A = Q_enc / ε_0 for E.

### 3.5 Conductors in electrostatic equilibrium (key consequences of Gauss's law)

- **E = 0** everywhere inside the conducting material.
- Any net charge resides entirely on the **surface**.
- **E** just outside the surface is perpendicular to it, magnitude E = σ / ε_0.
- The conductor is an equipotential (volume and surface).
- A cavity inside a conductor with no enclosed charge has E = 0 (electrostatic shielding / Faraday cage).

**Pitfall:** Trying to use Gauss's law to get E for a charge distribution with no symmetry — the integral ∮E·dA still equals Q/ε_0, but you can't pull E out of the integral.

---

## 4. Electric Potential

### 4.1 Definitions

- **Potential energy change:** ΔU = -W_field = -∫ **F**·d**l** = -q ∫ **E**·d**l**.
- **Electric potential:** V = U / q (energy per unit charge, scalar). ΔV = V_b - V_a = -∫(a→b) **E**·d**l**.
- Potential of a point charge: V = k q / r (with V = 0 at r = ∞).
- Superposition: V = Σ k q_i / r_i = ∫ k dq / r (scalar sum — much easier than the vector E-field sum).

### 4.2 Relationship between E and V

```
ΔV = -∫ E·dl        and        E = -∇V
1D:  E_x = -dV/dx
```
**E** points "downhill" in potential — from high V to low V — and is perpendicular to equipotential surfaces.

### 4.3 Potential energy of a charge configuration

U = k Σ_(i<j) q_i q_j / r_ij  (sum over all unique pairs). This is the work to assemble the configuration from infinity.

### 4.4 Worked patterns

- **Charged conductor sphere (radius R, charge Q):** outside V = kQ/r; on/inside V = kQ/R (constant — it's an equipotential).
- **Energy of accelerated charge:** q ΔV = ΔKE → e.g., electron through potential difference: (1/2)m v^2 = e V.
- **Capacitor plates:** V = E d (uniform field).

### 4.5 Procedure

1. To find V from charges: scalar superposition V = Σ k q_i / r_i (mind signs of q).
2. To find V from E: integrate -∫E·dl along any convenient path.
3. To find E from V: E = -gradient of V.
4. Energy problems: use q ΔV = -ΔU and the work-energy theorem.

**Pitfall:** Potential is a scalar — do NOT assign it a direction. Also: V can be zero where E is nonzero (e.g., midpoint between +q and -q) and E can be zero where V is nonzero (inside a charged conductor).

---

## 5. Capacitance and Dielectrics

### 5.1 Definition

A capacitor stores charge +Q and -Q on two conductors at potential difference V:
```
C = Q / V        (farad, F)
```
C depends only on geometry (and the dielectric), not on Q or V.

### 5.2 Capacitor geometries

| Geometry | Capacitance |
|---|---|
| Parallel plate (area A, separation d) | C = ε_0 A / d |
| Cylindrical (length L, radii a < b) | C = 2π ε_0 L / ln(b/a) |
| Spherical (radii a < b) | C = 4π ε_0 a b / (b - a) |
| Isolated sphere (radius R) | C = 4π ε_0 R |

### 5.3 Combinations

- **Parallel:** same V, charges add → C_eq = C1 + C2 + ...
- **Series:** same Q, voltages add → 1/C_eq = 1/C1 + 1/C2 + ...

(Note: opposite rules from resistors.)

### 5.4 Energy stored

```
U = (1/2) Q V = (1/2) C V^2 = Q^2 / (2C)
```
Energy density of the electric field: u_E = (1/2) ε_0 E^2 (J/m^3). Energy is stored in the field itself.

### 5.5 Dielectrics

Inserting a dielectric (dielectric constant κ > 1) between plates:
- Capacitance increases: C = κ C_0.
- Permittivity becomes ε = κ ε_0.
- The dielectric reduces the field (E = E_0/κ) by polarization; allows more charge at the same voltage.
- If the battery stays connected: V fixed, Q increases. If isolated: Q fixed, V decreases.

**Pitfall:** Mixing up series/parallel rules — they are the *reverse* of resistor rules. Also forgetting whether the battery is connected (V constant) or disconnected (Q constant) when a dielectric is inserted.

---

## 6. Current, Resistance, and DC Circuits

### 6.1 Current and current density

- Current: I = dQ/dt (amperes). Conventional current = direction positive charge would flow.
- Current density: J = I / A; microscopically J = n q v_drift, where n = carrier density, v_drift = drift velocity.

### 6.2 Ohm's law and resistance

```
V = I R          (Ohm's law for ohmic materials)
R = ρ L / A      (ρ = resistivity, L = length, A = cross-section)
```
- Resistivity temperature dependence: ρ(T) ≈ ρ_0 [1 + α (T - T_0)].
- Microscopic Ohm's law: **J** = σ **E**, σ = 1/ρ (conductivity).

### 6.3 Power

```
P = I V = I^2 R = V^2 / R
```
Power dissipated as heat in a resistor (Joule heating). For a battery delivering energy: P = I·EMF.

### 6.4 EMF and internal resistance

A real battery: terminal voltage V = EMF - I r, where r = internal resistance. Maximum power transfer to a load when R_load = r.

### 6.5 Resistor combinations

- **Series:** same I → R_eq = R1 + R2 + ...
- **Parallel:** same V → 1/R_eq = 1/R1 + 1/R2 + ...

### 6.6 Kirchhoff's rules

- **Junction (current) rule:** Σ I_in = Σ I_out at any node (charge conservation).
- **Loop (voltage) rule:** Σ ΔV = 0 around any closed loop (energy conservation). Sign conventions: across a resistor, ΔV = -IR in the direction of assumed current; across a battery, +EMF going - to +.

**Procedure:** assign current variables and directions; write junction equations (one fewer than the number of nodes); write independent loop equations; solve the linear system. A negative current just means the actual direction is opposite to your guess.

### 6.7 RC circuits

Charging a capacitor through a resistor (EMF ε, time constant τ = RC):
```
q(t)   = C ε (1 - e^(-t/τ))
I(t)   = (ε/R) e^(-t/τ)
V_C(t) = ε (1 - e^(-t/τ))
```
Discharging: q(t) = Q_0 e^(-t/τ), I(t) = (Q_0/RC) e^(-t/τ).
After one τ, charge reaches ~63% of final (or decays to ~37%). After ~5τ, essentially complete.

**Pitfall:** Treating a capacitor as a wire in steady state — at long times (fully charged) it carries NO current (acts as open circuit); at t = 0 (uncharged) it acts like a wire (short circuit).

---

## 7. Magnetic Fields and Magnetic Forces

### 7.1 Magnetic force on a moving charge

```
F = q v x B        magnitude F = q v B sin θ
```
Force is perpendicular to both **v** and **B** (right-hand rule). Magnetic force does **no work** (F ⊥ v) — it changes direction, not speed.

### 7.2 Charged particle motion in a uniform B

- **v ⊥ B:** circular motion. Radius r = m v / (q B); period T = 2π m / (q B); cyclotron frequency ω = q B / m (independent of speed).
- **v at an angle to B:** helical path (circular component ⊥ B, uniform drift ∥ B).
- **Velocity selector (crossed E and B):** undeflected when q E = q v B → v = E/B.

### 7.3 Force on a current-carrying wire

```
F = I L x B        magnitude F = I L B sin θ
```
For a non-uniform field or curved wire: F = I ∫ d**l** x **B**.

### 7.4 Torque on a current loop / magnetic dipole

- Magnetic moment: **μ** = N I A n̂ (N turns, area A).
- Torque: **τ** = **μ** x **B**, magnitude τ = μ B sin θ.
- Potential energy: U = -**μ**·**B**. This is the principle of motors and galvanometers.

### 7.5 Hall effect

A current-carrying conductor in a perpendicular B develops a transverse voltage V_Hall; sign reveals carrier sign, magnitude gives carrier density.

**Pitfall:** Forgetting the sin θ factor (no force when v ∥ B). Sloppy right-hand rule (for negative charges, force is opposite to v x B).

---

## 8. Sources of Magnetic Field

### 8.1 Biot–Savart Law

The field from a current element:
```
dB = (μ_0 / 4π) I dl x r̂ / r^2
```
Integrate over the full circuit for total **B**.

Standard results:

| Source | Field |
|---|---|
| Infinite straight wire (distance r) | B = μ_0 I / (2π r) |
| Center of circular loop (radius R) | B = μ_0 I / (2R) |
| On axis of loop (distance x) | B = μ_0 I R^2 / [2 (R^2 + x^2)^(3/2)] |
| Inside a long solenoid (n turns/length) | B = μ_0 n I (uniform; ~0 outside) |
| Inside a toroid (N total turns) | B = μ_0 N I / (2π r) |

Direction: right-hand rule — thumb along current, fingers curl in the direction of **B**.

### 8.2 Ampère's Law (Maxwell equation #4, magnetostatic form)

```
∮ B·dl = μ_0 I_enclosed
```
The line integral of **B** around any closed (Amperian) loop equals μ_0 times the current threading the loop. Useful for finding **B** when there is enough symmetry (straight wire, solenoid, toroid, current sheet).

**Procedure:** choose an Amperian loop matching the symmetry so **B** is constant and parallel/perpendicular along it; evaluate ∮B·dl = B·(path length); set equal to μ_0 I_enc; solve for B.

### 8.3 Forces between parallel currents

Two parallel wires distance d apart, currents I1, I2:
```
F/L = μ_0 I1 I2 / (2π d)
```
Parallel currents attract; antiparallel currents repel.

### 8.4 Gauss's law for magnetism (Maxwell equation #2)

```
∮ B·dA = 0
```
No magnetic monopoles — magnetic field lines always close on themselves; net magnetic flux through any closed surface is zero.

### 8.5 Magnetic materials (brief)

Diamagnetic (weakly repelled), paramagnetic (weakly attracted), ferromagnetic (strong, retains magnetization — domains, hysteresis). Relative permeability μ_r; B = μ_r μ_0 H inside material.

**Pitfall:** Confusing the Biot–Savart approach (always works, integral) with Ampère's law (exact always, *solvable* only with symmetry). Also: B outside an ideal solenoid ≈ 0, not μ_0 n I.

---

## 9. Electromagnetic Induction (Faraday's Law)

### 9.1 Magnetic flux

Φ_B = ∫ **B**·d**A** = B A cos θ for a uniform field through a flat loop.

### 9.2 Faraday's Law (Maxwell equation #3)

```
EMF = -dΦ_B / dt          (for N turns: EMF = -N dΦ_B/dt)
```
A changing magnetic flux through a circuit induces an EMF. Flux can change via: changing B, changing area A, or changing orientation θ.

### 9.3 Lenz's Law

The induced current flows in the direction that **opposes the change** in flux that produced it (the minus sign in Faraday's law). It is a statement of energy conservation — the induced effects resist the change driving them.

### 9.4 Motional EMF

A rod of length L moving with speed v perpendicular to B:
```
EMF = B L v
```
Derivation: magnetic force on carriers qvB drives them along the rod until an electrostatic field balances it; the potential difference is B L v. If the rod completes a circuit of resistance R: I = BLv/R, and an external force F = BIL = B^2L^2v/R is needed to maintain v (the work done equals I^2R dissipated).

### 9.5 Induced electric fields

A changing B creates a non-conservative (curling) electric field even with no charges present:
```
∮ E·dl = -dΦ_B / dt
```
Unlike electrostatic fields, ∮E·dl ≠ 0 here — induced E-field lines form closed loops.

### 9.6 Applications

Generators (rotating loop → sinusoidal EMF: EMF = N B A ω sin(ωt)), transformers (V_s/V_p = N_s/N_p), eddy currents (induced currents in bulk conductors → braking, heating), induction cooktops.

**Pitfall:** Sign confusion — use Lenz's law qualitatively to get the current direction, and use the magnitude |dΦ/dt| for the EMF size. Also: EMF depends on the *rate of change* of flux, not the flux itself (constant large flux → zero EMF).

---

## 10. Inductance and AC Circuits

### 10.1 Self-inductance

A changing current in a coil induces an EMF opposing the change:
```
EMF = -L dI/dt          L = N Φ_B / I  (henry)
```
Solenoid inductance: L = μ_0 n^2 V = μ_0 N^2 A / l.

### 10.2 Mutual inductance

EMF_2 = -M dI_1/dt; M depends on geometry and coupling between the coils (basis of transformers).

### 10.3 Energy stored in an inductor

```
U = (1/2) L I^2
```
Magnetic energy density: u_B = B^2 / (2 μ_0) (J/m^3).

### 10.4 RL circuits

Current rise through R and L with EMF ε (time constant τ = L/R):
```
I(t) = (ε/R)(1 - e^(-t/τ))      [energizing]
I(t) = I_0 e^(-t/τ)             [de-energizing]
```
After 1τ current reaches ~63% of final value. An inductor opposes *changes* in current: at t=0 it acts like an open circuit; at steady state it acts like a plain wire.

### 10.5 LC oscillations

An ideal LC circuit oscillates: energy sloshes between the capacitor's electric field and the inductor's magnetic field.
```
ω = 1 / sqrt(L C)        T = 2π sqrt(L C)
```
Direct analog of a mass–spring oscillator (q ↔ x, I ↔ v, 1/C ↔ k, L ↔ m).

### 10.6 RLC circuits and AC

- Series RLC has resonance at ω_0 = 1/sqrt(LC).
- Reactances: capacitive X_C = 1/(ωC), inductive X_L = ωL.
- Impedance: Z = sqrt(R^2 + (X_L - X_C)^2); peak current I_0 = V_0 / Z.
- Phase angle: tan φ = (X_L - X_C)/R.
- RMS values: V_rms = V_0/sqrt(2); average power P_avg = I_rms V_rms cos φ (cos φ = power factor).

**Pitfall:** Treating an inductor as instantly conducting — it resists current changes. Also confusing the inductor/capacitor steady-state behaviors (capacitor → open, inductor → short at DC steady state).

---

## 11. Maxwell's Equations and Electromagnetic Waves

### 11.1 Maxwell's equations (integral form, in vacuum)

```
(1) Gauss's law:            ∮ E·dA = Q_enc / ε_0
(2) Gauss's law (magnetism): ∮ B·dA = 0
(3) Faraday's law:           ∮ E·dl = -dΦ_B/dt
(4) Ampère–Maxwell law:      ∮ B·dl = μ_0 I_enc + μ_0 ε_0 dΦ_E/dt
```
Maxwell's key addition: the **displacement current** term μ_0 ε_0 dΦ_E/dt — a changing electric field acts as a source of magnetic field, just as a current does. This makes the equations self-consistent and predicts EM waves.

### 11.2 Electromagnetic waves

In free space, Maxwell's equations combine to give a wave equation; **E** and **B** propagate together:
```
c = 1 / sqrt(μ_0 ε_0) = 2.998 x 10^8 m/s
```
Properties of an EM plane wave:
- **E** ⊥ **B** ⊥ direction of propagation (transverse wave).
- E and B oscillate in phase; E/B = c at every instant.
- No medium required (propagates through vacuum).
- Speed in a medium: v = c/n, n = index of refraction = sqrt(κ μ_r) ≈ sqrt(κ).

### 11.3 Energy, intensity, momentum

- Poynting vector (energy flux): **S** = (1/μ_0) **E** x **B**; direction = propagation direction.
- Intensity (time-averaged): I = S_avg = (1/2) ε_0 c E_0^2 = E_rms B_rms / μ_0.
- Radiation pressure: P = I/c (absorbed) or 2I/c (reflected).

### 11.4 The EM spectrum

Radio → microwave → infrared → visible (≈ 400–700 nm) → ultraviolet → X-ray → gamma. All travel at c in vacuum; differ only in frequency/wavelength (c = f λ).

---

## 12. Introduction to Optics

### 12.1 Geometric optics

- **Law of reflection:** angle of incidence = angle of reflection (measured from the normal).
- **Snell's law (refraction):** n_1 sin θ_1 = n_2 sin θ_2.
- **Total internal reflection:** occurs going from higher to lower n when θ_1 > θ_c, where sin θ_c = n_2/n_1.
- **Dispersion:** n depends weakly on wavelength → prisms separate colors.

### 12.2 Mirrors and lenses

Thin-lens / mirror equation:
```
1/f = 1/d_o + 1/d_i        magnification m = -d_i/d_o = h_i/h_o
```
Sign conventions: f > 0 for converging lens / concave mirror; f < 0 for diverging lens / convex mirror. d_i > 0 for real images (opposite side for lens, same side for mirror). m < 0 means inverted. Lensmaker's equation: 1/f = (n - 1)(1/R_1 - 1/R_2).

### 12.3 Physical (wave) optics

- **Double-slit interference (Young):** bright fringes at d sin θ = m λ; dark at d sin θ = (m + 1/2)λ.
- **Single-slit diffraction:** dark minima at a sin θ = m λ (m = 1, 2, ...).
- **Diffraction grating:** principal maxima at d sin θ = m λ — sharp, bright lines; basis of spectroscopy.
- **Thin films:** interference between reflections from the two surfaces; a π phase shift occurs on reflection going to a higher-index medium. Condition depends on film thickness and whether there are 0, 1, or 2 phase-inverting reflections.

**Pitfall:** Forgetting the half-wavelength phase shift on reflection in thin-film problems; mixing up the interference-maximum condition (d sin θ = mλ) with the single-slit *minimum* condition (a sin θ = mλ) — they look alike but mean opposite things.

---

## 13. General Problem-Solving Strategy (E&M)

1. **Identify the regime:** electrostatics (Coulomb, Gauss, potential), circuits (Ohm, Kirchhoff, RC/RL), magnetostatics (Biot–Savart, Ampère, magnetic force), induction (Faraday, Lenz), or waves/optics.
2. **Exploit symmetry.** Spherical/cylindrical/planar → Gauss's law or Ampère's law. No symmetry → direct integration (Coulomb / Biot–Savart) or superposition.
3. **Use potential (scalar) over field (vector) when you can** — V superposition is a scalar sum.
4. **Circuits:** reduce series/parallel combinations first; if irreducible, go straight to Kirchhoff's rules and solve the linear system.
5. **Induction:** get the EMF magnitude from |dΦ/dt|, get the current direction from Lenz's law.
6. **Check limits and units.** Far-field behavior (point-charge-like), correct dimensions, sensible sign.

### Recurring student pitfalls (master list)

- Treating electric potential as a vector (it is a scalar).
- Using Gauss's or Ampère's law where there is no symmetry.
- Swapping series/parallel rules between capacitors and resistors.
- Forgetting "battery connected (V fixed)" vs "isolated (Q fixed)" when inserting a dielectric.
- Forgetting the sin θ in magnetic force; sloppy right-hand rule, especially for negative charges.
- Thinking magnetic force does work (it never does).
- Assuming a capacitor conducts in steady state or that an inductor conducts instantly.
- Confusing flux with rate of change of flux in Faraday's law.
- Omitting the displacement-current term in Ampère–Maxwell.
- Sign-convention errors in lens/mirror equations.
- Missing the reflection phase shift in thin-film interference.

---

## Open-source sources used

- OpenStax, *University Physics Volume 2* (Thermodynamics; Electricity and Magnetism) — openstax.org/books/university-physics-volume-2 — chapter summaries, key equations, and key terms for Chapters 5–16.
- OpenStax, *University Physics Volume 3* (Optics and Modern Physics) — openstax.org/books/university-physics-volume-3 — geometric and wave optics chapters.
- LibreTexts Physics, *University Physics II – Thermodynamics, Electricity, and Magnetism (OpenStax)* — phys.libretexts.org — derivations and worked treatments of Gauss's law, capacitance, induction, and Maxwell's equations.
- MIT OpenCourseWare 8.02 *Physics II: Electricity and Magnetism* — ocw.mit.edu — lecture notes, problem-solving methodology, and the Maxwell's equations synthesis.
- OpenStax, *College Physics 2e* — openstax.org/books/college-physics-2e — supplementary algebra-based treatment of circuits and optics.
