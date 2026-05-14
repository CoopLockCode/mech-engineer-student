# Heat Transfer Reference

> Graduate-level study companion for ME 3440 (Heat Transfer). Covers conduction (1-D/2-D, transient, fins, lumped capacitance), convection (free and forced, internal and external, dimensionless groups, Nusselt correlations), radiation (blackbody, view factors, exchange), and heat exchangers (LMTD and effectiveness-NTU). Plain-text math: `*` multiply, `/` divide, `^` power, `d/dx` derivative, `del^2` Laplacian, Greek spelled out (rho, alpha, epsilon, sigma, theta).

---

## 0. The Three Modes and Foundational Concepts

### 0.1 The three modes of heat transfer
- **Conduction** — energy transfer through a stationary medium by molecular/electronic interaction. Needs a temperature gradient and a material.
- **Convection** — energy transfer between a surface and a moving fluid. Combines conduction (at the wall) with bulk fluid motion (advection).
- **Radiation** — energy transfer by electromagnetic waves; needs no medium (works in vacuum). Every surface above 0 K emits.

### 0.2 Heat flux vs heat rate; sign convention
- **Heat rate q** [W] — total energy per unit time.
- **Heat flux q'' ** [W/m^2] — heat rate per unit area: q = integral( q'' dA ).
- **Sign convention:** heat flows from high temperature to low temperature. In Fourier's law the minus sign enforces this — q'' is positive in the direction of *decreasing* T.

### 0.3 The conservation-of-energy framework
For a control volume:
```
E_dot_in - E_dot_out + E_dot_gen = E_dot_stored = dU/dt = rho*V*c_p*dT/dt
```
For a **surface** (no volume, no storage, no generation): E_dot_in = E_dot_out — this surface energy balance couples conduction, convection, and radiation at a boundary.

---

## 1. Conduction — Governing Laws

### 1.1 Fourier's law
```
q'' = -k * dT/dx           (1-D)
q''_vector = -k * del T    (general; heat flows down the gradient)
```
- **k** = thermal conductivity [W/(m*K)] — a material property. High for metals (Cu ~ 400, Al ~ 240), low for insulators (~0.03–0.1), intermediate for liquids, very low for gases.
- The minus sign: heat flows opposite the temperature gradient.

### 1.2 The heat diffusion (heat) equation
From an energy balance on a differential element with Fourier's law (constant k):
```
del^2 T + q_gen'''/k = (1/alpha) * dT/dt
Cartesian: d2T/dx2 + d2T/dy2 + d2T/dz2 + q'''/k = (1/alpha)*dT/dt
```
where **thermal diffusivity** alpha = k / (rho*c_p) [m^2/s] — measures how fast a material responds thermally (ratio of heat conducted to heat stored).

Special cases:
- Steady state: dT/dt = 0 -> del^2 T + q'''/k = 0 (**Poisson**); no generation -> del^2 T = 0 (**Laplace**).
- 1-D, steady, no generation, constant k: d2T/dx2 = 0 -> T is **linear** in x.
- Transient, no generation: dT/dt = alpha*del^2 T (the **diffusion equation**).

### 1.3 Boundary and initial conditions
- **1st kind (Dirichlet):** specified surface temperature, T(0,t) = T_s.
- **2nd kind (Neumann):** specified surface heat flux, -k*dT/dx|_0 = q''_s. Insulated/adiabatic/symmetry: dT/dx = 0.
- **3rd kind (Robin / convective):** -k*dT/dx|_0 = h*(T_infinity - T(0,t)).
A transient problem also needs an **initial condition** T(x,0).

---

## 2. Steady 1-D Conduction and Thermal Resistance

### 2.1 The thermal-resistance analogy
Heat flow is analogous to electric current: q = DT / R_th (DT ~ voltage, q ~ current, R_th ~ resistance). Resistances in **series add**; in **parallel** combine as reciprocals.

| Configuration | Thermal resistance R_th |
|---|---|
| Plane wall (thickness L, area A) | L / (k*A) |
| Cylindrical shell (r_1 to r_2, length L) | ln(r_2/r_1) / (2*pi*k*L) |
| Spherical shell (r_1 to r_2) | (1/r_1 - 1/r_2) / (4*pi*k) |
| Convection at a surface | 1 / (h*A) |
| Radiation at a surface | 1 / (h_r*A), with h_r = eps*sigma*(T_s+T_sur)*(T_s^2+T_sur^2) |
| Contact resistance between two solids | R''_t,c / A |

### 2.2 Composite walls and the overall heat transfer coefficient
For a composite wall with convection on both sides:
```
q = (T_inf,1 - T_inf,2) / R_total
R_total = 1/(h_1*A) + sum(L_i/(k_i*A)) + 1/(h_2*A)
Overall coefficient U:  q = U*A*DT_overall,  so  1/(U*A) = R_total
```

### 2.3 Conduction with thermal energy generation
1-D plane wall, generation q''', symmetric cooling, constant k:
```
d2T/dx2 + q'''/k = 0   ->   T(x) = -(q'''/(2k))*x^2 + C1*x + C2
Plane wall, T_s at both faces (half-thickness L):  T_max - T_s = q'''*L^2 / (2k)
Solid cylinder, radius r_o:  T_max - T_s = q'''*r_o^2 / (4k)
Solid sphere, radius r_o:    T_max - T_s = q'''*r_o^2 / (6k)
```
Apply BCs (symmetry at center, convection at surface) to find the constants.

### 2.4 The critical radius of insulation
Adding insulation to a small pipe/wire can *increase* heat loss because it adds conduction resistance but also adds outer surface area (lowering convection resistance). The total resistance is minimized at:
```
Cylinder:  r_cr = k_insulation / h
Sphere:    r_cr = 2*k_insulation / h
```
Add insulation beyond r_cr to reduce loss; below r_cr (e.g., insulating a thin wire) it *raises* loss — which is exploited to dissipate heat from current-carrying wires.

---

## 3. Extended Surfaces — Fins

### 3.1 Purpose and the fin equation
Fins increase the surface area available for convection. For a fin of uniform cross-section A_c, perimeter P, length L, with the excess temperature theta(x) = T(x) - T_infinity:
```
d2theta/dx2 - m^2 * theta = 0      where  m^2 = h*P / (k*A_c)
General solution:  theta(x) = C1*exp(m*x) + C2*exp(-m*x)
```
Assumptions: 1-D conduction along the fin, constant k and h, steady state, no generation, uniform cross-section.

### 3.2 Fin solutions by tip condition

| Tip condition | Temperature distribution theta/theta_b | Fin heat rate q_f |
|---|---|---|
| Infinitely long fin | exp(-m*x) | sqrt(h*P*k*A_c) * theta_b = M |
| Adiabatic (insulated) tip | cosh(m(L-x)) / cosh(mL) | M * tanh(mL) |
| Convective tip | (corrected-length form, below) | M * tanh(m*L_c) |
| Specified tip temperature | combination of sinh terms | (table form) |

where M = sqrt(h*P*k*A_c) * theta_b and theta_b = T_base - T_infinity.
**Corrected length** (simple, accurate way to handle a convecting tip): L_c = L + A_c/P. For a rectangular fin of thickness t: L_c = L + t/2. For a pin fin of diameter D: L_c = L + D/4.

### 3.3 Fin performance metrics
- **Fin effectiveness:** eps_f = q_f / (h*A_c,b*theta_b). Worth adding a fin only if eps_f > ~2; eps_f rises with k, with P/A_c (thin, closely spaced fins), and with low h.
- **Fin efficiency:** eta_f = q_f / q_max = q_f / (h*A_fin*theta_b), where q_max is the heat rate if the entire fin were at the base temperature. eta_f = tanh(m*L_c)/(m*L_c) for a straight fin with an adiabatic/corrected tip.
- **Overall surface efficiency** (finned + unfinned area): eta_o = 1 - (A_fin/A_total)*(1 - eta_f).

**Pitfall:** A fin always *reduces* the surface temperature; adding fins on a surface with already-high h (e.g., boiling) can be pointless or counterproductive (eps_f < 1).

---

## 4. Transient Conduction

### 4.1 Lumped capacitance method
Assumes the body has **negligible internal temperature gradients** — temperature is spatially uniform, varies only with time. Energy balance:
```
-h*A_s*(T - T_inf) = rho*V*c_p*dT/dt
Solution:  (T - T_inf)/(T_i - T_inf) = exp(-t/tau)
Time constant:  tau = rho*V*c_p / (h*A_s) = R_th * C_th
```

**Validity — the Biot number:**
```
Bi = h*L_c / k_solid          L_c = V / A_s  (characteristic length)
Lumped capacitance valid when  Bi < 0.1
```
Bi compares internal conduction resistance to surface convection resistance. Bi << 1 means the body conducts heat internally far faster than it loses it at the surface, so it stays nearly uniform.

### 4.2 The Fourier number
```
Fo = alpha*t / L_c^2          (dimensionless time)
```
Physically, the ratio of the rate of heat conduction to the rate of heat storage. Fo >> 1 means the transient is well advanced.

### 4.3 One-term approximation (one-dimensional transient, Bi > 0.1)
For a plane wall, infinite cylinder, or sphere with convective surfaces, when **Fo > 0.2**, the infinite series solution is dominated by its first term:
```
theta* = (T - T_inf)/(T_i - T_inf) = C_1 * exp(-zeta_1^2 * Fo) * f(zeta_1 * x*)
```
- zeta_1 and C_1 are tabulated functions of Bi (different tables for wall, cylinder, sphere).
- f is cos(zeta_1*x*) for a wall, J_0 for a cylinder, sin(zeta_1*r*)/(zeta_1*r*) for a sphere.
- These are the **Heisler charts** in graphical form (midplane temperature, position correction, and total heat transfer Q/Q_max charts).

### 4.4 Semi-infinite solid
A body so thick the far face never feels the surface change (valid while the thermal penetration depth < body thickness). For a sudden surface temperature change to T_s:
```
(T(x,t) - T_i)/(T_s - T_i) = erfc( x / (2*sqrt(alpha*t)) )
Surface heat flux:  q''_s(t) = k*(T_s - T_i) / sqrt(pi*alpha*t)
```
Other cases: constant surface flux, and surface convection (involves erfc with an exponential term). Thermal penetration depth ~ sqrt(alpha*t).

### 4.5 Multidimensional transient — product solution
A 2-D or 3-D transient body that is the geometric *intersection* of 1-D systems (e.g., a short cylinder = infinite cylinder ∩ plane wall) has a solution that is the **product** of the 1-D dimensionless temperatures:
```
theta*_2D(x,r,t) = theta*_wall(x,t) * theta*_cylinder(r,t)
```

---

## 5. Convection — Fundamentals and Dimensionless Groups

### 5.1 Newton's law of cooling
```
q'' = h * (T_s - T_infinity)        q = h*A_s*(T_s - T_infinity)
```
**h** = the convection heat transfer coefficient [W/(m^2*K)] — NOT a property; it depends on geometry, flow, fluid properties, and surface conditions. The whole subject of convection is *predicting h*.

### 5.2 The thermal boundary layer
Just as the velocity boundary layer is where the velocity adjusts from 0 to U_infinity, the **thermal boundary layer** is where the temperature adjusts from T_s to T_infinity. At the wall, heat enters the fluid purely by conduction (the fluid is stationary there — no-slip), so:
```
h = -k_fluid * (dT/dy)|_wall / (T_s - T_infinity)
```
This is the link between conduction at the wall and the convection coefficient. A thinner thermal boundary layer (steeper wall gradient) -> higher h.

### 5.3 The key dimensionless groups in convection

| Group | Definition | Physical meaning | Role |
|---|---|---|---|
| Nusselt number, Nu | h*L / k_fluid | dimensionless temperature gradient at the wall; convection / pure-conduction across the same fluid layer | the *output* of a correlation; Nu = 1 means pure conduction |
| Reynolds number, Re | rho*V*L/mu = V*L/nu | inertia / viscous forces | sets laminar vs turbulent in forced convection |
| Prandtl number, Pr | nu/alpha = mu*c_p/k | momentum diffusivity / thermal diffusivity | relates the velocity and thermal boundary-layer thicknesses (delta/delta_t ~ Pr^(1/3)) |
| Grashof number, Gr | g*beta*(T_s-T_inf)*L^3 / nu^2 | buoyancy / viscous forces | the "Reynolds number" of free convection |
| Rayleigh number, Ra | Gr*Pr = g*beta*(T_s-T_inf)*L^3 / (nu*alpha) | drives free convection; onset of buoyant flow | the *input* for free-convection correlations |
| Peclet number, Pe | Re*Pr = V*L/alpha | advection / conduction of heat | appears in internal-flow entry-length scaling |
| Stanton number, St | h/(rho*V*c_p) = Nu/(Re*Pr) | convected heat / thermal capacity of the flow | used with the Reynolds analogy |

- **Pr meaning:** gases Pr ~ 0.7 (velocity and thermal BLs comparable); liquid metals Pr << 1 (thermal BL much thicker); oils Pr >> 1 (thermal BL much thinner).
- **beta** = volumetric thermal expansion coefficient; for an ideal gas, beta = 1/T (T absolute).

### 5.4 The Reynolds analogy
Because momentum and heat transfer are governed by similar equations, for Pr ≈ 1: C_f/2 = St = Nu/(Re*Pr). The **modified (Chilton–Colburn) analogy** extends it: C_f/2 = St*Pr^(2/3) for 0.6 < Pr < 60. Lets you estimate h from drag data and vice versa.

### 5.5 Property evaluation — the film temperature
For external flow and free convection, evaluate fluid properties at the **film temperature**:
```
T_film = (T_s + T_infinity) / 2
```
For internal flow, evaluate at the **mean (bulk) fluid temperature** T_m, often the average of inlet and outlet bulk temperatures. **Pitfall:** using properties at the wrong reference temperature is a silent, common error.

---

## 6. Forced Convection — Correlations

### 6.1 External flow correlations

| Geometry / regime | Correlation | Validity |
|---|---|---|
| Flat plate, laminar, local | Nu_x = 0.332 * Re_x^(1/2) * Pr^(1/3) | Re_x < 5e5, Pr > 0.6 |
| Flat plate, laminar, average | Nu_L = 0.664 * Re_L^(1/2) * Pr^(1/3) | Re_L < 5e5 |
| Flat plate, turbulent, local | Nu_x = 0.0296 * Re_x^(4/5) * Pr^(1/3) | 5e5 < Re_x < 1e7 |
| Flat plate, mixed (lam+turb), avg | Nu_L = (0.037*Re_L^(4/5) - 871) * Pr^(1/3) | Re_x,c = 5e5 |
| Cylinder in cross-flow (Hilpert) | Nu_D = C * Re_D^m * Pr^(1/3) | C, m tabulated by Re_D range |
| Cylinder in cross-flow (Churchill–Bernstein) | Nu_D = 0.3 + (0.62*Re_D^(1/2)*Pr^(1/3))/[1+(0.4/Pr)^(2/3)]^(1/4) * [1+(Re_D/282000)^(5/8)]^(4/5) | Re_D*Pr > 0.2 (all Re_D) |
| Sphere (Whitaker) | Nu_D = 2 + (0.4*Re_D^(1/2) + 0.06*Re_D^(2/3))*Pr^0.4 * (mu_inf/mu_s)^(1/4) | 3.5 < Re_D < 7.6e4 |
| Tube banks (Zukauskas) | Nu_D = C * Re_D,max^m * Pr^0.36 * (Pr/Pr_s)^(1/4) | configuration-dependent C, m |

Note: a sphere always has Nu_D -> 2 as Re_D -> 0 (pure conduction limit into an infinite stagnant medium).

### 6.2 Internal (pipe) flow — fully developed

**Laminar, fully developed (analytical, exact):**
```
Constant surface heat flux:        Nu_D = 4.36
Constant surface temperature:      Nu_D = 3.66
```
Note: laminar Nu is *constant* — h does not depend on Re or Pr once fully developed.

**Turbulent, fully developed:**

| Correlation | Form | Validity |
|---|---|---|
| Dittus–Boelter | Nu_D = 0.023 * Re_D^(4/5) * Pr^n; n = 0.4 heating, n = 0.3 cooling | Re_D > 1e4, 0.6 < Pr < 160, L/D > 10 |
| Colburn | Nu_D = 0.023 * Re_D^(4/5) * Pr^(1/3) | similar range |
| Sieder–Tate (large property variation) | Nu_D = 0.027 * Re_D^(4/5) * Pr^(1/3) * (mu/mu_s)^0.14 | accounts for temperature-dependent viscosity |
| Gnielinski (most accurate, wide range) | Nu_D = (f/8)*(Re_D-1000)*Pr / [1 + 12.7*(f/8)^(1/2)*(Pr^(2/3)-1)] | 3000 < Re_D < 5e6; f = (0.790*ln(Re_D)-1.64)^(-2) |

### 6.3 Internal flow — energy balance and outlet temperature
The mean temperature rises along the tube. With m_dot and c_p:
```
q = m_dot * c_p * (T_m,out - T_m,in)
```
- **Constant surface heat flux q''_s:** T_m(x) rises *linearly*; T_m,out = T_m,in + q''_s*P*L/(m_dot*c_p).
- **Constant surface temperature T_s:** T_m approaches T_s *exponentially*:
  ```
  (T_s - T_m,out)/(T_s - T_m,in) = exp( -h*P*L / (m_dot*c_p) )
  q = h*A_s*DT_lm, with DT_lm the log-mean temperature difference (see Section 9)
  ```

### 6.4 Internal flow — entry lengths
```
Laminar:    L_h/D ≈ 0.05*Re_D ;  L_t/D ≈ 0.05*Re_D*Pr
Turbulent:  L_h/D ≈ L_t/D ≈ 10  (often taken as 10–60 diameters)
```
In the entry region, h is higher than the fully developed value and decreases toward it.

---

## 7. Free (Natural) Convection — Correlations

### 7.1 The driving mechanism
No external flow; motion is driven by **buoyancy** from density differences caused by temperature differences. The relevant parameter is the **Rayleigh number** Ra = Gr*Pr. Below a critical Ra the fluid stays stagnant (pure conduction); above it, buoyant cells form.

### 7.2 General correlation form
```
Nu = C * Ra^n
```
n ≈ 1/4 for laminar free convection, n ≈ 1/3 for turbulent free convection (then Nu becomes independent of the length scale).

### 7.3 Common free-convection correlations

| Geometry | Correlation | Notes |
|---|---|---|
| Vertical plate (Churchill–Chu) | Nu = {0.825 + 0.387*Ra_L^(1/6) / [1+(0.492/Pr)^(9/16)]^(8/27) }^2 | all Ra_L; L = plate height |
| Vertical plate, laminar | Nu_L = 0.59 * Ra_L^(1/4) | 1e4 < Ra_L < 1e9 |
| Horizontal plate, hot side up (or cold down) | Nu = 0.54*Ra_L^(1/4) (1e4–1e7); 0.15*Ra_L^(1/3) (1e7–1e11) | L_c = A_s/P |
| Horizontal plate, hot side down (or cold up) | Nu = 0.27 * Ra_L^(1/4) | 1e5 < Ra_L < 1e10 |
| Horizontal cylinder (Churchill–Chu) | Nu_D = {0.60 + 0.387*Ra_D^(1/6)/[1+(0.559/Pr)^(9/16)]^(8/27)}^2 | Ra_D < 1e12 |
| Sphere | Nu_D = 2 + 0.589*Ra_D^(1/4) / [1+(0.469/Pr)^(9/16)]^(4/9) | Ra_D < 1e11, Pr > 0.7 |

### 7.4 Mixed convection
When forced and free convection are comparable, compare Gr/Re^2:
- Gr/Re^2 << 1: forced convection dominates.
- Gr/Re^2 >> 1: free convection dominates.
- Gr/Re^2 ~ 1: mixed — combine as Nu^3 = Nu_forced^3 ± Nu_free^3 (sign depends on assisting/opposing flow).

---

## 8. Radiation

### 8.1 Blackbody radiation laws
A **blackbody** is the ideal emitter and absorber: absorbs all incident radiation, emits the maximum possible at every wavelength and temperature.
```
Stefan–Boltzmann (total blackbody emissive power):  E_b = sigma * T^4
   sigma = 5.670e-8 W/(m^2*K^4),  T absolute
Planck's law:  spectral distribution E_b,lambda(lambda, T)
Wien's displacement law:  lambda_max * T = 2898 micron*K  (peak shifts to shorter wavelength as T rises)
```

### 8.2 Real surfaces — radiative properties
- **Emissivity epsilon** = E / E_b — ratio of actual emission to blackbody emission (0 <= eps <= 1).
- **Absorptivity alpha** = fraction of incident radiation absorbed.
- **Reflectivity rho** and **transmissivity tau**: alpha + rho + tau = 1 (for opaque surfaces tau = 0, so alpha + rho = 1).
- **Kirchhoff's law:** at thermal equilibrium, eps = alpha (for a given wavelength and direction; the gray-surface approximation extends it to total values).
- **Gray surface** — eps and alpha independent of wavelength. **Diffuse surface** — independent of direction. The "diffuse-gray" assumption underlies most engineering radiation analysis.

### 8.3 Radiation heat transfer between a surface and large surroundings
```
q = eps * sigma * A_s * (T_s^4 - T_sur^4)
Radiation heat transfer coefficient:  h_r = eps*sigma*(T_s + T_sur)*(T_s^2 + T_sur^2)
   so that  q = h_r * A_s * (T_s - T_sur)  — lets radiation join the resistance network
```

### 8.4 View factors (configuration / shape factors)
The **view factor F_ij** = the fraction of radiation leaving surface i that strikes surface j. Properties:
- **Reciprocity:** A_i * F_ij = A_j * F_ji.
- **Summation rule:** for an enclosure, sum_j F_ij = 1 (all radiation leaving i must land somewhere).
- **Superposition** and **symmetry** rules help build unknown factors from known ones.
- A flat or convex surface cannot see itself: F_ii = 0. A concave surface can: F_ii > 0.

### 8.5 Radiation exchange in an enclosure of diffuse-gray surfaces
Network method — two resistance types:
- **Surface resistance** (a surface being non-black): R_surface = (1 - eps_i) / (eps_i * A_i). Drives between the blackbody emissive power E_bi = sigma*T_i^4 and the **radiosity** J_i (total radiation leaving the surface).
- **Space (geometric) resistance** between surfaces i and j: R_space = 1 / (A_i * F_ij). Drives between J_i and J_j.
```
Net radiation from surface i:  q_i = (E_bi - J_i) / [(1-eps_i)/(eps_i*A_i)]
Net exchange between i and j:   q_ij = (J_i - J_j) / (1/(A_i*F_ij))
```
**Two-surface enclosure** (very common — concentric cylinders/spheres, parallel plates, small object in large surroundings):
```
q_12 = sigma*(T_1^4 - T_2^4) / [ (1-eps_1)/(eps_1*A_1) + 1/(A_1*F_12) + (1-eps_2)/(eps_2*A_2) ]
```
Limiting cases of the two-surface result:
- Large parallel plates (A_1 = A_2 = A, F_12 = 1): q = sigma*A*(T_1^4 - T_2^4) / (1/eps_1 + 1/eps_2 - 1).
- Small convex object 1 in a large enclosure 2 (A_1/A_2 -> 0): q = eps_1*sigma*A_1*(T_1^4 - T_2^4).
- **Radiation shields** — inserting a thin low-emissivity sheet adds two surface resistances and a space resistance in series, sharply cutting the net exchange.

### 8.6 Radiation pitfalls
- **Always use absolute temperature** — radiation is a T^4 law; °C is meaningless.
- The T^4 difference is *not* the same as (DT)^4 or 4*T^3*DT except for small DT.
- Don't conflate emissivity (emission) with absorptivity unless Kirchhoff's-law conditions hold (gray surface, or matched spectra).
- A surface in an enclosure can radiate to itself if concave — don't assume F_ii = 0.

---

## 9. Heat Exchangers

### 9.1 Types and classification
- **By flow arrangement:** parallel-flow (both fluids same direction), counterflow (opposite — thermodynamically superior), cross-flow (perpendicular; fluids "mixed" or "unmixed").
- **By construction:** double-pipe (concentric tube), shell-and-tube (with pass arrangements), compact (plate, plate-fin — high area density).

### 9.2 The overall heat transfer coefficient
Series resistances from hot fluid to cold fluid, including wall conduction and fouling:
```
1/(U*A) = 1/(h_i*A_i) + R''_f,i/A_i + R_wall + R''_f,o/A_o + 1/(h_o*A_o)
```
R''_f = fouling factor (deposit buildup over service life). For a thin wall, U*A is referenced consistently to one area (A_i or A_o).

### 9.3 The LMTD method
Use when **all four terminal temperatures are known (or easily found)** — typically a *rating/sizing* problem where outlets are specified.
```
q = U * A * F * DT_lm
DT_lm = (DT_1 - DT_2) / ln(DT_1/DT_2)
```
- DT_1, DT_2 = temperature differences between the hot and cold streams at the two ends of the exchanger.
- **Parallel-flow:** DT_1 = T_h,in - T_c,in ; DT_2 = T_h,out - T_c,out.
- **Counterflow:** DT_1 = T_h,in - T_c,out ; DT_2 = T_h,out - T_c,in.
- **F** = correction factor (= 1 for pure parallel or pure counterflow; < 1 for cross-flow and multipass shell-and-tube, read from charts as a function of P and R parameters).
- For the *same* terminal temperatures, **counterflow gives a larger DT_lm** -> needs less area, and counterflow can have T_c,out > T_h,out (impossible in parallel flow).

### 9.4 The effectiveness–NTU method
Use when **outlet temperatures are unknown** — typically a *performance prediction* problem with a given exchanger.

Definitions:
```
Heat capacity rates:  C = m_dot * c_p   for each stream;  C_min, C_max are the smaller/larger
Maximum possible heat rate:  q_max = C_min * (T_h,in - T_c,in)
Effectiveness:  epsilon = q / q_max = (actual heat transfer) / (max possible)
Number of transfer units:  NTU = U*A / C_min
Capacity ratio:  C_r = C_min / C_max
```
Then epsilon = f(NTU, C_r, flow arrangement), and once epsilon is known: q = epsilon * C_min * (T_h,in - T_c,in).

| Arrangement | epsilon = f(NTU, C_r) |
|---|---|
| Parallel-flow | eps = [1 - exp(-NTU*(1+C_r))] / (1 + C_r) |
| Counterflow (C_r < 1) | eps = [1 - exp(-NTU*(1-C_r))] / [1 - C_r*exp(-NTU*(1-C_r))] |
| Counterflow (C_r = 1) | eps = NTU / (1 + NTU) |
| Any arrangement, C_r = 0 (e.g. condenser/evaporator/boiler) | eps = 1 - exp(-NTU) |
| Cross-flow, both unmixed (approx.) | eps = 1 - exp{ (NTU^0.22/C_r)*[exp(-C_r*NTU^0.78) - 1] } |

- **C_r = 0** applies when one fluid undergoes phase change (its temperature is constant, so its effective c_p -> infinity, C -> infinity).
- For a fixed NTU, **counterflow yields the highest effectiveness** of all arrangements.
- As NTU -> infinity, eps -> 1 for C_r = 0, and eps -> 1/(1+C_r) for parallel flow (parallel flow can never reach eps = 1).

### 9.5 Worked-example patterns — heat exchangers
- **LMTD (sizing):** known inlets and outlets -> q from an energy balance on one stream -> DT_lm -> F (if needed) -> solve q = U*A*F*DT_lm for A.
- **NTU (rating):** known inlets, geometry, U, A -> C_min, C_max, C_r -> NTU = UA/C_min -> eps from the relation -> q = eps*C_min*DT_max -> outlet temperatures from energy balances.
- Energy balances tie it together: q = C_h*(T_h,in - T_h,out) = C_c*(T_c,out - T_c,in).

---

## 10. Master List of Common Student Pitfalls

1. **Absolute temperature in radiation** — E_b = sigma*T^4 and all radiation exchange require K or R. This is the single most common radiation error.
2. **h is not a property** — never look it up in a table the way you do k; it must come from a correlation or be given.
3. **Reference temperature for properties** — film temperature for external flow / free convection; mean bulk temperature for internal flow. Using the wrong one quietly corrupts every property.
4. **Biot vs Nusselt** — both look like h*L/k, but Bi uses k of the *solid* (governs transient conduction validity), Nu uses k of the *fluid* (the convection result). Mixing them is a classic trap.
5. **Lumped capacitance check** — always verify Bi < 0.1 *before* using exp(-t/tau). If Bi > 0.1, you need the one-term/Heisler approach.
6. **Characteristic length** — L_c = V/A_s for lumped capacitance and Biot; the half-thickness for a plane wall in the one-term solution; D for cylinders/spheres in correlations. They are not interchangeable.
7. **Fourier number gate** — the one-term approximation needs Fo > 0.2; for smaller Fo use the full series or charts.
8. **Heating vs cooling exponent** — Dittus–Boelter uses Pr^0.4 when the fluid is being heated, Pr^0.3 when cooled.
9. **Laminar internal Nu is constant** — Nu = 4.36 (constant flux) or 3.66 (constant T_s); it does *not* depend on Re. Don't apply a turbulent correlation in the laminar regime.
10. **Resistances: series vs parallel** — composite walls in series add; parallel paths combine reciprocally. Drawing the circuit prevents errors.
11. **Critical radius of insulation** — adding insulation to a thin pipe/wire can *increase* heat loss; check r vs r_cr.
12. **Fin effectiveness** — a fin is only worthwhile if eps_f > ~2; on a high-h surface a fin can hurt.
13. **LMTD end-difference definitions differ** between parallel and counterflow — assigning DT_1 and DT_2 wrong is common; counterflow uses (hot-in vs cold-out) and (hot-out vs cold-in).
14. **Cross-flow / multipass needs the F factor** — q = U*A*F*DT_lm with F < 1; forgetting F overpredicts performance.
15. **C_min is whichever stream has the smaller m_dot*c_p**, not the smaller mass flow rate or the smaller c_p alone.
16. **Phase-change stream -> C_r = 0** — a boiling or condensing fluid has effectively infinite heat capacity rate.
17. **q_max uses C_min and the inlet temperature difference** — q_max = C_min*(T_h,in - T_c,in), never C_max.
18. **Steady vs transient** — check whether dT/dt = 0 before reaching for steady-state resistance formulas.
19. **Sign of the Fourier-law gradient** — heat flows down the gradient; keep the minus sign or you will get the direction wrong.
20. **View factor self-viewing** — concave surfaces have F_ii > 0; flat/convex have F_ii = 0.

---

## Open-source sources used

- **Lienhard, John H. IV and Lienhard, John H. V.** *A Heat Transfer Textbook*, 6th edition. Freely downloadable from MIT (Dover/MIT, CC-licensed for personal and non-profit instructional use). https://ahtt.mit.edu/ and table of contents https://ahtt.mit.edu/table-of-contents/ — used for conduction concepts and thermal resistance, the overall heat transfer coefficient, fin design, transient and multidimensional conduction, laminar/turbulent boundary layers, forced and natural convection correlations, radiative heat transfer, and heat exchanger design (LMTD and effectiveness–NTU).
- **MIT OpenCourseWare**, 2.51 / 2.55 / 16.unified Heat Transfer course materials — cross-reference for the heat diffusion equation derivation, the lumped-capacitance and one-term transient solutions, Biot/Fourier numbers, and the Reynolds analogy.
- **Engineering LibreTexts — Heat Transfer / Thermodynamics bookshelf.** https://eng.libretexts.org/Bookshelves/Mechanical_Engineering — cross-reference for the conduction–convection–radiation framework, the resistance analogy, and dimensionless-group definitions.
- **Wikipedia** (cross-reference only, for the standard forms of the Churchill–Bernstein, Dittus–Boelter, Gnielinski, Churchill–Chu, and Zukauskas correlations and the Nusselt/Rayleigh/Prandtl number definitions): "Nusselt number," "Churchill–Bernstein equation," "Dittus–Boelter equation."
