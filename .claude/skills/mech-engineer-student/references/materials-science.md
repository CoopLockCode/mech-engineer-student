# Materials Science & Engineering Reference

PhD-level study companion for ME 3101 — Materials Science & Engineering, Kennesaw State University.
Covers atomic bonding, crystal structures & defects, diffusion, mechanical behavior & testing, dislocations & strengthening, failure (fracture/fatigue/creep), phase diagrams & the Fe-C system, heat treatment, polymers, ceramics, composites, electrical/thermal properties, and corrosion.

Math is in plain text: `x^2` = x squared, `sqrt(x)` = square root, `d^(-1/2)` = d to the minus one-half, subscripts written inline (sigma_y).

---

## 1. Atomic Structure & Interatomic Bonding

### 1.1 Atomic bonding fundamentals
- **Primary (strong) bonds:** ionic, covalent, metallic. Bond energies 100–1000 kJ/mol.
  - **Ionic** — electron transfer (metal → nonmetal); nondirectional; e.g. NaCl, MgO, Al2O3. High melting point, hard, brittle, electrically insulating.
  - **Covalent** — electron sharing; highly directional; e.g. diamond, Si, polymers (C-C backbone). Directionality governs crystal geometry.
  - **Metallic** — delocalized "electron sea" around positive ion cores; nondirectional; e.g. Fe, Cu, Al. Explains ductility, electrical/thermal conductivity, opacity, luster.
- **Secondary (weak) bonds:** van der Waals, hydrogen bonding. Bond energies < 100 kJ/mol. Govern polymer inter-chain forces, boiling points, physical adsorption.

### 1.2 The condensed-matter interatomic potential
Net potential energy between two atoms:
`E_N(r) = E_A + E_R = -A/r^m + B/r^n` with `n > m` (repulsion shorter-range than attraction).
- **Equilibrium spacing r0** at `dE_N/dr = 0` → the bond length.
- **Bonding energy E0** = depth of the potential well at r0.
- **Deep, narrow well** → high E0 → high melting temp, high elastic modulus, low thermal expansion.
- Elastic modulus is proportional to `(d^2 E_N / dr^2)` evaluated at r0 — curvature of the well at the bottom.
- Coefficient of thermal expansion scales with the **asymmetry (anharmonicity)** of the well.

### 1.3 Common student pitfalls
- Confusing bond *energy* (well depth) with bond *length* (well minimum position).
- Forgetting that secondary bonds, though weak, dictate polymer thermal/mechanical behavior.
- Assuming all ceramics are ionic — many (SiC, Si3N4) are substantially covalent.

---

## 2. Crystal Structures

### 2.1 The seven crystal systems & 14 Bravais lattices
Crystal systems defined by lattice parameters (a, b, c) and interaxial angles (alpha, beta, gamma): cubic, tetragonal, orthorhombic, rhombohedral (trigonal), hexagonal, monoclinic, triclinic.

### 2.2 Common metallic structures

| Structure | Atoms/cell | Coordination # | APF | a vs R | Examples |
|-----------|-----------|----------------|-----|--------|----------|
| BCC | 2 | 8 | 0.68 | a = 4R/sqrt(3) | alpha-Fe, Cr, W, Mo, V |
| FCC | 4 | 12 | 0.74 | a = 2R*sqrt(2) | gamma-Fe, Al, Cu, Ni, Ag, Au, Pb |
| HCP | 6 | 12 | 0.74 | c/a ideal = 1.633 | Mg, Zn, Ti, Cd, Co |

- **Atomic Packing Factor (APF)** = (volume of atoms in cell) / (volume of cell). FCC and HCP are close-packed (0.74).
- **Theoretical density:** `rho = (n * A) / (V_C * N_A)` — n = atoms/cell, A = atomic weight, V_C = cell volume, N_A = Avogadro's number.

### 2.3 Crystallographic directions & planes
- **Directions [uvw]:** vector components reduced to smallest integers; negatives written with overbar.
- **Planes (hkl) — Miller indices:** reciprocals of axis intercepts, cleared of fractions. `(hkl)` plane is perpendicular to `[hkl]` direction in cubic systems.
- **Linear density** = atoms centered on a direction vector / vector length. **Planar density** = atoms centered on a plane / plane area.
- **Slip** occurs on close-packed planes along close-packed directions (highest planar/linear density).
- **Interplanar spacing (cubic):** `d_hkl = a / sqrt(h^2 + k^2 + l^2)`.

### 2.4 X-ray diffraction
- **Bragg's law:** `n*lambda = 2*d*sin(theta)` — n = order, lambda = wavelength, d = interplanar spacing, theta = Bragg angle (incident angle to plane).
- Diffraction occurs only when Bragg's law is satisfied AND structure-factor selection rules permit:
  - BCC: peaks when (h+k+l) is even.
  - FCC: peaks when h,k,l are all even or all odd (unmixed).

### 2.5 Pitfalls
- Mixing up the *measured* angle (2*theta in a diffractometer) vs the Bragg angle theta.
- Forgetting selection rules — not every plane diffracts.
- HCP uses 4-index (Miller-Bravais) notation [uvtw]; do not apply cubic shortcuts.

---

## 3. Imperfections (Defects) in Solids

### 3.1 Point defects
- **Vacancy** — missing atom. Equilibrium concentration: `N_v / N = exp(-Q_v / (k*T))` — Q_v = vacancy formation energy, k = Boltzmann constant, T = absolute temp. Concentration rises exponentially with T.
- **Self-interstitial** — atom squeezed into interstitial site (high energy, rare in metals).
- **Substitutional & interstitial impurities** — solid solutions.
- **Hume-Rothery rules** for extensive substitutional solid solubility: (1) atomic size difference < ~15%, (2) same crystal structure, (3) similar electronegativity, (4) same or higher valence preferred.
- **Composition:** weight percent `C1 = m1/(m1+m2) * 100`; atom percent `C1' = n_m1/(n_m1+n_m2) * 100`.

### 3.2 Line defects — dislocations (see Section 6 for mechanics)
- **Edge dislocation** — extra half-plane of atoms; Burgers vector **b** perpendicular to dislocation line; glides only on its slip plane.
- **Screw dislocation** — spiral ramp distortion; **b** parallel to line; can **cross-slip** onto intersecting planes.
- **Mixed dislocation** — edge + screw character along a curved line.
- **Burgers vector b** — magnitude and direction of lattice distortion, found via a Burgers circuit. For FCC slip, b = (a/2)<110>.

### 3.3 Interfacial (planar) defects
- **Grain boundaries** — misorientation between grains; low-angle vs high-angle; higher energy than bulk → preferential sites for corrosion, segregation, second-phase nucleation.
- **Twin boundaries** — mirror-image lattice across the boundary (annealing twins in FCC; deformation twins in BCC/HCP).
- **Stacking faults** — error in close-packed stacking sequence (ABCABC for FCC).
- **Free surfaces** — highest-energy interface.

### 3.4 Bulk defects
Pores, cracks, inclusions, other-phase regions — introduced during processing.

### 3.5 Microscopy & grain size
- **ASTM grain size number G:** `N = 2^(G-1)` — N = grains per square inch at 100x magnification. Higher G = finer grains.
- Techniques: optical microscopy (grains, phases), SEM (fracture surfaces, topography), TEM (dislocations, fine precipitates), AFM (surface profilometry).

---

## 4. Diffusion

### 4.1 Mechanisms
- **Vacancy diffusion** — atom-vacancy site exchange; dominant for substitutional and self-diffusion.
- **Interstitial diffusion** — small atoms (C, N, H) hop between interstitial sites; much faster than vacancy diffusion (smaller atoms, more available sites).

### 4.2 Fick's First Law — steady state
`J = -D * (dC/dx)`
- J = diffusion flux (mass or atoms per unit area per unit time).
- D = diffusion coefficient (m^2/s).
- dC/dx = concentration gradient. Negative sign: flux flows down-gradient (high → low concentration).
- Steady state ⇒ flux and concentration profile do not change with time; dC/dx is constant.

### 4.3 Fick's Second Law — non-steady state
`dC/dt = D * (d^2 C / dx^2)`
Standard solution for a semi-infinite solid with constant surface concentration (e.g. carburizing):
`(C_x - C_0) / (C_s - C_0) = 1 - erf( x / (2*sqrt(D*t)) )`
- C_0 = initial uniform concentration, C_s = surface concentration, C_x = concentration at depth x after time t.
- erf = Gaussian error function (table lookup).
- **Key engineering consequence:** to hold a concentration profile constant while changing temperature, `D*t = constant`.

### 4.4 Temperature dependence — Arrhenius
`D = D_0 * exp(-Q_d / (R*T))`
- D_0 = temperature-independent pre-exponential, Q_d = activation energy for diffusion, R = gas constant, T = absolute temp.
- Plotting `ln(D)` vs `1/T` gives a straight line of slope `-Q_d/R` — the standard way to extract Q_d experimentally.

### 4.5 Worked-example pattern — carburizing
1. Identify C_0, C_s, target C_x, depth x.
2. Get D at the process temperature via Arrhenius.
3. Solve the Fick's-2nd-law erf equation for the erf argument, invert via the erf table to find `x/(2*sqrt(Dt))`.
4. Solve for t (or x, or T).
5. For "equivalent treatment at a different T," set `D1*t1 = D2*t2`.

### 4.6 Pitfalls
- Using temperature in Celsius — must be Kelvin in the Arrhenius exponent.
- Forgetting the sign convention in Fick's first law.
- Interpolating the erf table linearly without checking spacing.

---

## 5. Mechanical Properties & Testing

### 5.1 Stress & strain definitions
- **Engineering stress** `sigma = F / A_0` (original cross-section). **Engineering strain** `epsilon = (l_i - l_0)/l_0`.
- **True stress** `sigma_T = F / A_i` (instantaneous area). **True strain** `epsilon_T = ln(l_i/l_0)`.
- Conversions (valid pre-necking, constant volume): `sigma_T = sigma*(1+epsilon)`, `epsilon_T = ln(1+epsilon)`.
- **Shear:** `tau = F/A_0`, shear strain `gamma = tan(theta)`.

### 5.2 Elastic behavior
- **Hooke's law:** `sigma = E*epsilon`; E = elastic (Young's) modulus = slope of the elastic region.
- **Shear:** `tau = G*gamma`; G = shear modulus.
- **Poisson's ratio:** `nu = -epsilon_lateral / epsilon_axial` (typically 0.25–0.35 for metals; 0.5 is the incompressible limit).
- Isotropic relation: `E = 2*G*(1 + nu)`.
- Elastic modulus is fundamentally set by interatomic bond stiffness (Section 1.2) — **not** changed by alloying or heat treatment to any large degree.

### 5.3 Plastic behavior & tensile-test parameters
- **Yield strength sigma_y** — 0.2% offset method: line parallel to elastic region offset by epsilon = 0.002.
- **Tensile strength (UTS)** — maximum engineering stress; onset of necking.
- **Ductility** — % elongation `%EL = (l_f - l_0)/l_0 * 100`; % reduction in area `%RA = (A_0 - A_f)/A_0 * 100`.
- **Resilience** — modulus of resilience `U_r = sigma_y^2 / (2*E)` = elastic strain energy density absorbed up to yield.
- **Toughness** — total area under the stress-strain curve to fracture (energy per unit volume).
- **Strain hardening** in the plastic region: `sigma_T = K * epsilon_T^n` — K = strength coefficient, n = strain-hardening exponent (0.1–0.5; higher n = more uniform stretching before necking).

### 5.4 Hardness
- Measures resistance to localized plastic indentation. Tests: Rockwell (A/B/C scales), Brinell (HB), Vickers (HV), Knoop (HK).
- For steels, empirically `TS (MPa) ~ 3.45 * HB`.
- Hardness correlates with tensile strength because both reflect resistance to plastic flow.

### 5.5 Property scatter & design
- **Design stress:** `sigma_d = N * sigma_calculated` (N > 1).
- **Safe / working stress:** `sigma_w = sigma_y / N` — N = factor of safety (typically 1.2–4 depending on consequence and confidence).

### 5.6 Pitfalls
- Reporting UTS as "the stress at fracture" — fracture stress is lower (engineering curve) because of necking.
- Confusing stiffness (E, structure-insensitive) with strength (structure-sensitive).
- Applying true-stress conversions past necking — they are invalid there.

---

## 6. Dislocations & Strengthening Mechanisms

### 6.1 Why real strength << theoretical strength
Theoretical shear strength from a sinusoidal interatomic force model: `tau ≈ G/(2*pi)` — on the order of `G/10` (~10 GPa). Measured yield strengths are 10–100 MPa — **2 to 3 orders of magnitude lower**. Resolution: plastic flow proceeds by **dislocation glide**, which moves one row of bonds at a time rather than shearing a whole plane simultaneously (the "rug wrinkle" analogy).

### 6.2 Slip systems & resolved shear stress
- A **slip system** = a slip plane + a slip direction (close-packed plane, close-packed direction).
  - FCC: {111}<110> → 12 systems → very ductile.
  - BCC: {110}<111> (plus others) → 12+ systems but less close-packed → moderate ductility.
  - HCP: {0001}<11-20> → only 3 systems → limited ductility.
- **Schmid's law — resolved shear stress:** `tau_R = sigma * cos(phi) * cos(lambda)`
  - phi = angle between loading axis and slip-plane normal.
  - lambda = angle between loading axis and slip direction.
  - `m = cos(phi)*cos(lambda)` is the **Schmid factor** (max value 0.5 at phi = lambda = 45°).
- **Critical resolved shear stress (CRSS) — tau_crss:** slip begins when `tau_R = tau_crss`. Yield strength of a single crystal: `sigma_y = tau_crss / (cos(phi)*cos(lambda))_max`.
- Polycrystalline approximation: `sigma_y = tau_crss * mbar`, with mbar ≈ 3 for FCC and BCC.

### 6.3 Dislocation strain energy & interactions
- **Screw dislocation strain energy per unit length:** `U_screw = (G*b^2 / (4*pi)) * ln(r/r_0) ≈ G*b^2`.
- **Edge dislocation strain energy:** `U_edge = G*b^2 / (1 - nu)` (somewhat larger than screw because of the dilatational field).
- **Line tension** `T ≈ G*b^2` — dislocations behave like stretched strings; bowing under stress curves to radius `r = G*b / tau`.
- Dislocations of like sign **repel**; opposite sign **attract and annihilate**.

### 6.4 The four strengthening mechanisms
All work by **impeding dislocation motion**. The universal trade-off: increasing strength generally decreases ductility/toughness.

**(a) Grain-size reduction — Hall-Petch:**
`sigma_y = sigma_0 + k_y * d^(-1/2)`
- sigma_0 = lattice friction stress (intrinsic resistance), k_y = strengthening coefficient, d = average grain diameter.
- Mechanism: grain boundaries block slip because slip systems in adjacent grains are misaligned; dislocations **pile up** at boundaries. Finer grains = more boundary area = more obstacles.
- Bonus: fine grains also improve toughness — one of the few mechanisms that raises strength *and* toughness.

**(b) Solid-solution strengthening:**
- Solute atoms create local strain fields. A **smaller substitutional atom** produces a tensile field that attracts the compressive side of a dislocation; a **larger atom** traps the tensile side. Either way the dislocation is pinned.
- Strengthening increment scales roughly with `sqrt(concentration)` and with the size/modulus misfit.
- Interstitial solutes (C, N in Fe) are especially potent (asymmetric tetragonal distortion).

**(c) Strain hardening (work hardening / cold work):**
- Plastic deformation multiplies dislocations; they intersect, form **jogs**, and tangle — dislocations obstruct each other.
- `tau = tau_0 + A*G*b*sqrt(rho)` — rho = dislocation density, A ≈ 0.3–0.6.
- Quantified by **percent cold work:** `%CW = (A_0 - A_d)/A_0 * 100`. Raises sigma_y and TS, lowers ductility.

**(d) Precipitation / dispersion strengthening:**
- Hard second-phase particles obstruct dislocations.
- **Cutting (shearing)** of small coherent particles vs **Orowan looping** around large incoherent particles.
- **Orowan stress:** `tau ≈ G*b / L` — L = inter-particle spacing. Closer particles ⇒ stronger.
- Basis of precipitation-hardened Al alloys (Al-Cu) and maraging steels.

### 6.5 Recovery, recrystallization, grain growth (annealing a cold-worked metal)
1. **Recovery** — dislocation rearrangement/annihilation; relieves internal stress, restores some conductivity; little hardness change.
2. **Recrystallization** — new strain-free equiaxed grains nucleate and grow, consuming the deformed structure. Strength drops, ductility recovers. **Recrystallization temperature** ≈ 0.3–0.6 * T_melt (absolute); lowered by greater prior cold work.
3. **Grain growth** — at higher T/longer time, large grains grow at the expense of small ones to reduce total boundary energy: `d^2 - d_0^2 = K*t`.

### 6.6 Pitfalls
- Treating Hall-Petch as `d^(-1)` — it is `d^(-1/2)`.
- Forgetting that cold work is *erased* by recrystallization.
- Assuming all strengthening mechanisms cost ductility equally — grain refinement is the exception.

---

## 7. Failure: Fracture, Fatigue, Creep

### 7.1 Ductile vs brittle fracture
- **Ductile** — extensive plastic deformation, slow crack propagation, "cup-and-cone" fracture surface with dimples (microvoid coalescence). Energy-absorbing, gives warning.
- **Brittle** — little plastic deformation, rapid crack propagation, flat surface, transgranular (cleavage, "river patterns") or intergranular. Catastrophic, no warning.

### 7.2 Fracture mechanics
- **Stress concentration** at an elliptical flaw tip: `sigma_m = 2*sigma_0 * sqrt(a / rho_t)` — a = half crack length (surface crack: full length), rho_t = tip radius. Stress-concentration factor `K_t = sigma_m/sigma_0`.
- **Griffith critical stress (brittle):** `sigma_c = sqrt( 2*E*gamma_s / (pi*a) )` — gamma_s = specific surface energy.
- **Fracture toughness:** `K_c = Y * sigma * sqrt(pi*a)` — Y = dimensionless geometry factor (~1).
  - **Plane-strain fracture toughness K_IC** — thick-section, mode I, material property (MPa*sqrt(m)).
  - Design criterion: fracture when `Y*sigma*sqrt(pi*a) >= K_IC`. Use it to solve for critical stress *or* critical/detectable flaw size.
- **Ductile-to-brittle transition (DBTT)** — BCC metals (steels) lose toughness sharply below a transition temperature; measured by Charpy/Izod impact testing. FCC metals (Al, Cu, austenitic stainless) do not show a sharp DBTT. Historically responsible for Liberty-ship and pipeline failures.

### 7.3 Fatigue — failure under cyclic load below sigma_y
- **Stress cycle parameters:** mean stress `sigma_m = (sigma_max + sigma_min)/2`; range `Delta_sigma = sigma_max - sigma_min`; amplitude `sigma_a = Delta_sigma/2`; stress ratio `R = sigma_min/sigma_max`.
- **S-N curve** (stress amplitude vs cycles to failure, log N):
  - Ferrous alloys / Ti show a **fatigue (endurance) limit** — below it, effectively infinite life.
  - Al, Cu and most nonferrous alloys show no true limit — characterized by **fatigue strength** at a specified N.
- **Stages:** (1) crack initiation, usually at a surface stress concentration; (2) crack propagation — leaves **beach marks** (macro) and **striations** (micro, one per cycle); (3) final fast fracture.
- **Increasing mean stress shortens fatigue life.** Goodman relation captures the mean-stress effect.
- **Mitigation:** improve surface finish, **shot peening** / carburizing / nitriding (compressive residual surface stress), remove stress raisers, generous fillet radii.

### 7.4 Creep — time-dependent deformation at high T (above ~0.4 * T_melt)
- **Creep curve** (strain vs time at constant load and T):
  1. **Primary (transient)** — decreasing creep rate (strain hardening dominates).
  2. **Secondary (steady-state)** — constant minimum creep rate, the design-relevant region; balance of hardening and recovery.
  3. **Tertiary** — accelerating rate → rupture (necking, void/grain-boundary cavitation).
- **Steady-state creep rate (Weertman-Dorn / power law):**
  `eps_dot_s = A * sigma^n * exp(-Q_c / (R*T))`
  - n = stress exponent (3–8 typical), Q_c = creep activation energy ≈ activation energy for self-diffusion.
- **Larson-Miller parameter** for extrapolating rupture life: `LMP = T*(C + log t_r)` — C ≈ 20; lets short high-T tests predict long-life service behavior.
- **Mitigation:** high-melting-point alloys, large grain size (fewer boundaries to slide — opposite of room-temp strategy!), solid-solution and precipitate strengthening, single-crystal turbine blades.

### 7.5 Pitfalls
- Using the *full* crack length for a surface crack in K_IC — it is the full length for an edge crack but `a` = half-length only for an internal/central crack. Always check geometry and Y.
- Assuming all metals have a fatigue limit (only ferrous/Ti do).
- Carrying over "fine grain = good" to creep — at high T, **coarse** grains resist creep.

---

## 8. Phase Diagrams

### 8.1 Definitions
- **Phase** — a homogeneous portion with uniform physical/chemical characteristics.
- **Component** — pure metals/compounds making up the alloy.
- **Solubility limit** — max solute that dissolves to form a single-phase solid solution.
- **Microstructure** — number, proportion, and spatial arrangement of phases.

### 8.2 Reading a binary diagram
- **Gibbs phase rule:** `P + F = C + N`. For condensed systems at fixed pressure: `P + F = C + 1` — P = phases, F = degrees of freedom, C = components.
- For a point in a **two-phase region:**
  - **Phase compositions** — draw the **tie line** (isotherm) across the two-phase field; read compositions at the intersections with the boundary curves.
  - **Phase amounts — the lever rule:** mass fraction of a phase = (length of tie line on the *opposite* side of the overall composition) / (total tie-line length).
    - `W_L = (C_alpha - C_0)/(C_alpha - C_L)`, `W_alpha = (C_0 - C_L)/(C_alpha - C_L)`.

### 8.3 Invariant reactions (three phases in equilibrium, F = 0)
| Reaction | On cooling | Example |
|----------|-----------|---------|
| Eutectic | L → alpha + beta | Pb-Sn at 61.9 wt% Sn, 183 °C |
| Eutectoid | gamma → alpha + beta | Fe-C: austenite → ferrite + cementite |
| Peritectic | L + alpha → beta | Fe-C peritectic near 0.16 wt% C |
| Monotectic | L1 → alpha + L2 | — |

### 8.4 The Iron-Carbon (Fe-Fe3C) diagram
Phases:
- **Ferrite (alpha)** — BCC iron, max ~0.022 wt% C at 727 °C. Soft, ductile, magnetic.
- **Austenite (gamma)** — FCC iron, max ~2.14 wt% C at 1147 °C. Not stable below 727 °C in plain steel. Higher C solubility (larger interstitial sites in FCC).
- **Delta ferrite** — BCC, high-temperature.
- **Cementite (Fe3C)** — iron carbide, 6.70 wt% C. Hard, brittle, metastable intermetallic.

Key points:
- **Eutectoid:** 0.76 wt% C, 727 °C — `gamma → alpha + Fe3C`. The eutectoid product is **pearlite** (alternating lamellae of ferrite and cementite).
- **Eutectic:** 4.30 wt% C, 1147 °C — `L → gamma + Fe3C` (ledeburite).
- Classification by carbon:
  - **Steels** < 2.14 wt% C: hypoeutectoid (< 0.76), eutectoid (= 0.76), hypereutectoid (> 0.76).
  - **Cast irons** > 2.14 wt% C (practically 3–4.5 wt%).

Microstructure development on slow cooling:
- **Hypoeutectoid steel** — proeutectoid ferrite forms at grain boundaries above 727 °C; remaining austenite (now at 0.76% C) transforms to pearlite at 727 °C.
- **Hypereutectoid steel** — proeutectoid cementite forms at boundaries; remaining austenite → pearlite.
- Use the lever rule twice: once just above 727 °C (proeutectoid phase + austenite), once just below (total ferrite + total cementite, or proeutectoid + pearlite).

### 8.5 Pitfalls
- Applying the lever rule in a single-phase region (it only applies in two-phase fields).
- Confusing eutectic (liquid reactant) with eutectoid (solid reactant).
- Forgetting that the Fe-C diagram is *metastable* — true equilibrium is Fe + graphite.

---

## 9. Phase Transformations & Heat Treatment of Steel

### 9.1 Kinetics
- Transformation rate governed by **nucleation + growth**; overall fraction transformed often follows the **Avrami equation:** `y = 1 - exp(-k*t^n)`.
- **Rate** is often defined as `1 / t_0.5` (reciprocal of time to 50% transformation).

### 9.2 Isothermal transformation (TTT / I-T) and continuous-cooling (CCT) diagrams
Products of austenite decomposition, in order of increasing cooling rate:
- **Coarse pearlite** — slow cooling, high-T transformation; soft, ductile.
- **Fine pearlite** — moderate cooling; harder/stronger than coarse pearlite (thinner lamellae → more ferrite/cementite interface).
- **Bainite** — lower transformation temperature; fine, non-lamellar ferrite + cementite; harder than fine pearlite, still reasonably tough.
- **Martensite** — formed by rapid **quench**; diffusionless, shear transformation of FCC austenite to **BCT (body-centered tetragonal)** with trapped supersaturated carbon. Very hard, very brittle. Forms between M_s (start) and M_f (finish) temperatures — depends on amount of undercooling, *not* time (the martensite line is horizontal on a TTT diagram).
- **Spheroidite** — prolonged heating near 700 °C spheroidizes cementite; the softest, most ductile, most machinable form.

### 9.3 The standard hardening sequence
1. **Austenitize** — heat into the gamma field, hold to dissolve carbon uniformly.
2. **Quench** — cool fast enough to bypass the pearlite/bainite "nose" of the CCT diagram → martensite.
3. **Temper** — reheat the brittle as-quenched martensite (typically 250–650 °C). Martensite → **tempered martensite** (fine cementite particles in a ferrite matrix). Trades some hardness for greatly improved toughness and ductility. Higher tempering temperature / longer time → softer, tougher.

### 9.4 Hardenability
- **Hardenability** = the *depth* to which martensite forms — not the maximum hardness.
- Measured by the **Jominy end-quench test**: a standard bar quenched on one end; hardness vs distance from the quenched end gives the hardenability curve.
- Improved by alloying (Cr, Mo, Ni, Mn) — these shift the CCT nose to longer times, allowing slower quenches.
- **Quenching-medium severity:** brine > water > oil > air (faster quench = deeper hardening but more distortion/cracking risk).

### 9.5 Precipitation (age) hardening (non-ferrous, e.g. Al-Cu)
1. **Solution heat treatment** — heat into single-phase field, dissolve solute.
2. **Quench** — retain a supersaturated solid solution.
3. **Age** (natural at room T, or artificial at elevated T) — fine, coherent precipitates (GP zones → transition phases) form and impede dislocations.
- **Overaging** — too long/too hot: precipitates coarsen, spacing increases, strength falls (Orowan, Section 6.4d).

### 9.6 Pitfalls
- Confusing hardness (intensive, set by C content + structure) with hardenability (depth, set by alloying).
- Thinking martensite forms over time at constant T — it is athermal.
- Skipping the temper — as-quenched martensite is too brittle for service.

---

## 10. Polymers

### 10.1 Structure
- Long-chain macromolecules; **degree of polymerization** = number of repeat (mer) units; **number-** and **weight-average molecular weights** (Mn, Mw); polydispersity index `PDI = Mw/Mn`.
- Chain configurations: linear, branched, crosslinked, network.
- **Stereoisomerism:** isotactic, syndiotactic, atactic — affects crystallizability.
- **Crystallinity** — partial; chains fold into lamellae within spherulites. Higher crystallinity → denser, stiffer, stronger, more solvent-resistant, less transparent.

### 10.2 Classification
- **Thermoplastics** — linear/branched; soften on heating, reprocessable; e.g. PE, PP, PS, PVC, PET, PC, nylon.
- **Thermosets** — heavily crosslinked network; degrade rather than melt; e.g. epoxy, phenolic, polyester, vulcanized rubber.
- **Elastomers** — lightly crosslinked; large reversible elastic strains; rubbery.

### 10.3 Thermal & mechanical behavior
- **Glass transition temperature Tg** — amorphous regions go from glassy (rigid) to rubbery (compliant). **Melting temperature Tm** — crystalline regions.
- Mechanical response strongly **temperature- and strain-rate-dependent** (viscoelastic): below Tg brittle/glassy; near Tg leathery; above Tg rubbery; then viscous flow.
- **Viscoelasticity:** stress relaxation (stress decays at fixed strain), creep (strain grows at fixed stress); relaxation modulus `E_r(t) = sigma(t)/eps_0`.
- Deformation mechanisms: chain uncoiling/sliding, crazing (in glassy polymers).

### 10.4 Pitfalls
- Treating polymer modulus as a constant — it depends heavily on T and loading rate.
- Conflating Tg with Tm — both can exist in a semicrystalline polymer.

---

## 11. Ceramics

### 11.1 Structure & properties
- Ionic + covalent bonding; crystal structure set by **cation/anion radius ratio** (coordination number) and **charge neutrality**. Examples: rock-salt (NaCl, MgO), fluorite (CaF2), perovskite, corundum (Al2O3), silica/silicates (SiO4 tetrahedra).
- **Mechanical:** very high compressive strength and hardness; **brittle** (no dislocation mobility — slip would force like-charged ions together); near-zero ductility; high stiffness; high melting point; chemically inert; thermally/electrically insulating (mostly).
- **Strength is flaw-controlled and scatters widely** → characterized statistically with **Weibull statistics**, not a single value.
- Measured in bending — **flexural strength (modulus of rupture)** — because tensile testing is impractical for brittle materials.

### 11.2 Processing
- Powder-based: pressing + **sintering** (densification by diffusion below the melting point); slip casting; tape casting; hot pressing; glass forming (blowing, pressing, drawing) exploiting the viscosity-temperature curve.
- **Thermal shock** — sudden temperature change induces stresses; resistance improves with high thermal conductivity, low thermal expansion, low modulus.

### 11.3 Pitfalls
- Quoting a single "strength" for a ceramic — always think distribution.
- Forgetting ceramics are strong in compression but weak in tension.

---

## 12. Composites

### 12.1 Classification
- **By matrix:** polymer-matrix (PMC), metal-matrix (MMC), ceramic-matrix (CMC).
- **By reinforcement:** particle-reinforced (large-particle, dispersion-strengthened), fiber-reinforced (continuous/aligned, discontinuous/aligned, discontinuous/random), structural (laminates, sandwich panels).

### 12.2 Rule of mixtures — continuous aligned fibers
- **Longitudinal modulus (isostrain, fibers + matrix strain equally):**
  `E_cl = E_f * V_f + E_m * V_m` with `V_f + V_m = 1`.
- **Transverse modulus (isostress):**
  `1/E_ct = V_f/E_f + V_m/E_m`.
- **Load partition (longitudinal):** `F_f / F_m = (E_f * V_f) / (E_m * V_m)`.
- Longitudinal properties are **fiber-dominated**; transverse properties are **matrix-dominated** → strong anisotropy.

### 12.3 Design notes
- Fibers carry load; matrix transfers load between fibers, protects them, and sets transverse/shear behavior.
- **Critical fiber length** `l_c = sigma_f* * d / (2*tau_c)` — fibers shorter than l_c pull out rather than break; longer fibers approach continuous-fiber efficiency.
- Specific stiffness/strength (property per unit density) is the headline advantage — basis of aerospace CFRP.

### 12.4 Pitfalls
- Using the isostrain formula for transverse loading (or vice versa).
- Ignoring anisotropy — composite properties are direction-dependent.

---

## 13. Electrical, Thermal & Magnetic Properties

### 13.1 Electrical
- **Ohm's law (material form):** `J = sigma * E_field`; conductivity `sigma = n*|e|*mu_e` (n = carrier density, mu_e = electron mobility); resistivity `rho = 1/sigma`.
- **Band theory:** conductors (overlapping/partly filled bands), semiconductors (small band gap, ~1 eV), insulators (large band gap, > ~2 eV).
- **Matthiessen's rule:** `rho_total = rho_thermal + rho_impurity + rho_deformation` — total resistivity is the sum of independent scattering contributions. Resistivity rises with temperature, impurity content, and cold work.
- **Semiconductors:** intrinsic vs extrinsic; **n-type** (donor dopants, e.g. P in Si) and **p-type** (acceptor dopants, e.g. B in Si); carrier concentration increases with temperature (opposite trend to metals).

### 13.2 Thermal
- **Heat capacity** `C = dQ/dT`; specific heat `c`. Dulong-Petit limit `C_v ≈ 3R` at high T.
- **Thermal expansion:** `Delta_L / L_0 = alpha_l * Delta_T` — alpha_l = linear coefficient of thermal expansion; rooted in anharmonicity of the interatomic potential (Section 1.2).
- **Thermal conductivity** `q = -k * (dT/dx)` (Fourier's law). In metals, free electrons dominate heat transport ⇒ **Wiedemann-Franz law:** `k / (sigma * T) = L` (Lorenz number ≈ constant). In ceramics/polymers, phonons (lattice vibrations) carry the heat.
- **Thermal stress** (constrained bar): `sigma = E * alpha_l * Delta_T`.

### 13.3 Magnetic
- **B = mu_0*(H + M)**; magnetization `M = chi_m * H`; permeability `mu = B/H`.
- Types: diamagnetic, paramagnetic, **ferromagnetic** (Fe, Co, Ni), antiferromagnetic, ferrimagnetic (ferrites).
- **Curie temperature** — ferromagnetism is lost above it. **Hysteresis loop** — soft magnets (thin loop, low loss, transformers) vs hard magnets (fat loop, high coercivity, permanent magnets).

### 13.4 Pitfalls
- Expecting metal and semiconductor conductivity to respond the same way to temperature — they move in opposite directions.
- Forgetting cold work and impurities raise resistivity (Matthiessen).

---

## 14. Corrosion & Degradation

### 14.1 Electrochemistry of corrosion
- Corrosion = electrochemical: **anode** (oxidation, metal loss: `M → M^n+ + n*e-`) + **cathode** (reduction: hydrogen evolution `2H+ + 2e- → H2`, or oxygen reduction).
- **Standard EMF / galvanic series** rank metals by tendency to corrode; the more anodic (active) metal corrodes preferentially when two are coupled.
- **Nernst equation** corrects electrode potential for non-standard ion concentration.
- **Faraday's law** — corrosion rate is proportional to current density; **corrosion penetration rate (CPR)** expresses metal loss as thickness/time (mpy or mm/yr).

### 14.2 Forms of corrosion
Uniform attack; **galvanic** (dissimilar-metal couple); **crevice** (depleted-oxygen occluded regions); **pitting** (localized, autocatalytic, very dangerous — small mass loss, deep penetration); **intergranular** (grain-boundary attack — e.g. sensitized stainless steel with Cr-carbide precipitation depleting boundary Cr); **selective leaching** (dezincification of brass); **erosion-corrosion**; **stress-corrosion cracking** (tensile stress + corrosive environment); **hydrogen embrittlement**.

### 14.3 Passivation & protection
- **Passivation** — some metals (stainless steel, Al, Ti, Cr) form a thin, adherent, self-healing oxide film that drastically slows further attack.
- **Protection methods:**
  - Material selection / proper alloying.
  - **Cathodic protection** — make the structure the cathode: sacrificial anode (Mg, Zn — galvanizing is sacrificial Zn on steel) or impressed current.
  - Coatings, paints, inhibitors.
  - Design: avoid crevices, dissimilar-metal contact, stagnant zones; allow drainage.
- **Ceramics** are largely corrosion-resistant (already oxidized/stable). **Polymers** degrade by swelling, dissolution, UV/thermal scission rather than electrochemical corrosion.

### 14.4 Pitfalls
- Assuming uniform corrosion is the worst case — localized forms (pitting, SCC) cause sudden failure with little total mass loss.
- Coupling dissimilar metals in design without considering relative areas — a small anode + large cathode is the worst geometry (high anodic current density).

---

## Quick-Reference Equation Sheet

| Quantity | Equation |
|----------|----------|
| Vacancy concentration | N_v/N = exp(-Q_v/(k*T)) |
| Theoretical density | rho = n*A/(V_C*N_A) |
| Bragg's law | n*lambda = 2*d*sin(theta) |
| Interplanar spacing (cubic) | d = a/sqrt(h^2+k^2+l^2) |
| Fick's 1st law | J = -D*(dC/dx) |
| Fick's 2nd law (solution) | (Cx-C0)/(Cs-C0) = 1 - erf(x/(2*sqrt(D*t))) |
| Diffusivity (Arrhenius) | D = D0*exp(-Qd/(R*T)) |
| Hooke's law | sigma = E*epsilon |
| Isotropic elasticity | E = 2*G*(1+nu) |
| True stress / strain | sigma_T = sigma*(1+eps); eps_T = ln(1+eps) |
| Strain hardening | sigma_T = K*eps_T^n |
| Modulus of resilience | U_r = sigma_y^2/(2*E) |
| Schmid's law | tau_R = sigma*cos(phi)*cos(lambda) |
| Hall-Petch | sigma_y = sigma_0 + k_y*d^(-1/2) |
| Forest hardening | tau = tau_0 + A*G*b*sqrt(rho) |
| Orowan stress | tau = G*b/L |
| Stress concentration | sigma_m = 2*sigma_0*sqrt(a/rho_t) |
| Griffith stress | sigma_c = sqrt(2*E*gamma_s/(pi*a)) |
| Fracture toughness | K_c = Y*sigma*sqrt(pi*a) |
| Steady-state creep | eps_dot = A*sigma^n*exp(-Q_c/(R*T)) |
| Larson-Miller | LMP = T*(C + log t_r) |
| Lever rule | W_alpha = (C_0 - C_L)/(C_alpha - C_L) |
| Gibbs phase rule | P + F = C + N |
| Avrami | y = 1 - exp(-k*t^n) |
| Composite E (isostrain) | E_cl = E_f*V_f + E_m*V_m |
| Composite E (isostress) | 1/E_ct = V_f/E_f + V_m/E_m |
| Critical fiber length | l_c = sigma_f*d/(2*tau_c) |
| Matthiessen's rule | rho = rho_th + rho_imp + rho_def |
| Thermal expansion | dL/L0 = alpha_l*dT |
| Thermal stress (constrained) | sigma = E*alpha_l*dT |
| Fourier's law | q = -k*(dT/dx) |
| Wiedemann-Franz | k/(sigma*T) = L |

---

## Open-source sources used

- **Roylance, D., *Mechanics of Materials* (MIT OpenCourseWare 3.11 / 3.21 modules)**, hosted on Engineering LibreTexts — "Dislocation Basis of Yield and Creep," "Yield and Fracture" chapters. https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_of_Materials_(Roylance) and https://web.mit.edu/course/3/3.11/www/modules/
- **Engineering LibreTexts — Materials Science bookshelves** (strengthening mechanisms, Hall-Petch, solid-solution strengthening, diffusion). https://eng.libretexts.org/Bookshelves/Materials_Science
- **MIT OpenCourseWare 3.091 — Introduction to Solid State Chemistry** (atomic bonding, crystal structures, defects, band theory). https://ocw.mit.edu/courses/3-091sc-introduction-to-solid-state-chemistry-fall-2010/
- **DoITPoMS, University of Cambridge — Teaching and Learning Packages** (crystallography, dislocations, phase diagrams, diffusion). https://www.doitpoms.ac.uk/
- General open-courseware Callister-aligned lecture material from public university repositories (Colorado State, Mustansiriyah) for chapter structure on dislocations and strengthening mechanisms.
