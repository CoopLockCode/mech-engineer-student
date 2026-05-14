# Strength of Materials Reference

A graduate-level study companion for Strength of Materials / Mechanics of Materials
(ENGR 3131/3132). Covers stress and strain, axial loading, torsion, bending,
transverse shear, stress transformation and Mohr's circle, combined loading, beam
deflection, columns and buckling, pressure vessels, and energy methods. Plain-text
math notation throughout: `^` = power, `*` = multiply, `sqrt()` = square root,
`int()` = integral, `pi` = 3.14159..., subscripts written inline (sigma_x).

---

## 0. Foundations, Conventions, and Notation

### 0.1 What "Mechanics of Materials" adds to Statics

Statics treats bodies as rigid and solves for external reactions and internal
resultants (N, V, M, T). Mechanics of Materials drops the rigid-body assumption and
asks the next two questions:

1. **Strength** — given the internal resultants, what is the *stress* at every
   point, and will the material yield or fracture?
2. **Stiffness / stability** — how much does the body *deform* (elongate, twist,
   deflect), and will a slender member buckle?

The three-legged stool of every Mechanics of Materials problem:

- **Equilibrium** — sum of forces and moments = 0 (from Statics; gives internal resultants).
- **Compatibility (kinematics)** — geometry of deformation; displacements must be
  continuous and consistent (e.g., plane sections remain plane).
- **Constitutive law** — material behavior linking stress to strain (Hooke's law
  in the elastic range).

When a problem has more unknowns than equilibrium equations alone can supply, it is
**statically indeterminate**, and you *must* bring in compatibility + constitutive
relations to close the system.

### 0.2 Units

| Quantity | SI | US Customary |
|---|---|---|
| Force | newton (N) | pound (lb), kip = 1000 lb |
| Stress / pressure / modulus | pascal (Pa = N/m^2), MPa, GPa | psi, ksi (1 ksi = 1000 psi) |
| Length | m, mm | in, ft |
| Moment / torque | N·m | lb·in, lb·ft, kip·in |
| Area moment of inertia | m^4, mm^4 | in^4 |

Useful: 1 MPa = 1 N/mm^2 (extremely convenient — keep all lengths in mm and forces
in N and stresses come out directly in MPa). 1 ksi ≈ 6.895 MPa.

### 0.3 Sign conventions (memorize these — most student errors live here)

- **Normal stress / normal force:** tension positive, compression negative.
- **Shear force V on a beam:** positive shear rotates the beam element *clockwise*
  (equivalently: positive V acts downward on the right face of a left-hand segment).
- **Bending moment M on a beam:** positive M is *sagging* (concave up) — it puts the
  bottom fiber in tension and the top fiber in compression. Negative M is *hogging*.
- **Torque T:** by right-hand rule along the member axis; sign is consistent as long
  as you pick a positive axis direction and stay with it.
- **Shear stress tau_xy:** positive on a positive face pointing in the positive
  direction of the other axis. On a stress element, positive shear stresses tend to
  rotate the element counterclockwise about its center is *not* universal — use the
  "positive face / positive direction" rule and be consistent.
- **Mohr's circle shear convention:** shear that tends to rotate the element
  clockwise is plotted *upward* (this is the most common textbook convention; some
  texts flip it — pick one and never mix).

### 0.4 The stress tensor and the strain tensor

At a point, the full 3-D **state of stress** is six independent components:

```
        | sigma_x   tau_xy   tau_xz |
[sigma]=| tau_xy    sigma_y  tau_yz |   (symmetric: tau_xy = tau_yx, etc.)
        | tau_xz    tau_yz   sigma_z|
```

Symmetry (tau_xy = tau_yx) follows from moment equilibrium of the differential
element — the "complementary shear" theorem: **shear stresses on perpendicular
planes are equal in magnitude and both point toward or both away from the common
edge.**

The **state of strain** has the analogous six components: three normal strains
(epsilon_x, epsilon_y, epsilon_z) and three shear strains (gamma_xy, gamma_yz,
gamma_xz). Note the **tensor shear strain** is gamma/2; the **engineering shear
strain** gamma is what appears in Hooke's law and on most strain gauges.

---

## 1. Stress and Strain

### 1.1 Normal stress and normal strain

**Average normal stress** on a cross-section carrying axial force N:

```
sigma = N / A
```

valid when the load passes through the centroid and the section is far from points
of load application (Saint-Venant's principle: local stress disturbances die out
within roughly one characteristic dimension of the cross-section).

**Normal strain** — change in length per unit length:

```
epsilon = delta / L          (average, uniform bar)
epsilon = d(delta)/dx        (at a point, nonuniform)
```

Strain is dimensionless; often reported in microstrain (1 ue = 1e-6).

### 1.2 Shear stress and shear strain

**Average shear stress** on an area A_v carrying shear force V:

```
tau = V / A_v
```

Examples: bolt in single shear (A_v = bolt cross-section), bolt in double shear
(A_v = 2 × bolt cross-section), punch shearing a plate (A_v = perimeter × thickness),
glued lap joint (A_v = glued area).

**Shear strain** gamma — the change in the right angle between two originally
perpendicular line elements, in radians.

### 1.3 Hooke's law and elastic constants

**Uniaxial Hooke's law:**

```
sigma = E * epsilon
```

E = **modulus of elasticity** (Young's modulus). Steel ≈ 200 GPa (29,000 ksi),
aluminum ≈ 69 GPa (10,000 ksi).

**Shear:**

```
tau = G * gamma
```

G = **shear modulus** (modulus of rigidity).

**Poisson's ratio** nu — magnitude of the ratio of lateral to axial strain in
uniaxial loading:

```
nu = -epsilon_lateral / epsilon_axial      (0 <= nu <= 0.5 for isotropic materials)
```

Steel ≈ 0.30, aluminum ≈ 0.33, rubber → 0.5 (incompressible).

**The isotropic relation linking the three constants:**

```
G = E / (2 * (1 + nu))
```

Only two of {E, G, nu} are independent for an isotropic material.

**Generalized (3-D) Hooke's law** — normal strains:

```
epsilon_x = (1/E) * [ sigma_x - nu*(sigma_y + sigma_z) ]
epsilon_y = (1/E) * [ sigma_y - nu*(sigma_z + sigma_x) ]
epsilon_z = (1/E) * [ sigma_z - nu*(sigma_x + sigma_y) ]
```

Shear strains (uncoupled for isotropic material):

```
gamma_xy = tau_xy / G,  gamma_yz = tau_yz / G,  gamma_xz = tau_xz / G
```

**Bulk modulus / dilatation.** Volumetric strain e = epsilon_x + epsilon_y +
epsilon_z. Under hydrostatic pressure p, e = -p/K where the **bulk modulus** is:

```
K = E / (3 * (1 - 2*nu))
```

Note nu → 0.5 makes K → infinity (incompressible), which is why no real isotropic
material exceeds nu = 0.5.

### 1.4 The stress-strain diagram (ductile metal in tension)

Key landmarks, in order of increasing strain:

1. **Proportional limit** — end of the linear region; Hooke's law valid up to here.
2. **Elastic limit** — last point from which the material fully recovers on
   unloading (very close to proportional limit; often treated as the same point).
3. **Yield point / yield strength S_y** — onset of large permanent (plastic)
   deformation. For materials with no sharp yield point, use the **0.2% offset
   method**: draw a line parallel to the elastic slope, offset by epsilon = 0.002;
   its intersection with the curve defines S_y.
4. **Strain hardening region** — stress rises again as the material strengthens.
5. **Ultimate tensile strength S_u** — peak engineering stress.
6. **Necking** — localized cross-section reduction; engineering stress falls.
7. **Fracture.**

- **Engineering stress/strain** use the *original* area and length.
  **True stress/strain** use the instantaneous values; true stress keeps rising to
  fracture.
- **Ductile** materials (mild steel, aluminum) yield and neck, % elongation large.
  **Brittle** materials (cast iron, concrete, glass) fracture with little warning,
  near the proportional limit, and are much stronger in compression than tension.
- **Resilience** = area under the curve up to yield (energy absorbed elastically per
  unit volume), modulus of resilience u_r = S_y^2 / (2E).
- **Toughness** = total area under the curve to fracture (energy per unit volume to
  break the material).

### 1.5 Allowable stress, factor of safety, design

```
Factor of safety:  n = sigma_failure / sigma_allowable = S_y / sigma_allow  (or S_u / sigma_allow)
Allowable stress:  sigma_allow = S_y / n
```

Choose the failure stress (S_y for "no yielding" designs, S_u for brittle/fracture
designs). n > 1 always; typical structural values 1.5–3, higher where loads or
material data are uncertain or consequences severe.

### 1.6 Thermal strain and thermal stress

Free (unrestrained) thermal strain:

```
epsilon_T = alpha * deltaT      (alpha = coefficient of thermal expansion)
delta_T = alpha * deltaT * L
```

If the body is **free to expand**, there is strain but **no thermal stress**. Thermal
stress arises only when expansion is *restrained*. Procedure for a fully restrained
bar: superpose (a) free thermal elongation and (b) the mechanical force needed to
push it back to its original length; set total delta = 0:

```
alpha * deltaT * L  -  P*L/(A*E) = 0   =>   sigma = P/A = E * alpha * deltaT
```

### 1.7 Stress concentration

Geometric discontinuities (holes, fillets, notches, keyways) raise the local stress:

```
sigma_max = K_t * sigma_nominal
```

K_t = **theoretical (geometric) stress concentration factor**, read from charts as a
function of geometry ratios (e.g., r/d, D/d). For *static* loading of *ductile*
materials, localized yielding redistributes stress, so K_t is often neglected for
static strength but **must** be kept for brittle materials and for *all* fatigue
analysis (see machine-design reference).

---

## 2. Axially Loaded Members

### 2.1 Elongation of a bar

For a prismatic bar, constant N, A, E:

```
delta = N * L / (A * E)
```

General case (N, A, or E varies, or several segments):

```
delta = int_0^L [ N(x) / (A(x) * E(x)) ] dx          (continuous variation)
delta = sum_i [ N_i * L_i / (A_i * E_i) ]            (discrete segments)
```

Sign: tension N positive → elongation positive. Always draw the **axial force
diagram** first when loads are applied at multiple points along the bar.

The group A*E is the **axial rigidity**; A*E/L is the **axial stiffness** k of the
bar acting as a spring (P = k*delta).

### 2.2 Statically indeterminate axial problems — the master procedure

When equilibrium alone is insufficient (e.g., a bar fixed at both ends, or a load
shared by parallel members of different material):

1. **Equilibrium** — write all available force equations; identify the number of
   redundant unknowns.
2. **Compatibility** — write a geometric statement about the deformations
   (e.g., delta_total = 0 for a bar fixed both ends; delta_1 = delta_2 for two
   parallel members of equal length sharing a rigid cap).
3. **Force–deformation (constitutive)** — substitute delta = N*L/(A*E) for each
   member into the compatibility equation.
4. **Solve** equilibrium + compatibility simultaneously for the forces, then back
   out stresses and deflections.

Common configurations: bar fixed at both ends with an intermediate load; composite
("bolt-and-sleeve" or concrete-with-rebar) members in parallel; bars of unequal
length with a gap that may or may not close.

### 2.3 Saint-Venant's principle

The stress distribution becomes essentially uniform (= N/A) at distances greater
than about one cross-sectional dimension away from concentrated loads or supports.
Justifies the use of average stress formulas away from such regions.

---

## 3. Torsion

### 3.1 Assumptions for circular shafts

- Plane cross-sections remain plane and rigid (do **not** warp) — true for *circular*
  sections only. Non-circular sections warp and need a different theory.
- Radii remain straight; the cross-section rotates as a rigid disk.
- Material linear-elastic, shaft prismatic (for the basic formula).

### 3.2 Derivation of the torsion formula

**Kinematics.** Consider a shaft of length L twisting through total angle phi. A
radial line at radius rho rotates; the resulting shear strain at radius rho is

```
gamma(rho) = rho * (dphi/dx) = rho * phi / L      (linear in rho)
```

So shear strain is **zero at the center and maximum at the outer surface**.

**Constitutive.** Apply Hooke's law in shear, tau = G*gamma:

```
tau(rho) = G * rho * (dphi/dx)        — shear stress also linear in rho
```

**Equilibrium.** The internal torque is the resultant moment of the shear stresses
about the axis:

```
T = int_A [ rho * tau(rho) ] dA = G*(dphi/dx) * int_A rho^2 dA = G*(dphi/dx) * J
```

where the **polar moment of inertia** J = int_A rho^2 dA. Solve for G*(dphi/dx) =
T/J and substitute back:

```
THE TORSION FORMULA:    tau = T * rho / J

Maximum shear stress:   tau_max = T * c / J        (c = outer radius)
```

**Angle of twist** (integrate dphi/dx = T/(G*J) over the length):

```
phi = T * L / (G * J)              (prismatic, constant T)
phi = int_0^L [ T(x) / (G(x)*J(x)) ] dx     (general)
phi = sum_i [ T_i * L_i / (G_i * J_i) ]     (segments)
```

G*J is the **torsional rigidity**.

### 3.3 Polar moment of inertia J

| Section | J |
|---|---|
| Solid circular, radius c | J = pi*c^4 / 2 = pi*d^4 / 32 |
| Hollow circular, outer c_o, inner c_i | J = (pi/2)*(c_o^4 - c_i^4) |

For circular sections, J = I_x + I_y = 2*I (since I_x = I_y for a circle).

### 3.4 Power transmission

For a shaft rotating at angular speed omega (rad/s) transmitting power P:

```
P = T * omega = 2*pi*f*T          (f = rev/s = Hz)
```

US customary: horsepower hp = T*n / 63025 with T in lb·in and n in rpm. SI: P in
watts, T in N·m, omega in rad/s.

### 3.5 Statically indeterminate torsion

Same three-step logic as axial: equilibrium (sum of torques), compatibility (e.g.,
phi_total = 0 for a shaft fixed at both ends; phi_A = phi_B for series/parallel
shafts), and the force–deformation relation phi = TL/(GJ).

### 3.6 Non-circular sections and thin-walled tubes (awareness level)

- **Non-circular solid sections warp.** Maximum shear is generally at the point on
  the boundary *closest* to the centroid (not the farthest), and is found from
  tabulated coefficients (e.g., for a rectangle, tau_max = T/(alpha*a*b^2)).
- **Thin-walled closed tubes** (one cell): shear flow q = tau*t is constant around
  the perimeter, q = T/(2*A_m) where A_m is the area *enclosed by the median line*.
  Angle of twist phi = (T*L)/(4*A_m^2*G) * int(ds/t).

### 3.7 Torsion pitfalls

- Using diameter instead of radius for c, or forgetting J uses d^4/32 (not d^4/64,
  which is the bending I).
- Mixing degrees and radians: phi from TL/(GJ) is in **radians**.
- Forgetting that tau is **zero at the center** — the centroidal material carries
  no torsional shear.
- Applying the circular-shaft formula to a square bar.

---

## 4. Bending of Beams

### 4.1 Internal resultants: shear force V and bending moment M

Cut the beam, draw the FBD of one segment, and enforce equilibrium. Sign convention
per §0.3 (positive V = clockwise shear, positive M = sagging).

**Differential relations among load w(x), shear V(x), moment M(x)** (w positive
downward in many texts — be consistent; here w is the distributed load intensity):

```
dV/dx = -w(x)        (slope of shear diagram = -distributed load)
dM/dx = V(x)         (slope of moment diagram = shear)
d^2M/dx^2 = -w(x)
```

Integrated forms (the "area method" for drawing diagrams):

```
V_2 - V_1 = -(area under load curve between 1 and 2)
M_2 - M_1 =  (area under shear curve between 1 and 2)
```

**Consequences used to sketch and check diagrams:**
- A concentrated force causes a *jump* in V (equal to the force).
- A concentrated couple causes a *jump* in M.
- M is maximum or minimum where V = 0 (or where V crosses zero / jumps through zero).
- Between point loads, w = 0 → V constant → M linear.
- Under uniform w → V linear → M parabolic.

### 4.2 Derivation of the flexure formula

**Assumptions (Euler–Bernoulli beam theory):** prismatic beam, linear-elastic
material, plane sections remain plane and perpendicular to the neutral axis,
deflections small, pure bending (or bending dominated — shear effect on stress
neglected), cross-section symmetric about the plane of loading, stresses below
proportional limit.

**Kinematics.** Under positive (sagging) moment the beam curves with radius of
curvature rho. A longitudinal fiber at distance y *above* the neutral axis shortens.
With "plane sections remain plane," the longitudinal strain varies linearly with y:

```
epsilon_x(y) = -y / rho
```

(zero on the neutral axis, compressive above it for positive M).

**Constitutive.** sigma_x = E*epsilon_x = -E*y/rho — **bending stress is linear in y.**

**Equilibrium #1 — no net axial force.** int_A sigma_x dA = 0 →
-(E/rho) int_A y dA = 0 → int_A y dA = 0. The **first moment of area about the
neutral axis is zero**, which means *the neutral axis passes through the centroid*
of the cross-section.

**Equilibrium #2 — internal moment equals applied moment.**

```
M = int_A (-y * sigma_x) dA = (E/rho) * int_A y^2 dA = (E/rho) * I
```

where the **second moment of area (moment of inertia)** I = int_A y^2 dA. Hence the
**moment–curvature relation**:

```
1/rho = M / (E*I)
```

Substitute E/rho = M/I back into sigma_x = -E*y/rho:

```
THE FLEXURE FORMULA:    sigma_x = -M * y / I

Magnitude / max:        sigma_max = M * c / I = M / S
```

where c is the distance to the extreme fiber and **S = I/c is the section modulus**.
The sign: for positive M, fibers above the NA (y > 0) are in compression, below in
tension — but in practice most students compute the magnitude M*c/I and assign
tension/compression by inspection of the bending direction.

E*I is the **flexural rigidity**.

### 4.3 Moment of inertia and section properties

**Parallel-axis theorem:**

```
I = I_centroid + A * d^2
```

where d is the distance between the centroidal axis and the new (parallel) axis. Use
it to build up composite sections: split into rectangles/standard shapes, find each
piece's I about its own centroid, transfer each to the section's overall centroidal
axis, and sum.

**Standard centroidal area moments of inertia (about the horizontal axis through the centroid):**

| Section | Area A | I (about centroidal axis) | c | S = I/c |
|---|---|---|---|---|
| Rectangle, base b, height h | b*h | b*h^3 / 12 | h/2 | b*h^2 / 6 |
| Solid circle, diameter d | pi*d^2/4 | pi*d^4 / 64 | d/2 | pi*d^3 / 32 |
| Hollow circle, d_o, d_i | (pi/4)(d_o^2-d_i^2) | (pi/64)(d_o^4 - d_i^4) | d_o/2 | I/c |
| Triangle, base b, height h | b*h/2 | b*h^3 / 36 | (centroid at h/3 from base; c differs each way) | — |
| I-beam / built-up | sum of parts | use parallel-axis on each rectangle | h/2 | I/c |

Note: for torsion of circular shafts use **J = pi*d^4/32**; for bending use
**I = pi*d^4/64**. They differ by a factor of 2.

### 4.4 Transverse (horizontal) shear stress in beams

When V varies along the beam, bending stress varies between adjacent sections; the
imbalance is carried by **longitudinal shear**, which (by complementary shear) equals
the transverse shear stress on the cross-section.

**The shear formula:**

```
tau = V * Q / (I * b)
```

- V = shear force at the section.
- Q = **first moment of area** of the portion of the cross-section *beyond* (above or
  below) the point where tau is wanted, taken about the neutral axis:
  Q = A' * y_bar', where A' is that partial area and y_bar' is the distance from the
  NA to A''s centroid.
- I = moment of inertia of the *whole* cross-section about the NA.
- b = width of the cross-section *at the location where tau is evaluated*.

**Key results:**
- Shear stress is **zero at the top and bottom edges** (Q = 0 there) and **maximum at
  the neutral axis** (Q is largest there).
- Rectangular section: tau_max = 1.5 * V/A = (3/2)(V/(b*h)) — 50% higher than the
  average V/A. Distribution is parabolic.
- Circular section: tau_max = (4/3) * V/A at the NA.
- I-beam: the web carries almost all the shear; a common approximation is
  tau ≈ V / A_web.

**Shear flow** for built-up / fastened members (nails, bolts, glue holding flanges
to a web):

```
q = V * Q / I        (force per unit length along the joint)
```

Fastener spacing s and capacity F per fastener: s = F / q (per shear plane; double
the capacity for two fastener rows or two glue lines).

### 4.5 Bending pitfalls

- Forgetting that the neutral axis goes through the **centroid** — using a wrong
  reference axis for I.
- Using the full-section I but forgetting parallel-axis transfers for composite shapes.
- In the shear formula, using b at the wrong height, or computing Q for the wrong
  partial area (it is the area *outside* the cut, between the cut and the free edge).
- Confusing S (section modulus, I/c) with I.
- Sign confusion: just compute magnitudes and reason about tension/compression sides
  from the bending direction.

---

## 5. Stress Transformation and Mohr's Circle

### 5.1 Plane stress

A point is in **plane stress** when one face of the element is stress-free
(sigma_z = tau_xz = tau_yz = 0). Common: free surfaces of any loaded body. The state
is then fully described by sigma_x, sigma_y, tau_xy.

### 5.2 Transformation equations

Rotate the element by angle theta (counterclockwise positive) to new axes x'–y':

```
sigma_x' = (sigma_x + sigma_y)/2 + (sigma_x - sigma_y)/2 * cos(2theta) + tau_xy * sin(2theta)
sigma_y' = (sigma_x + sigma_y)/2 - (sigma_x - sigma_y)/2 * cos(2theta) - tau_xy * sin(2theta)
tau_x'y' = -(sigma_x - sigma_y)/2 * sin(2theta) + tau_xy * cos(2theta)
```

Invariant: sigma_x' + sigma_y' = sigma_x + sigma_y (sum of normal stresses is
constant under rotation).

### 5.3 Principal stresses and maximum shear

**Principal stresses** — the extreme normal stresses; the planes on which they act
carry **zero shear stress**:

```
sigma_1,2 = (sigma_x + sigma_y)/2  +/-  sqrt[ ((sigma_x - sigma_y)/2)^2 + tau_xy^2 ]
```

**Orientation of principal planes:**

```
tan(2*theta_p) = 2*tau_xy / (sigma_x - sigma_y)
```

(two roots 90° apart — one gives sigma_1, the other sigma_2).

**Maximum in-plane shear stress:**

```
tau_max = sqrt[ ((sigma_x - sigma_y)/2)^2 + tau_xy^2 ] = (sigma_1 - sigma_2)/2
```

acting on planes **45° from the principal planes**. On the planes of maximum shear,
the normal stress equals the average:

```
sigma_avg = (sigma_x + sigma_y)/2
```

### 5.4 Mohr's circle — construction procedure

Mohr's circle is the transformation equations plotted as a circle in
(sigma, tau) space.

1. **Axes:** horizontal = sigma (tension right, positive). Vertical = tau. Use the
   convention "clockwise shear plotted up" (or pick the opposite and stay consistent).
2. **Plot point X** = (sigma_x, tau_xy) and **point Y** = (sigma_y, -tau_xy)
   (Y uses the opposite shear sign). X and Y are diametrically opposite.
3. **Center** C = ((sigma_x + sigma_y)/2, 0) on the sigma axis.
4. **Radius** R = sqrt[ ((sigma_x - sigma_y)/2)^2 + tau_xy^2 ] = tau_max.
5. **Principal stresses** = C +/- R = where the circle crosses the sigma axis
   (tau = 0 there).
6. **Rotations:** an angle theta in the *physical* element corresponds to **2·theta
   in the same direction** on the circle. To get stresses on a plane rotated theta
   CCW from x, rotate the radius to X by 2·theta CCW.
7. **tau_max** = top/bottom of the circle = R; the corresponding normal stress is
   sigma_avg (the center).
8. **Absolute maximum shear (3-D check):** even in plane stress, sigma_3 = 0 is a
   principal stress. Order the three principal stresses (including 0). The true
   absolute max shear is (sigma_max - sigma_min)/2 using all three. If sigma_1 and
   sigma_2 have the **same sign**, the absolute max shear is *larger* than the
   in-plane value — a classic exam trap.

### 5.5 Strain transformation and strain rosettes

Strain transforms like stress, but with **gamma/2** in place of tau:

```
epsilon_x' = (epsilon_x+epsilon_y)/2 + (epsilon_x-epsilon_y)/2 cos(2th) + (gamma_xy/2) sin(2th)
gamma_x'y'/2 = -(epsilon_x-epsilon_y)/2 sin(2th) + (gamma_xy/2) cos(2th)
```

Principal strains and a Mohr's circle for strain follow identically (plot
(epsilon, gamma/2)).

**Strain rosette:** three gauges at known angles (theta_a, theta_b, theta_c) read
epsilon_a, epsilon_b, epsilon_c. Write the normal-strain transformation equation
three times and solve the linear system for epsilon_x, epsilon_y, gamma_xy. Then use
Hooke's law to get stresses. 45° rectangular rosette (0°/45°/90°) gives the tidy
result epsilon_x = epsilon_a, epsilon_y = epsilon_c, gamma_xy = 2*epsilon_b -
epsilon_a - epsilon_c.

### 5.6 Transformation pitfalls

- Wrong shear sign for point Y on Mohr's circle.
- Forgetting the **factor of 2** between physical angle and circle angle.
- Using gamma instead of gamma/2 in strain transformation.
- Reporting only the in-plane max shear when the 3-D (absolute) max shear governs.
- Forgetting that principal planes have zero shear by definition.

---

## 6. Combined Loading

Real members carry several internal resultants at once (axial N, torsion T, bending
M, shear V). **Procedure:**

1. **Section** the member at the critical location; find N, V, M, T there.
2. **Compute the stress from each resultant separately:**
   - Axial: sigma = N/A (uniform over the section).
   - Bending: sigma = M*c/I (linear; tension one side, compression the other).
   - Torsion: tau = T*c/J (shafts) — max at the surface.
   - Transverse shear: tau = V*Q/(I*b) — max at the NA, zero at the extreme fibers.
3. **Identify candidate critical points** — typically the extreme fibers (max bending
   + axial, but transverse shear = 0 there) and the neutral axis (max transverse
   shear, but bending = 0 there). For a shaft, the surface point where bending and
   torsion stack.
4. **Superpose** stresses of the *same type* at each candidate point (normal stresses
   add algebraically; shear stresses add as vectors / with attention to direction).
   Superposition is valid because everything is linear-elastic and deflections small.
5. **Build the stress element** at each candidate point: (sigma_x, sigma_y, tau_xy).
6. **Transform** — compute principal stresses and max shear (Mohr's circle).
7. **Apply a failure theory** (see machine-design reference) to decide whether the
   point is safe.

**Classic case — shaft with combined bending + torsion** (point on the surface where
both peak):

```
sigma_x = M*c/I = 32*M/(pi*d^3)        sigma_y = 0
tau_xy  = T*c/J = 16*T/(pi*d^3)

sigma_1,2 = sigma_x/2  +/-  sqrt[ (sigma_x/2)^2 + tau_xy^2 ]
tau_max   =                sqrt[ (sigma_x/2)^2 + tau_xy^2 ]
```

This leads to the "equivalent moment" / "equivalent torque" shaft-design formulas in
Machine Design.

**Eccentric axial load** (load P offset by e from the centroid) = pure axial P + a
bending moment M = P*e. Superpose: sigma = P/A +/- P*e*c/I. The load can be entirely
compressive yet produce tension on the far face if the eccentricity is large enough
("kern" of the section is the region where the load causes no tension anywhere).

---

## 7. Beam Deflection

### 7.1 The elastic curve and the governing differential equation

For small slopes, curvature ≈ d^2v/dx^2, and the moment–curvature relation gives the
**second-order (moment) form**:

```
E*I * (d^2v/dx^2) = M(x)
```

where v(x) is the transverse deflection (positive up, in most texts). Differentiating
and using dM/dx = V and dV/dx = -w:

```
E*I * (d^3v/dx^3) = V(x)            (third-order, shear form)
E*I * (d^4v/dx^4) = -w(x)           (fourth-order, load form)
```

Slope theta(x) = dv/dx.

### 7.2 Method 1 — Double integration

1. Write M(x) for each region (use as few regions as possible).
2. Integrate once: E*I*v' = int M dx + C1  (slope).
3. Integrate again: E*I*v = int(int M) dx + C1*x + C2 (deflection).
4. **Boundary conditions** (geometric): pin/roller → v = 0; fixed support → v = 0 and
   v' = 0; free end → no geometric condition (use natural conditions on M, V).
5. **Continuity conditions:** at the junction of two regions, v and v' from each
   region's equations must match. (n regions → 2n constants → need 2n conditions.)
6. Solve for the constants; report slope/deflection where wanted.

**Macaulay's bracket / singularity-function method** condenses multi-region problems:
write a single M(x) using bracket terms `<x - a>^n` that "switch on" only for x > a,
then integrate once for the whole beam. Greatly reduces the bookkeeping for several
loads.

### 7.3 Method 2 — Moment-area theorems

Define the M/EI diagram (the bending-moment diagram divided by EI).

- **Theorem 1:** the change in slope between points A and B equals the **area** of
  the M/EI diagram between A and B.

  ```
  theta_B - theta_A = area of (M/EI) from A to B
  ```

- **Theorem 2:** the **tangential deviation** of B from the tangent drawn at A
  (vertical distance, measured at B, between the elastic curve's tangent at A and
  point B) equals the **first moment of the M/EI area between A and B, taken about B**.

  ```
  t_{B/A} = (area of M/EI from A to B) * (centroidal distance of that area from B)
  ```

Excellent for cantilevers (tangent at the fixed end is horizontal → slope and
deflection at the free end come directly) and for finding slopes/deflections at
specific points.

### 7.4 Method 3 — Superposition

Because the beam equation is linear, the deflection (and slope) due to a combination
of loads equals the **sum** of the deflections due to each load acting alone. Look up
each elementary case in a standard table (below), then add. This is the fastest
method for statically determinate beams with several loads, and the standard tool for
solving **statically indeterminate beams**:

1. Remove the redundant reaction(s) to get a determinate "released" beam.
2. Compute the deflection at the redundant's location due to (a) the actual loads and
   (b) the unknown redundant force/moment, from the table.
3. **Compatibility:** the actual deflection (or slope) at that point is zero (or
   matches the support condition). Set the superposed deflection = 0 and solve for
   the redundant.
4. Back-substitute into equilibrium for the remaining reactions.

### 7.5 Standard beam deflection cases

Notation: L = span, E*I = flexural rigidity, x measured from the left end,
delta = deflection (downward positive in this table), theta = slope. P = point load,
M_0 = applied couple, w = uniform load intensity, w_0 = peak of triangular load.

**Cantilever beams (fixed at left end A, free at right end B):**

| Loading | Max deflection (at free end B) | Slope at B |
|---|---|---|
| Point load P at free end | delta_B = P*L^3 / (3*E*I) | theta_B = P*L^2 / (2*E*I) |
| Point load P at distance a from fixed end | delta_B = (P*a^2/(6EI))*(3L - a) | theta_B = P*a^2 / (2*E*I) |
| Uniform load w over full span | delta_B = w*L^4 / (8*E*I) | theta_B = w*L^3 / (6*E*I) |
| Triangular load, 0 at free end → w_0 at fixed end | delta_B = w_0*L^4 / (30*E*I) | theta_B = w_0*L^3 / (24*E*I) |
| Couple M_0 at free end | delta_B = M_0*L^2 / (2*E*I) | theta_B = M_0*L / (E*I) |

**Simply supported beams (pin at A, roller at B, span L):**

| Loading | Max deflection | Location / slopes |
|---|---|---|
| Central point load P | delta_max = P*L^3 / (48*E*I) | at midspan; theta_ends = P*L^2/(16*E*I) |
| Point load P at distance a from A (b = L-a) | delta at load = P*a^2*b^2/(3*E*I*L); delta_max = P*b*(L^2-b^2)^1.5 / (9*sqrt(3)*E*I*L) at x = sqrt((L^2-b^2)/3) | theta_A = P*b*(L^2-b^2)/(6EIL) |
| Uniform load w over full span | delta_max = 5*w*L^4 / (384*E*I) | at midspan; theta_ends = w*L^3/(24*E*I) |
| Couple M_0 at end A | delta_max = M_0*L^2 / (9*sqrt(3)*E*I) | theta_A = M_0*L/(3EI), theta_B = M_0*L/(6EI) |
| Triangular load 0 at A → w_0 at B | delta_max ≈ 0.00652 * w_0*L^4 / (E*I) | near x ≈ 0.519 L |

**Fixed–fixed and propped cantilever (statically indeterminate, common results):**

| Beam & loading | Key result |
|---|---|
| Fixed–fixed, uniform load w | end moments M = w*L^2/12; midspan moment = w*L^2/24; delta_mid = w*L^4/(384*E*I) |
| Fixed–fixed, central point load P | end moments = P*L/8; delta_mid = P*L^3/(192*E*I) |
| Propped cantilever (fixed A, roller B), uniform load w | roller reaction R_B = 3*w*L/8; fixed-end moment = w*L^2/8; delta_max ≈ w*L^4/(185*E*I) at x ≈ 0.4215 L |
| Propped cantilever, point load P at midspan | R_B = 5P/16; fixed-end moment = 3PL/16 |

### 7.6 Deflection pitfalls

- Mixing sign conventions between M(x) and the assumed positive direction of v.
- Forgetting continuity conditions in multi-region double integration (you need 2n
  conditions for n regions).
- Using a table case whose **support/loading does not exactly match** the problem.
- Units: keep E in consistent units; a deflection that comes out in "ksi·in / (psi)"
  means a unit slip. Deflection should come out in length units.
- Forgetting that superposition for indeterminate beams needs the **compatibility**
  equation at the released redundant to actually solve anything.

---

## 8. Columns and Buckling

### 8.1 The phenomenon

A slender member in compression can fail by **elastic instability (buckling)** —
sudden large lateral deflection — at a load *well below* the yield-stress load
sigma_y*A. Buckling is a *stiffness/stability* failure, not a strength failure.

### 8.2 Euler buckling load — derivation (pin-pin column)

Consider a pin-ended column carrying axial load P, slightly deflected by v(x). The
internal moment at a section is M = -P*v (the load times the lateral offset). Insert
into E*I*v'' = M:

```
E*I * v'' = -P*v   =>   v'' + (P/(E*I)) * v = 0
```

This is the harmonic-oscillator ODE; let k^2 = P/(EI). General solution
v = A*sin(kx) + B*cos(kx). Boundary conditions v(0) = 0 → B = 0; v(L) = 0 →
A*sin(kL) = 0. The nontrivial solution (A ≠ 0) requires sin(kL) = 0, i.e.,
kL = n*pi. The smallest nonzero root (n = 1) gives the **critical (Euler) load**:

```
P_cr = pi^2 * E * I / L^2          (pin-pin column)
```

### 8.3 Effective length and end conditions

General Euler formula:

```
P_cr = pi^2 * E * I / (K*L)^2
```

K = **effective-length factor** (L_e = K*L is the effective length = distance
between inflection points):

| End conditions | K (theoretical) | K (recommended design) |
|---|---|---|
| Pinned – pinned | 1.0 | 1.0 |
| Fixed – free (cantilever column) | 2.0 | 2.1 |
| Fixed – fixed | 0.5 | 0.65 |
| Fixed – pinned | 0.7 | 0.80 |

Use the **minimum I** of the cross-section (the column buckles about its weakest
axis) unless bracing prevents buckling about that axis.

### 8.4 Critical stress, slenderness ratio, radius of gyration

Define the **radius of gyration** r = sqrt(I/A). Then the **critical stress**:

```
sigma_cr = P_cr / A = pi^2 * E / (K*L/r)^2
```

The group **(K*L/r) is the slenderness ratio**. Euler's formula is valid only while
sigma_cr <= proportional limit — i.e., for **long, slender columns** above a
transition slenderness ratio (KL/r)_transition = sqrt(2*pi^2*E / sigma_y) (using S_y;
some texts use the proportional limit).

### 8.5 Column classification and intermediate columns

- **Short columns / "blocks":** fail by yielding/crushing, sigma = P/A approaches S_y.
- **Long (slender) columns:** fail by elastic Euler buckling; use P_cr above.
- **Intermediate columns:** fail by *inelastic buckling* — Euler overpredicts. Use an
  empirical formula:
  - **Johnson parabola** (common in machine design):
    sigma_cr = S_y - (1/E)*(S_y*KL/(2*pi*r))^2, valid below the tangent point with
    the Euler curve.
  - **Secant formula** for eccentrically loaded columns (load offset e):
    sigma_max = (P/A)*[ 1 + (e*c/r^2)*sec( (KL/(2r))*sqrt(P/(EA)) ) ].

### 8.6 Buckling pitfalls

- Using the wrong I — must be the **minimum** unless bracing dictates otherwise.
- Forgetting to apply K (effective length) — using L instead of K*L.
- Applying Euler's formula to a stocky column where it is invalid (always check the
  slenderness ratio against the transition value).
- Treating buckling as a stress problem — it's an instability; a perfectly straight
  ideal column carries P_cr with *zero* lateral deflection up to the bifurcation.

---

## 9. Pressure Vessels

### 9.1 Thin-walled assumption

A vessel is "thin-walled" when **r/t >= 10** (inner radius to wall thickness). Then
the stress is essentially uniform through the wall thickness and the simple membrane
formulas apply.

### 9.2 Thin-walled cylinder — derivation

**Hoop (circumferential) stress sigma_h.** Cut the cylinder with a longitudinal plane
through the axis. The FBD of half the cylinder, length L: internal pressure p pushes
out on the projected area (2r·L); two wall strips of area (t·L) each resist.
Equilibrium:

```
p * (2r) * L = sigma_h * (2 * t * L)   =>   sigma_h = p*r / t
```

**Longitudinal (axial) stress sigma_l.** Cut with a transverse plane. Pressure acts
on the end cap area pi*r^2; the wall ring of area 2*pi*r*t resists. Equilibrium:

```
p * pi*r^2 = sigma_l * (2*pi*r*t)   =>   sigma_l = p*r / (2*t)
```

**Key result:** sigma_h = 2 * sigma_l — the hoop stress is **twice** the longitudinal
stress, which is why pressurized cylinders (and overcooked sausages) split along a
longitudinal line.

The radial stress at the inner wall is -p and at the outer wall is 0; both are small
compared to sigma_h when r/t is large, so radial stress is neglected in thin-wall
theory. The state of stress at the wall is therefore biaxial:
sigma_h = pr/t, sigma_l = pr/2t, tau = 0 (these are already principal stresses).
In-plane tau_max = (sigma_h - sigma_l)/2 = pr/(4t); the **absolute** max shear,
including the zero radial/through-thickness stress, is sigma_h/2 = pr/(2t).

### 9.3 Thin-walled sphere

By symmetry every great-circle cut gives the same result:

```
sigma = p*r / (2*t)        (same in all directions — equibiaxial)
```

A sphere is the most efficient pressure vessel shape (lowest wall stress for a given
p, r, t).

### 9.4 Thick-walled cylinders (Lamé equations — awareness level)

When r/t < 10 the stress varies through the wall. **Lamé's solution** for a cylinder
with inner radius a, outer radius b, internal pressure p_i, external pressure p_o:

```
sigma_r(r)     = (p_i*a^2 - p_o*b^2)/(b^2-a^2) - (p_i-p_o)*a^2*b^2 / [(b^2-a^2)*r^2]
sigma_theta(r) = (p_i*a^2 - p_o*b^2)/(b^2-a^2) + (p_i-p_o)*a^2*b^2 / [(b^2-a^2)*r^2]
```

The hoop stress is **maximum at the inner surface**. For internal pressure only,
sigma_theta(a) = p_i*(b^2+a^2)/(b^2-a^2).

### 9.5 Pressure vessel pitfalls

- Using **diameter** where the formula needs **radius** (sigma_h = pr/t, not pd/t).
- Forgetting hoop is 2× longitudinal — designing the weld for the wrong stress.
- Applying thin-wall formulas when r/t < 10.
- Forgetting that the cylinder wall is in **biaxial** stress when doing a failure-
  theory check.

---

## 10. Energy Methods

### 10.1 Strain energy

Work done by a slowly applied load is stored as **elastic strain energy U**. For a
linear-elastic member, U = (1/2)·(load)·(corresponding deflection).

**Strain energy by load type:**

```
Axial:    U = N^2 * L / (2*A*E)        or   int N(x)^2 / (2*A*E) dx
Torsion:  U = T^2 * L / (2*G*J)        or   int T(x)^2 / (2*G*J) dx
Bending:  U = int_0^L  M(x)^2 / (2*E*I) dx
Transverse shear: U = int  f_s * V(x)^2 / (2*G*A) dx   (f_s = form factor, usually neglected)
```

**Strain energy density** (energy per unit volume): u = sigma^2/(2E) for uniaxial
normal stress; u = tau^2/(2G) for pure shear.

### 10.2 Conservation of energy (direct method)

For a single load producing a single deflection at its point of application, set the
external work equal to the stored strain energy:

```
(1/2) * P * delta = U      =>   delta = 2U / P
```

Limited to one load / one deflection at the load point.

### 10.3 Castigliano's second theorem

The deflection (or rotation) at the point and in the direction of a load equals the
partial derivative of total strain energy with respect to that load:

```
delta_i = dU / dP_i           (deflection in the direction of force P_i)
theta_i = dU / dM_i           (rotation in the direction of couple M_i)
```

**Practical recipe (bending-dominated structures):**

1. If you want a deflection where no load acts, add a **dummy load Q** (or dummy
   couple) there.
2. Write M(x) for each region in terms of the real loads *and* Q.
3. delta = int_0^L [ M * (dM/dQ) / (E*I) ] dx, summed over regions.
4. Set Q = 0 *after* differentiating (if Q was fictitious).

The same structure works for trusses (sum over members of N·(dN/dP)·L/(AE)) and
shafts (torsion term). Castigliano also solves **indeterminate** problems: take the
redundant reaction as the "load," and the deflection in its direction is the known
support value (often zero) → solve dU/dR = 0 for the redundant.

### 10.4 Unit-load (virtual-work) method

Equivalent to Castigliano, often more direct for trusses and frames. To find the
deflection at a point:

```
1 * delta = sum [ n * N * L / (A*E) ]            (trusses)
1 * delta = int [ m(x) * M(x) / (E*I) ] dx       (beams/frames, bending term)
```

where N, M are the internal forces from the **real** loads, and n, m are the internal
forces from a **unit virtual load** applied at the point and direction of the desired
deflection. For a rotation, apply a unit virtual couple.

### 10.5 Impact / dynamic loading

A load W dropped from height h onto a structure of static stiffness produces an
**impact factor**:

```
delta_max = delta_st * [ 1 + sqrt(1 + 2h/delta_st) ]
n_impact  = 1 + sqrt(1 + 2h/delta_st)
```

where delta_st is the deflection W would cause if applied gradually. For a suddenly
applied load (h = 0), the impact factor is 2 — a suddenly applied load produces twice
the deflection and stress of a gradually applied one.

### 10.6 Energy-method pitfalls

- Differentiating *after* setting the dummy load to zero (must differentiate first).
- Forgetting to include all relevant energy terms — though for slender beams the
  bending term dominates and shear/axial are usually negligible.
- Sign of the dummy load defines the positive direction of the resulting deflection.

---

## 11. General Problem-Solving Patterns

### 11.1 The universal Mechanics of Materials workflow

1. **FBD and equilibrium** → external reactions.
2. **Internal resultants** → section the member, find N, V, M, T (draw diagrams if
   they vary).
3. **Determinate or indeterminate?** If indeterminate, add compatibility +
   constitutive relations before proceeding.
4. **Stress** at the critical point(s) from each resultant (N/A, Tc/J, Mc/I, VQ/Ib).
5. **Combine / transform** if multiaxial (superpose like stresses, then Mohr's
   circle for principals).
6. **Compare to allowable** — strength check (failure theory) and/or stiffness check
   (deflection, angle of twist) and/or stability check (buckling).
7. **Sanity-check** units, signs, and orders of magnitude.

### 11.2 Cross-cutting student pitfalls

- **Radius vs. diameter** — torsion and pressure-vessel formulas use radius; J and I
  use d^4 with different constants (J: d^4/32, I: d^4/64).
- **Centroid vs. arbitrary axis** — the neutral axis in bending and the reference for
  I must pass through the centroid.
- **Sign-convention drift** — pick conventions at the start and never switch
  mid-problem; the Mohr's-circle shear sign is the most error-prone.
- **Average vs. maximum** — V/A is the *average* shear; tau_max = 1.5 V/A for a
  rectangle. sigma = N/A is exact for axial but only nominal near discontinuities.
- **In-plane vs. absolute max shear** — include sigma_3 = 0 in plane-stress problems.
- **Determinacy** — counting unknowns vs. equations before reaching for compatibility.
- **Units** — 1 MPa = 1 N/mm^2; mixing kip/in/ksi with lb/ft is a constant source of
  factor-of-1000 and factor-of-12 errors.
- **Small-deflection assumption** — all the linear formulas (beam deflection, Euler
  buckling) assume small slopes; they break down for large deformations.

---

## Open-source sources used

- **Roylance, David.** *Mechanics of Materials.* MIT OpenCourseWare, hosted on
  Engineering LibreTexts (CC BY-NC-SA 4.0).
  https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_of_Materials_(Roylance)
  — chapters on tensile response, simple tensile/shear structures (pressure vessels,
  torsion), general stress/strain and stress transformation, bending, and yield/fracture.
- **Moore, Jacob, et al.** *Mechanics Map* open textbook (statics/mechanics, CC
  BY-NC-SA), Engineering LibreTexts and Penn State ROAM.
  https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.)
  and https://roam.libraries.psu.edu/node/1519 — internal resultants, shear/moment
  diagrams, section properties, equilibrium framework.
- **Lord, J., Davison, S., Richardson, A., Dillard, D.** *Strength of Materials*
  (Virginia Tech), Open Textbook Library (CC BY-NC-SA).
  https://open.umn.edu/opentextbooks/textbooks/1544 — scope and topic organization
  for an introductory one-semester Mechanics of Materials course.
- **Baker, D. and Haynes, W.** *Engineering Statics: Open and Interactive*, Open
  Textbook Library / Engineering LibreTexts (CC BY-NC-SA).
  https://engineeringstatics.org/ — equilibrium, FBDs, centroids and area moments of
  inertia, internal loadings (prerequisite material).
- **University of Prince Edward Island.** *Engineering Mechanics: Statics* open
  textbook (Pressbooks). https://pressbooks.library.upei.ca/statics/ — supplementary
  statics foundations.
- **Missouri S&T**, *Fundamental Mechanics of Materials Equations* formula sheet
  (open courseware handout). https://web.mst.edu/jthomas/classes/2210/formulas/ —
  cross-check of the standard formula set.
- **LibreTexts Engineering** Mechanical Engineering bookshelf (CC BY-NC-SA), general
  index. https://eng.libretexts.org/Bookshelves/Mechanical_Engineering
