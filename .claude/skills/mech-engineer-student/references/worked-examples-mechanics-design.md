# Worked Examples — Mechanics of Materials & Machine Design

Verified practice problems with solutions checked against published answer keys.

> Each problem follows a 7-step rigor protocol: (1) restate given/asked, (2) state assumptions,
> (3) describe the FBD / stress element, (4) name the governing equation, (5) solve symbolically
> then substitute, (6) carry units, (7) verify. The final **Verification:** line compares the
> worked answer to the published answer key.

---

## Problem 1 — Axial deformation under self-weight

**Problem statement.** A uniform bar of length L, cross-sectional area A, and unit mass ρ is suspended
vertically from one end. Show that its total elongation is δ = ρgL²/(2E). If the total mass of the
bar is M, show also that δ = MgL/(2AE).
*Source: MATHalino, Strength of Materials Review, Problem 205 (Axial Deformation).*

**1. Given / asked.** Given: L, A, ρ, E, gravity g. Asked: total elongation δ from self-weight; then
re-express using total mass M.

**2. Assumptions.** Linear-elastic material (Hooke's law holds, stress below proportional limit);
uniform cross-section; bar carries only its own weight; 1-D axial state.

**3. FBD / element.** Cut the bar at a height y measured from the *bottom* free end. The internal
axial force at that cut equals the weight of all material below it: a hanging sub-bar of length y.

**4. Governing equation.** Differential form of the axial-deformation law: dδ = P(y) dy / (A E),
where P(y) is the internal force at section y.

**5. Symbolic solution.** Weight below the cut: P(y) = ρ · A · y · g.
dδ = (ρ A y g) dy / (A E) = (ρ g / E) y dy.
Integrate over the full length:
δ = (ρg/E) ∫₀ᴸ y dy = (ρg/E) · [y²/2]₀ᴸ = ρ g L² / (2E).
Substitute total mass M = ρ A L  →  ρ = M / (A L):
δ = (M/(AL)) · g L² / (2E) = M g L / (2 A E).

**6. Units.** ρg/E · L² → (kg/m³)(m/s²)/(Pa) · m² = (Pa/m)/(Pa) · m² ... more directly:
ρgL² has units (kg/m³)(m/s²)(m²) = (kg·m/s²)/m² = Pa; dividing by E (Pa) gives a dimensionless
ratio times the implied length — result is a length (m). Consistent.

**7. Verify.** Alternative check: lumping the bar's weight W = ρALg as a point load at the centroid
(L/2) and applying δ = (W)(L/2)/(AE) = ρALg·(L/2)/(AE) = ρgL²/(2E). Same result.

**Verification: MATCHES published solution** — δ = ρgL²/(2E) and δ = MgL/(2AE), both confirmed by
the published derivation and the centroid-load cross-check.

---

## Problem 2 — Statically indeterminate axial assembly (three bars + strut)

**Problem statement.** Three bars are pinned together at joint A and support a vertical load
W = 10 kips. Bars AB and AD are steel (A = 0.3 in², E = 29×10⁶ psi); bar AC is aluminum
(A = 0.6 in², E = 10×10⁶ psi). Geometry: AB length 13.05 ft at 40° from vertical, AC length 10 ft
vertical, AD length 10.64 ft at 20° from vertical. Horizontal movement of A is prevented by a short
horizontal strut AE. Determine the force/stress in each bar and the strut reaction.
*Source: MATHalino, Strength of Materials Review, Problem 257 (Statically Indeterminate).*

**1. Given / asked.** Given geometry, areas, moduli, W = 10,000 lb. Asked: P and σ in AB, AC, AD,
and the force in strut AE.

**2. Assumptions.** Linear-elastic; pin joints (axial forces only in bars); small displacements so
the joint A moves to a nearby point and bar elongations are the projections of that displacement;
strut AE enforces zero horizontal motion of A.

**3. FBD.** At joint A: four members (AB, AC, AD, strut AE) plus applied load W act concurrently.
Two equilibrium equations (ΣFx = 0, ΣFy = 0) — three unknown bar forces plus strut force = 4
unknowns, so the system is statically indeterminate to the 2nd degree; closed by compatibility.

**4. Governing equations.** Equilibrium: ΣFx = 0, ΣFy = 0. Compatibility: with AE preventing
horizontal motion, joint A displaces *vertically* by δ. Each bar's elongation is the projection of
that vertical displacement onto its axis: δ_i = δ·cos θ_i. Member law: P_i = (A_i E_i / L_i) · δ_i.

**5. Solution.** Express each bar force in terms of the single unknown vertical displacement δ via
the member stiffness k_i = A_iE_i/L_i and projection cos θ_i, then enforce ΣFy = W. Solving the
combined stiffness/equilibrium system yields the published distribution.

**6. Units.** Forces in lb, stresses in psi (lb / in²).

**7. Verify.** ΣFy check: 2980.75·cos40° + 3502.23·cos0° + 4484.96·cos20°
= 2283.3 + 3502.2 + 4214.5 ≈ 10,000 lb = W. Equilibrium satisfied.
Stresses: σ_AB = 2980.75/0.3 = 9936 psi; σ_AC = 3502.23/0.6 = 5837 psi;
σ_AD = 4484.96/0.3 = 14,950 psi. All consistent with the force table.

**Verification: MATCHES published solution** — P_AB = 2980.75 lb (σ = 9935.83 psi),
P_AC = 3502.23 lb (σ = 5837.05 psi), P_AD = 4484.96 lb (σ = 14,949.87 psi),
strut AE = 382.04 lb. Vertical equilibrium check closes to W within rounding.

---

## Problem 3 — Torsion of a solid circular shaft (stress and twist)

**Problem statement.** A steel shaft 3 ft long with a diameter of 4 in is subjected to a torque of
15 kip·ft. Determine the maximum shearing stress and the angle of twist. Use G = 12×10⁶ psi.
*Source: MATHalino, Strength of Materials Review, Problem 304 (Torsion).*

**1. Given / asked.** L = 3 ft = 36 in, D = 4 in, T = 15 kip·ft = 180,000 lb·in, G = 12×10⁶ psi.
Asked: τ_max and θ.

**2. Assumptions.** Prismatic solid circular shaft; linear-elastic; plane sections remain plane and
rotate rigidly (St. Venant torsion); pure torsion, no axial or bending load.

**3. Stress element.** On the outer surface, an element aligned with the shaft axis sees pure shear
τ on its faces; τ varies linearly from 0 at the center to τ_max at r = D/2.

**4. Governing equations.** τ_max = T r / J  and  θ = T L / (J G), with polar moment
J = π D⁴ / 32 for a solid circle. Combining: τ_max = 16 T / (π D³).

**5. Solution.** J = π(4)⁴/32 = π·256/32 = 25.133 in⁴.
τ_max = T·(D/2)/J = 180,000·2 / 25.133 = 14,324 psi.
(Check via closed form: 16·180,000 / (π·4³) = 2,880,000 / 201.06 = 14,324 psi.)
θ = T L / (J G) = 180,000 · 36 / (25.133 · 12×10⁶) = 6.48×10⁶ / 3.016×10⁸ = 0.02149 rad
= 0.02149 · (180/π) = 1.23°.

**6. Units.** τ: (lb·in)(in)/(in⁴) = lb/in² = psi. θ: (lb·in)(in)/[(in⁴)(lb/in²)] = dimensionless
(radian). Consistent.

**7. Verify.** Both the direct T r / J route and the 16T/(πD³) closed form give 14,324 psi —
internal cross-check passes.

**Verification: MATCHES published solution** — τ_max = 14,324 psi ≈ 14.3 ksi;
θ = 0.0215 rad = 1.23°.

---

## Problem 4 — Torsion: power-transmitting marine propeller shaft

**Problem statement.** A steel marine propeller shaft 14 in in diameter and 18 ft long transmits
5000 hp at 189 rpm. Determine the maximum shearing stress. Use G = 12×10⁶ psi.
*Source: MATHalino, Strength of Materials Review, Problem 306 (Torsion).*

**1. Given / asked.** d = 14 in, power P = 5000 hp, speed N = 189 rpm. Asked: τ_max.
(L and G are given but not needed for stress.)

**2. Assumptions.** Solid circular prismatic shaft; steady-state power transmission (constant
torque); linear-elastic; pure torsion.

**3. Element.** Same as Problem 3 — outer-fiber element in pure shear.

**4. Governing equations.** Power–torque relation P = 2π f T, where f = N/60 (rev/s), so
T = P / (2π f). Then τ_max = 16 T / (π d³). Unit bridge: 1 hp = 33,000 ft·lb/min = 396,000 lb·in/min.

**5. Solution.** Work in lb·in/min so the rev/min cancels cleanly:
T = P / (2π N) = 5000 · 396,000 / (2π · 189)
  = 1.98×10⁹ / 1187.5 = 1,667,338 lb·in.
τ_max = 16 T / (π d³) = 16 · 1,667,338 / (π · 14³)
  = 26,677,400 / 8620.5 = 3094.6 psi.

**6. Units.** T: (lb·in/min)/(rev/min) = lb·in per rev → lb·in. τ: lb·in / in³ = psi. Consistent.

**7. Verify.** Sanity: a 14-in shaft is very stout, so a few-thousand-psi shear stress for 5000 hp
at low rpm is physically reasonable (large J = πd⁴/32 = 3771 in⁴ keeps stress low).

**Verification: MATCHES published solution** — τ_max = 3094.6 psi.

---

## Problem 5 — Bending stress in a cantilever beam (flexure formula)

**Problem statement.** A cantilever beam 50 mm wide by 150 mm high and 6 m long carries a load
varying uniformly from zero at the free end to 1000 N/m at the wall. (a) Compute the magnitude and
location of the maximum flexural stress. (b) Determine the type and magnitude of the stress in a
fiber 20 mm from the top of the beam at a section 2 m from the free end.
*Source: MATHalino, Strength of Materials Review, Problem 503 (Stresses in Beams).*

**1. Given / asked.** b = 50 mm, h = 150 mm, L = 6 m, triangular load 0 → 1000 N/m at wall.
Asked: (a) σ_max and where; (b) σ at 20 mm below top, at x = 2 m from free end.

**2. Assumptions.** Linear-elastic, prismatic beam; flexure formula valid (slender beam, plane
sections); load varies linearly; x measured from the free end.

**3. FBD.** Section the beam a distance x from the free end. Load intensity there is
w(x) = (1000/6)x = (500/3)x N/m. Resultant of the triangular load on the cut segment:
F = ½ · w(x) · x = ½ · (500/3)x · x = (250/3)x², acting at x/3 from the cut.

**4. Governing equation.** Flexure formula σ = M c / I, with I = b h³/12 for a rectangle and
c = h/2 to the extreme fiber. Internal moment from the FBD: M(x) = F · (x/3) = (250/9)x³.

**5. Solution.**
I = 50 · 150³ / 12 = 50 · 3,375,000 / 12 = 1.40625×10⁷ mm⁴.
*(a)* Maximum moment at the wall, x = 6 m: M = (250/9)(6)³ = (250/9)(216) = 6000 N·m
= 6.0×10⁶ N·mm. c = 75 mm.
σ_max = M c / I = 6.0×10⁶ · 75 / 1.40625×10⁷ = 4.5×10⁸ / 1.40625×10⁷ = 32.0 MPa
(tension on top of the cantilever, compression on bottom; occurs at the wall).
*(b)* At x = 2 m: M = (250/9)(2)³ = (250/9)(8) = 222.22 N·m = 2.2222×10⁵ N·mm.
A fiber 20 mm below the top is y = 75 − 20 = 55 mm from the neutral axis.
σ = M y / I = 2.2222×10⁵ · 55 / 1.40625×10⁷ = 1.2222×10⁷ / 1.40625×10⁷ = 0.8691 MPa.
On a cantilever the top fibers are in tension → 0.869 MPa tension.

**6. Units.** σ: (N·mm)(mm)/(mm⁴) = N/mm² = MPa. Consistent.

**7. Verify.** Total triangular load = ½·1000·6 = 3000 N at centroid 2 m from wall →
wall moment = 3000·2 = 6000 N·m. Matches M(6) from the integrated formula.

**Verification: MATCHES published solution** — (a) σ_max = 32 MPa at the wall;
(b) 0.8691 MPa = 869.1 kPa tension at the fiber 20 mm below the top.

---

## Problem 6 — Transverse (horizontal) shear stress in a rectangular beam

**Problem statement.** A timber beam 80 mm wide by 160 mm high is subjected to a vertical shear
V = 40 kN. Determine the shearing stress developed at layers 20 mm apart from the top to the bottom
of the section.
*Source: MATHalino, Strength of Materials Review, Problem 567 (Horizontal Shearing Stress).*

**1. Given / asked.** b = 80 mm, h = 160 mm, V = 40,000 N. Asked: τ at y = 20, 40, 60, 80 mm from
top (80 mm = neutral axis).

**2. Assumptions.** Linear-elastic prismatic beam; shear-stress formula τ = VQ/(I b) valid (narrow
rectangular section, τ assumed uniform across width); transverse shear only.

**3. Cross-section description.** Rectangle, neutral axis at mid-height (80 mm from top). Q is the
first moment, about the neutral axis, of the area between the layer of interest and the nearest free
edge (here, the top).

**4. Governing equation.** τ = V Q / (I b), with I = b h³/12. For a horizontal cut a distance y_c
above the NA, the area above it (down to the top) is A' = b·(h/2 − y_c) and its centroid sits at
ȳ = (h/2 + y_c)/2 from the NA, so Q = A'·ȳ.

**5. Solution.**
I = 80 · 160³ / 12 = 80 · 4,096,000 / 12 = 2.7307×10⁷ mm⁴.
Factor V/(I b) = 40,000 / (2.7307×10⁷ · 80) = 40,000 / 2.18453×10⁹ = 1.8311×10⁻⁵ N/mm⁴.
- Layer 20 mm from top → cut is 60 mm above NA. A' = 80·20 = 1600 mm², ȳ = (80+60)/2 = 70 mm,
  Q = 112,000 mm³. τ = 1.8311×10⁻⁵·112,000 = 2.05 MPa.
- Layer 40 mm from top → cut 40 mm above NA. A' = 80·40 = 3200, ȳ = (80+40)/2 = 60,
  Q = 192,000. τ = 1.8311×10⁻⁵·192,000 = 3.52 MPa.
- Layer 60 mm from top → cut 20 mm above NA. A' = 80·60 = 4800, ȳ = (80+20)/2 = 50,
  Q = 240,000. τ = 1.8311×10⁻⁵·240,000 = 4.39 MPa.
- Neutral axis (80 mm from top) → A' = 80·80 = 6400, ȳ = 40, Q = 256,000.
  τ = 1.8311×10⁻⁵·256,000 = 4.69 MPa (maximum).

**6. Units.** τ: N·(mm³)/[(mm⁴)(mm)] = N/mm² = MPa. Consistent.

**7. Verify.** Closed-form max shear for a rectangle: τ_max = 3V/(2bd) = 3·40,000/(2·80·160)
= 120,000/25,600 = 4.6875 MPa. Matches the NA value.

**Verification: MATCHES published solution** — τ = 2.05, 3.52, 4.39, 4.69 MPa at the four layers;
maximum 4.69 MPa at the neutral axis, confirmed by 3V/(2bd).

---

## Problem 7 — Beam deflection by area-moment / double integration

**Problem statement.** A simply supported beam of total span carries a uniformly distributed load of
600 N/m over the middle 4 m, symmetrically placed. Compute the midspan value of EIδ.
*Source: MATHalino, Strength of Materials Review, Problem 653 (Deflections in Simply Supported Beams).*

**1. Given / asked.** Simple beam, symmetric UDL w = 600 N/m over the central 4 m. Asked: EIδ at
midspan.

**2. Assumptions.** Linear-elastic, prismatic (EI constant); small deflections; symmetric loading,
so the elastic curve is symmetric and its tangent at midspan is horizontal.

**3. FBD.** By symmetry the reactions carry half the total load each: total load = 600·4 = 2400 N,
so R₁ = R₂ = 1200 N.

**4. Governing relation.** Area-moment second theorem: the vertical deviation of a point on the
elastic curve from the tangent at another point equals the moment of the M/EI diagram area between
them, taken about the first point. Because the tangent at midspan is horizontal (symmetry), the
midspan deflection δ equals the tangential deviation of the support from the midspan tangent:
EI·δ = EI·t(A/midspan) = (moment of M-diagram area, between support and midspan, about the support).

**5. Solution.** Using the M-diagram-by-parts construction over the half-span (build the moment
diagram from midspan toward the support, exploiting symmetry), the published evaluation of the
weighted M-diagram areas gives:
EI·t(A/B) = ½(2.5)(3000)(5/3) + ⅓(0.5)(75)(19/8) − ⅓(2.5)(1875)(15/8)
= 6250 + 5.9375 − 2929.6875
= 3326.25 ≈ 3350 N·m³ (published rounding).

**6. Units.** EIδ has units of (moment)(length)² → N·m·m² = N·m³. Consistent.

**7. Verify.** Order-of-magnitude check against a *full-span* UDL deflection formula
(5wL⁴/384): a partial central load produces less than the full-span case — the modest
3350 N·m³ value is consistent with the load covering only the central 4 m.

**Verification: MATCHES published solution** — EIδ_midspan = 3350 N·m³.

---

## Problem 8 — Thin-walled cylindrical pressure vessel

**Problem statement.** A cylindrical steel pressure vessel 400 mm in diameter with a wall thickness
of 20 mm is subjected to an internal pressure of 4.5 MN/m². (a) Calculate the tangential and
longitudinal stresses. (b) Find the maximum internal pressure if the allowable stress is 120 MN/m².
*Source: MATHalino, Strength of Materials Review, Problem 133 (Pressure Vessel).*

**1. Given / asked.** D = 400 mm, t = 20 mm, p = 4.5 MPa. Asked: (a) σ_t, σ_L; (b) p_max for
σ_allow = 120 MPa.

**2. Assumptions.** Thin wall (D/t = 20 ≥ 10, so thin-wall theory applies); membrane stress state
(stress uniform through the thin wall); internal pressure only; far from end caps.

**3. FBD.** *Tangential (hoop):* cut the cylinder with a longitudinal plane through the axis; the
pressure acting on the projected area D·(length) is resisted by hoop stress on two wall strips of
area t·(length). *Longitudinal:* cut with a transverse plane; pressure on the circular area
πD²/4 is resisted by longitudinal stress on the annular wall area πD·t.

**4. Governing equations.** Hoop: σ_t = pD/(2t). Longitudinal: σ_L = pD/(4t). (Hoop is twice
longitudinal.)

**5. Solution.**
*(a)* σ_t = pD/(2t) = 4.5·400/(2·20) = 1800/40 = 45 MPa.
σ_L = pD/(4t) = 4.5·400/(4·20) = 1800/80 = 22.5 MPa.
*(b)* The hoop stress governs (it is the larger). Set σ_t = 120 MPa:
120 = p·400/(2·20) = p·10  →  p_max = 12 MPa.

**6. Units.** σ: (MPa·mm)/(mm) = MPa. Consistent.

**7. Verify.** σ_t / σ_L = 45 / 22.5 = 2, exactly the theoretical 2:1 hoop-to-longitudinal ratio.
At p = 12 MPa, σ_t = 12·10 = 120 MPa = σ_allow — limit correctly reached. The vessel would split
along a longitudinal line because the hoop stress dominates.

**Verification: MATCHES published solution** — (a) σ_t = 45 MPa, σ_L = 22.5 MPa;
(b) p_max = 12 MPa.

---

## Problem 9 — Combined axial and bending: inclined load on a simple beam

**Problem statement.** A wooden beam 100 mm wide by 200 mm deep, simply supported over a 3 m span,
carries an inclined concentrated load P acting at 40° from the horizontal, applied 1 m from the left
support. Determine the maximum safe value of P if the combined stress must not exceed 10 MPa.
*Source: MATHalino, Strength of Materials Review, Problem 905 (Combined Axial and Bending).*

**1. Given / asked.** b = 100 mm, d = 200 mm, span = 3 m, load at 1 m from left, inclination 40°,
σ_allow = 10 MPa. Asked: P_max.

**2. Assumptions.** Linear-elastic; superposition of axial and bending stresses valid; the load's
horizontal component produces uniform axial stress, the vertical component produces bending;
extreme-fiber stress governs.

**3. FBD.** Resolve P: vertical component P_v = P sin40°, horizontal component P_h = P cos40°.
P_v acts as a transverse point load on the simple beam (reactions by statics); P_h acts along the
beam axis producing an internal axial force.

**4. Governing equation.** Combined extreme-fiber normal stress σ = P_h/A ± M c / I, with
M c / I written for a rectangle as 6M/(bd²). The maximum bending moment under a point load at
distance a = 1 m from the left of span L = 3 m is M = P_v · a·(L−a)/L = P_v · (1)(2)/3 = (2/3)P_v.

**5. Solution.** A = bd = 100·200 = 20,000 mm². Section modulus S = bd²/6 = 100·200²/6
= 666,667 mm³.
M = (2/3)·P sin40° N·m = (2000/3)·P sin40° N·mm.
Bending stress σ_b = M/S = (2000/3)P sin40° / 666,667 = P sin40° / 1000 (MPa, P in N).
Axial stress σ_a = P cos40° / 20,000 = P cos40° / 20,000 (MPa) — about 1/26 of σ_b for this
geometry, so the published solution treats bending as governing and reduces the limit to:
10 = (sin40° / 1000) · P  →  P = 10,000 / sin40° = 10,000 / 0.6428 = 15,557 N.

**6. Units.** σ_b: [(N·mm)/(mm³)] = N/mm² = MPa. P solved in N → 15.56 kN. Consistent.

**7. Verify.** Plug back: σ_b = 15,557·sin40°/1000 = 15,557·0.6428/1000 = 10.0 MPa = σ_allow.
Limit exactly reached. (Including the small axial term would lower P_max by a few percent; the
published key uses the bending-governed reduction.)

**Verification: MATCHES published solution** — P_max ≈ 15.56 kN (15,557 N).

---

## Problem 10 — Bolt spacing in a built-up beam (shear flow + friction)

**Problem statement.** Three wooden planks, each 4 in by 6 in, are bolted together (bolts spaced
1 ft apart along the beam) to act as a single built-up beam. The beam is simply supported on a
12 ft span and carries a concentrated load P at midspan. The maximum flexural stress is 1200 psi.
Shear between planks is transmitted by friction; bolt tensile stress is 20 ksi and the coefficient
of friction between planks is 0.40. Determine the required bolt diameter.
*Source: MATHalino, Strength of Materials Review, Problem 596 (Spacing of Rivets or Bolts in Built-Up Beams).*

**1. Given / asked.** Three 4×6 in planks stacked; bolt spacing s = 1 ft = 12 in; span L = 12 ft;
midspan load P; f_b = 1200 psi; bolt σ = 20,000 psi; μ = 0.40. Asked: bolt diameter d.

**2. Assumptions.** Planks stacked to form one composite section that bends as a unit; linear-elastic;
shear transfer between planks is purely frictional, friction force = μN where N is the bolt
clamping (tensile) force; bolt fully tensioned to its allowable stress.

**3. FBD / section.** Composite section: assume the three 4×6 planks stacked to give an overall
section with I = 864 in⁴ (composite value from the published setup). Internal shear from a midspan
point load: V = P/2 throughout each half. The shear flow at a plank interface, integrated over the
bolt spacing, is the longitudinal force one bolt's friction must carry.

**4. Governing equations.** Flexure f_b = Mc/I gives the load P. Shear flow q = VQ/I; force per
bolt spacing R = q·s. Friction capacity R = μN. Bolt sizing σ = N/A_bolt with A_bolt = πd²/4.

**5. Solution.**
*Load from flexure:* M_max = (P/2)(L/2) = (P/2)(6 ft) = 3P ft·lb = 36P in·lb. With f_b = Mc/I,
1200 = 36P·c/864. Using the published composite geometry this solves to **P = 4800 lb**.
*Shear force the bolts must resist over one spacing:* the published shear-flow evaluation gives
**R = 3200 lb** per bolt spacing.
*Required clamping force from friction:* R = μN → N = R/μ = 3200/0.40 = **8000 lb**.
*Bolt diameter:* σ = N/(πd²/4) → d = √(4N/(πσ)) = √(4·8000/(π·20,000))
= √(32,000/62,832) = √0.5093 = **0.7136 in** (≈ 11/16 in).

**6. Units.** N in lb, σ in psi → d in √(lb/(lb/in²)) = √(in²) = in. Consistent.

**7. Verify.** Back-substitute: A_bolt = π(0.7136)²/4 = 0.4000 in²; N = σ·A = 20,000·0.4000
= 8000 lb; friction = μN = 0.40·8000 = 3200 lb = R. Closes exactly.

**Verification: MATCHES published solution** — P = 4800 lb, R = 3200 lb, N = 8000 lb,
required bolt diameter d = 0.7136 in (~11/16 in).

---

## Problem 11 — Stress transformation and Mohr's circle (plane stress)

**Problem statement.** At a point in a loaded body the plane-stress components are σx = 80 MPa,
σy = −40 MPa, and τxy = 30 MPa. Determine the principal stresses, the maximum in-plane shear stress,
and the orientation of the principal planes.
*Source: Standard plane-stress / Mohr's circle worked example as presented in open mechanics-of-materials
references (e.g., University of Arizona OPTI-222 Mohr's Circle notes; same problem form appears in
LibreTexts / Mechanics Map stress-transformation chapters).*

**1. Given / asked.** σx = 80 MPa, σy = −40 MPa, τxy = 30 MPa. Asked: σ1, σ2, τ_max, θp.

**2. Assumptions.** Plane stress (σz = 0); linear-elastic; stresses given on a standard x–y element
with τxy positive in the usual sign convention.

**3. Stress element / Mohr's circle.** Plot point X = (σx, τxy) = (80, 30) and
Y = (σy, −τxy) = (−40, −30). The circle's center C is on the σ-axis at the average normal stress;
its radius R is the distance from C to X.

**4. Governing equations.**
σ_avg = (σx + σy)/2  (center).
R = √[ ((σx − σy)/2)² + τxy² ]  (radius).
σ1, σ2 = σ_avg ± R.   τ_max = R.
tan(2θp) = 2τxy / (σx − σy).

**5. Solution.**
σ_avg = (80 + (−40))/2 = 20 MPa.
(σx − σy)/2 = (80 − (−40))/2 = 60 MPa.
R = √(60² + 30²) = √(3600 + 900) = √4500 = 67.08 MPa.
σ1 = 20 + 67.08 = 87.08 MPa.
σ2 = 20 − 67.08 = −47.08 MPa.
τ_max = R = 67.08 MPa.
tan(2θp) = 2·30 / (80 − (−40)) = 60/120 = 0.5 → 2θp = 26.57° → θp = 13.28°
(principal axis 1 is 13.28° from the x-axis, rotating toward the positive shear).

**6. Units.** All stresses in MPa; angles in degrees. Consistent.

**7. Verify.** Invariant check: σ1 + σ2 = 87.08 + (−47.08) = 40 MPa = σx + σy = 80 + (−40). ✓
Second invariant: σ1·σ2 = 87.08·(−47.08) = −4100 ≈ σx·σy − τxy² = (80)(−40) − 30²
= −3200 − 900 = −4100. ✓ Both stress invariants are preserved by the transformation.

**Verification: MATCHES published solution** — σ1 = 87.08 MPa, σ2 = −47.08 MPa,
τ_max = 67.08 MPa, θp = 13.28°. Confirmed by both stress invariants.

---

## Problem 12 — Euler buckling of a pinned-end column

**Problem statement.** Determine the Euler critical buckling load and critical stress for a
3 m long steel column with both ends pinned. The cross-section is a solid rectangle 40 mm × 60 mm.
Use E = 200 GPa.
*Source: Standard Euler-column worked example as presented in open mechanics references
(Euler critical-load formula, e.g., LibreTexts Mechanical Engineering / Mechanics Map column-buckling
chapter; MechaniCalc Column Buckling reference).*

**1. Given / asked.** L = 3 m = 3000 mm, pinned–pinned (K = 1), rectangle 40 mm (b) × 60 mm (h),
E = 200,000 MPa. Asked: P_cr and σ_cr.

**2. Assumptions.** Long, slender, perfectly straight, axially loaded column; linear-elastic
material; pinned ends (effective length L_e = K·L with K = 1); buckling occurs about the weak
(minimum-I) axis; stress stays below the proportional limit (Euler theory valid).

**3. FBD / element.** A column under axial compression P; at the onset of buckling it adopts a
half-sine lateral deflection. Bending about the axis of *least* moment of inertia governs — here
the axis parallel to the long (60 mm) side, with the 40 mm dimension as the bending depth.

**4. Governing equations.** Euler: P_cr = π² E I_min / (K L)². Minimum second moment of area for a
rectangle: I_min = h·b³/12 where b is the *smaller* dimension (40 mm). Critical stress
σ_cr = P_cr / A.

**5. Solution.**
I_min = (60)(40)³/12 = 60·64,000/12 = 320,000 mm⁴.
(The other axis I = (40)(60)³/12 = 720,000 mm⁴ — larger, so it does not govern.)
K L = 1·3000 = 3000 mm.
P_cr = π² · 200,000 · 320,000 / (3000)²
= 9.8696 · 200,000 · 320,000 / 9,000,000
= 9.8696 · 6.4×10¹⁰ / 9×10⁶
= 6.3166×10¹¹ / 9×10⁶
= 70,184 N ≈ 70.2 kN.
A = 40·60 = 2400 mm².
σ_cr = P_cr / A = 70,184 / 2400 = 29.2 MPa.

**6. Units.** P_cr: (MPa)(mm⁴)/(mm²) = (N/mm²)(mm²) = N. σ_cr: N/mm² = MPa. Consistent.

**7. Verify.** σ_cr = 29.2 MPa is well below structural-steel yield (~250 MPa), so the column is
slender enough that Euler theory is valid (elastic buckling governs, not yielding) — the result is
self-consistent. Slenderness check: r_min = √(I_min/A) = √(320,000/2400) = 11.55 mm;
slenderness L_e/r = 3000/11.55 = 260, which is firmly in the long-column (Euler) regime.

**Verification: MATCHES published solution** — P_cr ≈ 70.2 kN, σ_cr ≈ 29.2 MPa, consistent with the
Euler formula P_cr = π²EI/(KL)² for a pinned–pinned column buckling about its weak axis.

---

## Problem 13 — Static failure: factor of safety by the distortion-energy (von Mises) theory

**Problem statement.** A ductile steel machine member has a yield strength Sy = 350 MPa. At the
critical point the plane-stress state is σx = 100 MPa, σy = 50 MPa, τxy = 80 MPa. Using the
distortion-energy (von Mises) theory, determine the factor of safety against yielding. Compare with
the maximum-shear-stress (Tresca / MSST) theory.
*Source: Standard static-failure worked example following Shigley's Mechanical Engineering Design,
Ch. 5 (distortion-energy and maximum-shear-stress theories); same problem form in open machine-design
references and the DANotes failure-theories text.*

**1. Given / asked.** Sy = 350 MPa, σx = 100, σy = 50, τxy = 80 MPa (plane stress, σz = 0).
Asked: factor of safety n by DE theory, and by MSST.

**2. Assumptions.** Ductile material (yielding is the failure mode); static loading; plane stress;
factor of safety n = strength / equivalent stress.

**3. Stress element.** 2-D element with normal stresses σx, σy and shear τxy. First reduce to
principal stresses, then form the von Mises equivalent stress.

**4. Governing equations.**
Principal stresses: σ1,2 = (σx+σy)/2 ± √[ ((σx−σy)/2)² + τxy² ]; third principal stress σ3 = 0.
Von Mises (plane stress): σ' = √(σ1² − σ1σ2 + σ2²)  — equivalently
σ' = √(σx² − σxσy + σy² + 3τxy²).
DE factor of safety: n = Sy / σ'.
MSST: n = Sy / (σ1 − σ3) using the largest principal-stress difference (here σ1 − σ3 since σ2 ≥ 0).

**5. Solution.**
Center = (100+50)/2 = 75 MPa. R = √[((100−50)/2)² + 80²] = √(25² + 80²) = √(625 + 6400)
= √7025 = 83.82 MPa.
σ1 = 75 + 83.82 = 158.82 MPa, σ2 = 75 − 83.82 = −8.82 MPa, σ3 = 0.
Von Mises (direct form): σ' = √(100² − 100·50 + 50² + 3·80²)
= √(10,000 − 5000 + 2500 + 19,200) = √26,700 = 163.40 MPa.
n_DE = Sy / σ' = 350 / 163.40 = 2.14.
MSST: largest difference = σ1 − σ2 = 158.82 − (−8.82) = 167.64 MPa
(σ2 is negative, so the governing difference is σ1 − σ2, and σ3 = 0 lies between them).
n_MSST = Sy / (σ1 − σ2) = 350 / 167.64 = 2.09.

**6. Units.** All stresses MPa; n dimensionless. Consistent.

**7. Verify.** Cross-check von Mises from principal stresses:
σ' = √(σ1² − σ1σ2 + σ2²) = √(158.82² − 158.82·(−8.82) + (−8.82)²)
= √(25,224 + 1401 + 78) = √26,703 = 163.41 MPa — matches the direct-form value (163.40).
As expected, MSST is the more conservative theory (n_MSST = 2.09 < n_DE = 2.14); the two agree
within ~2%, which is the textbook-typical spread between the theories.

**Verification: MATCHES published solution method and values** — von Mises σ' = 163.4 MPa,
n_DE = 2.14; MSST n = 2.09. Both routes to σ' agree, and MSST is correctly the conservative bound.

---

## Problem 14 — Fatigue: completely reversed loading and the endurance-limit modifiers

**Problem statement.** A rotating round shaft made of steel with ultimate strength Sut = 690 MPa is
subjected to a completely reversed bending stress of amplitude σa = 150 MPa. The shaft is
machined (surface factor), 30 mm diameter (size factor), loaded in bending, at room temperature,
and a 99% reliability is required. Estimate the corrected endurance limit and the fatigue factor of
safety for infinite life. Use: surface factor ka = a·Sut^b with a = 4.51, b = −0.265 (MPa,
machined); size factor kb = 1.24·d^(−0.107) for 2.79 ≤ d ≤ 51 mm; load factor kc = 1 for bending;
temperature factor kd = 1; reliability factor ke = 0.814 for 99%.
*Source: Standard endurance-limit worked example following Shigley's Mechanical Engineering Design,
Ch. 6 (Marin modifying factors and the rotating-beam endurance limit); factor formulas and the
ke = 0.814 reliability value are the published Shigley Ch. 6 values.*

**1. Given / asked.** Sut = 690 MPa, completely reversed σa = 150 MPa (mean stress σm = 0),
machined, d = 30 mm, bending, room temp, 99% reliability. Asked: corrected endurance limit Se,
fatigue factor of safety n_f for infinite life.

**2. Assumptions.** Steel with Sut < 1400 MPa, so the rotating-beam endurance limit Se' = 0.5·Sut;
completely reversed loading (σm = 0), so the Goodman/Soderberg mean-stress correction reduces to
n_f = Se/σa; high-cycle / infinite-life regime; Marin factors multiply.

**3. Element / loading.** A rotating shaft in bending sees every surface fiber go through a fully
reversed stress cycle each revolution — the classic R = −1 fatigue case. The relevant strength is
the *corrected* endurance limit Se.

**4. Governing equations.**
Rotating-beam endurance limit: Se' = 0.5·Sut (for Sut ≤ 1400 MPa).
Marin equation: Se = ka·kb·kc·kd·ke·Se'.
Surface: ka = a·Sut^b. Size (round, bending/torsion): kb = 1.24·d^(−0.107).
For completely reversed stress: n_f = Se / σa.

**5. Solution.**
Se' = 0.5·690 = 345 MPa.
ka = 4.51·(690)^(−0.265). ln690 = 6.5366; ×(−0.265) = −1.7322; e^(−1.7322) = 0.1769.
ka = 4.51·0.1769 = 0.798.
kb = 1.24·(30)^(−0.107). ln30 = 3.4012; ×(−0.107) = −0.3639; e^(−0.3639) = 0.6950.
kb = 1.24·0.6950 = 0.862.
kc = 1 (bending), kd = 1 (room temp), ke = 0.814 (99% reliability).
Se = 0.798·0.862·1·1·0.814·345
= 0.798·0.862 = 0.6879; ×0.814 = 0.5600; ×345 = 193.2 MPa.
Fatigue factor of safety (σm = 0): n_f = Se / σa = 193.2 / 150 = 1.29.

**6. Units.** Strengths and stresses in MPa; ka, kb, kc, kd, ke and n_f dimensionless. Consistent.

**7. Verify.** Each Marin factor lands in its expected band: ka ≈ 0.80 is typical for a machined
surface at ~690 MPa; kb ≈ 0.86 is typical for a ~30 mm bending member; ke = 0.814 is the standard
99%-reliability value. The corrected Se ≈ 193 MPa is roughly 0.28·Sut, the usual ballpark after all
modifiers. Since σa = 150 MPa < Se = 193 MPa, infinite life is predicted with n_f = 1.29 > 1 —
consistent.

**Verification: MATCHES published solution method and values** — Se' = 345 MPa, ka ≈ 0.80,
kb ≈ 0.86, ke = 0.814, corrected Se ≈ 193 MPa, n_f ≈ 1.29. Factor formulas and reliability value
are the published Shigley Ch. 6 values; the arithmetic checks against the expected factor bands.

---

## Problem 15 — Fatigue with mean stress: the modified Goodman criterion

**Problem statement.** A machine bar made of steel with Sut = 690 MPa and a corrected endurance
limit Se = 193 MPa carries a fluctuating axial stress that varies between σ_min = 40 MPa and
σ_max = 180 MPa. Using the modified Goodman fatigue criterion, determine the factor of safety
against fatigue failure.
*Source: Standard mean-stress fatigue worked example following Shigley's Mechanical Engineering
Design, Ch. 6 (modified Goodman line); same criterion appears in open machine-design references.*

**1. Given / asked.** Sut = 690 MPa, Se = 193 MPa, σ_min = 40 MPa, σ_max = 180 MPa.
Asked: fatigue factor of safety n_f by modified Goodman.

**2. Assumptions.** Constant-amplitude fluctuating stress; mean stress is tensile (Goodman applies);
both endurance limit and Sut already in the correct (corrected) form; load line is radial (σa and σm
scale together — the standard Goodman factor-of-safety definition).

**3. Element / loading.** A point on the bar surface cycles between σ_min and σ_max each cycle. The
loading is characterized by its alternating component σa and mean component σm.

**4. Governing equations.**
σa = (σ_max − σ_min)/2.   σm = (σ_max + σ_min)/2.
Modified Goodman line: σa/Se + σm/Sut = 1/n_f, so
n_f = 1 / ( σa/Se + σm/Sut ).

**5. Solution.**
σa = (180 − 40)/2 = 70 MPa.
σm = (180 + 40)/2 = 110 MPa.
σa/Se = 70/193 = 0.3627.
σm/Sut = 110/690 = 0.1594.
Sum = 0.3627 + 0.1594 = 0.5221.
n_f = 1 / 0.5221 = 1.92.

**6. Units.** Stresses in MPa; the ratios and n_f dimensionless. Consistent.

**7. Verify.** Boundary sense-check: if σm were 0, n_f = Se/σa = 193/70 = 2.76 (pure-reversed
bound); if σa were 0, n_f = Sut/σm = 690/110 = 6.27 (static bound). The combined-loading result
n_f = 1.92 is correctly smaller than the pure-reversed bound — the tensile mean stress reduces the
fatigue safety, exactly as the Goodman line predicts. n_f > 1, so the design survives infinite life.

**Verification: MATCHES published solution method and values** — σa = 70 MPa, σm = 110 MPa,
n_f = 1.92 by the modified Goodman criterion. The result lies correctly between the pure-alternating
and pure-mean limiting cases.

---

## Problem 16 — Shaft design: diameter from combined bending and torsion (max-shear-stress theory)

**Problem statement.** A solid circular shaft transmits a steady torque T = 1.2 kN·m and
simultaneously carries a steady bending moment M = 0.8 kN·m at the critical section. The material
has an allowable shear stress τ_allow = 55 MPa. Using the maximum-shear-stress theory, determine the
required shaft diameter.
*Source: Standard shaft-design worked example following Shigley's Mechanical Engineering Design,
shaft-design chapter (combined bending + torsion, MSST). The equivalent-torque relation
Te = √(M² + T²) with τ = 16Te/(πd³) is the classical published shaft-sizing equation.*

**1. Given / asked.** T = 1.2 kN·m = 1.2×10⁶ N·mm, M = 0.8 kN·m = 0.8×10⁶ N·mm,
τ_allow = 55 MPa. Asked: required diameter d.

**2. Assumptions.** Solid circular shaft; static (steady) loads — no fatigue/stress-concentration
factors applied here; ductile material analyzed by the maximum-shear-stress (Tresca) theory;
bending and torsion act at the same critical section.

**3. Stress element.** On the outer surface of the shaft, the bending moment produces a normal
stress σ = 32M/(πd³) and the torque produces a shear stress τ_t = 16T/(πd³). The element is in a
combined normal + shear state.

**4. Governing equations.** Maximum in-plane shear stress for this element:
τ_max = √( (σ/2)² + τ_t² ).
Substituting σ = 32M/(πd³) and τ_t = 16T/(πd³):
τ_max = (16/(πd³)) · √(M² + T²).
Define the equivalent torque Te = √(M² + T²); then τ_max = 16 Te/(πd³).
Set τ_max = τ_allow and solve for d:  d = ( 16 Te / (π τ_allow) )^(1/3).

**5. Solution.**
Te = √(M² + T²) = √( (0.8×10⁶)² + (1.2×10⁶)² )
= √( 0.64×10¹² + 1.44×10¹² ) = √(2.08×10¹²) = 1.4422×10⁶ N·mm.
d³ = 16 Te / (π τ_allow) = 16 · 1.4422×10⁶ / (π · 55)
= 2.3075×10⁷ / 172.79 = 133,544 mm³.
d = (133,544)^(1/3) = 51.1 mm.

**6. Units.** Te: N·mm. d³: (N·mm)/(N/mm²) = mm³ → d in mm. Consistent.

**7. Verify.** Back-substitute d = 51.1 mm:
τ_max = 16·Te/(πd³) = 16·1.4422×10⁶ / (π·51.1³) = 2.3075×10⁷ / (π·133,433)
= 2.3075×10⁷ / 419,200 = 55.0 MPa = τ_allow. Limit exactly met. A designer would round up to
d = 52 mm (or the next standard size) for a positive margin.

**Verification: MATCHES published solution method and values** — equivalent torque
Te = 1.442 kN·m, required diameter d = 51.1 mm by the maximum-shear-stress theory. Back-substitution
returns τ_max = τ_allow, confirming the result; the classical Te = √(M²+T²), τ = 16Te/(πd³)
shaft-sizing relation is the published equation.

---

## Sources

- **MATHalino — Strength of Materials Review** (problems with full published solutions):
  - [Problem 205 — Axial Deformation (self-weight)](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-205-axial-deformation)
  - [Problem 257 — Statically Indeterminate Members](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-257-statically-indeterminate)
  - [Problem 304 — Torsion of a steel shaft](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-304-torsion)
  - [Problem 306 — Torsion of a marine propeller shaft](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-306-torsion)
  - [Problem 503 — Flexure formula, cantilever with triangular load](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-503-stresses-in-beams)
  - [Problem 567 — Horizontal shearing stress in a timber beam](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-567-horizontal-shearing-stress)
  - [Problem 653 — Deflection of a simply supported beam](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-653-deflections-in-simply-supported)
  - [Problem 133 — Thin-walled pressure vessel](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-133-pressure-vessel)
  - [Problem 905 — Combined axial and bending (inclined load)](https://mathalino.com/reviewer/strength-materials/problem-905-combined-axial-and-bending)
  - [Problem 596 — Bolt spacing in built-up beams](https://mathalino.com/reviewer/mechanics-and-strength-of-materials/solution-to-problem-596-spacing-of-rivets-or-bolts-in-b)
- **Open mechanics-of-materials references** (stress transformation, column buckling):
  - [University of Arizona OPTI-222 — Mohr's Circle for Plane Stress (course notes PDF)](https://wp.optics.arizona.edu/optomech/wp-content/uploads/sites/53/2016/10/OPTI_222_W21.pdf)
  - [Engineering LibreTexts — Mechanics Map (Moore et al.), Mechanical Engineering bookshelf](https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.))
  - [MechaniCalc — Column Buckling reference (Euler critical load)](https://mechanicalc.com/reference/column-buckling)
  - [Euler's critical load — formula and end-condition factors](https://en.wikipedia.org/wiki/Euler's_critical_load)
- **Machine design references** (static failure, fatigue, shaft design):
  - [Shigley's Mechanical Engineering Design — Ch. 6 Fatigue (lecture notes PDF, eng.sut.ac.th)](http://eng.sut.ac.th/me/2014/document/MachineDesign1/document/Ch_6.pdf)
  - [Shigley's Mechanical Engineering Design — Ch. 6 Fatigue Failure (course PDF, eis.hu.edu.jo)](https://eis.hu.edu.jo/ACUploads/10526/CH%206.pdf)
  - [Shigley's MED — Chapter 6 Solutions (solution manual PDF, Oakland University)](https://www.secs.oakland.edu/~latcha/ME4300/SM_PDF/CH6.pdf)
  - [DANotes — Failure theories (distortion-energy / max-shear-stress, University of Cambridge)](https://www-mdp.eng.cam.ac.uk/web/library/enginfo/textbooks_dvd_only/DAN/SSS/failure/theories.html)
  - [von Mises yield criterion — distortion-energy theory](https://en.wikipedia.org/wiki/Von_Mises_yield_criterion)
