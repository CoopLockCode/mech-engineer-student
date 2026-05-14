# Fluid Mechanics Reference

> Graduate-level study companion for ME 3343 (Fluid Mechanics / Fluid Dynamics). Covers fluid properties, fluid statics, control-volume analysis (continuity, momentum, energy), Bernoulli, dimensional analysis and similitude, internal flow (laminar/turbulent, Moody chart, head loss), external flow (drag, lift, boundary layers), and the Navier–Stokes equations. Plain-text math: `*` multiply, `/` divide, `^` power, `d/dx` derivative, `D/Dt` material derivative, `del` for the gradient operator, Greek spelled out (rho, mu, nu, tau).

---

## 0. Fluid Properties and Foundational Concepts

### 0.1 What is a fluid
A **fluid** deforms continuously under *any* applied shear stress, no matter how small. A solid resists shear with a finite static deformation; a fluid keeps flowing. Fluids include liquids (nearly incompressible, form a free surface) and gases (highly compressible, fill their container).

### 0.2 The continuum hypothesis
We treat fluid properties (rho, P, T, V) as continuous point functions, ignoring molecular discreteness. Valid when the **Knudsen number** Kn = (molecular mean free path) / (characteristic length) << 1. Breaks down in rarefied gases / micro-scale flows.

### 0.3 Core properties

| Property | Symbol | Definition / relation | Units (SI) |
|---|---|---|---|
| Density | rho | mass per unit volume | kg/m^3 |
| Specific volume | v | 1/rho | m^3/kg |
| Specific weight | gamma | rho*g | N/m^3 |
| Specific gravity | SG | rho / rho_water (4°C, 1000 kg/m^3) | — |
| Dynamic viscosity | mu | tau / (du/dy) for Newtonian fluid | Pa*s = kg/(m*s) |
| Kinematic viscosity | nu | mu / rho | m^2/s |
| Bulk modulus | E_v | -v*(dP/dv) = rho*(dP/drho) | Pa |
| Surface tension | sigma | energy per unit area / force per unit length | N/m |
| Vapor pressure | P_v | pressure at which a liquid boils at given T | Pa |

### 0.4 Viscosity and Newton's law of viscosity
For a **Newtonian fluid**, shear stress is linearly proportional to the rate of strain:
```
tau = mu * (du/dy)
```
- du/dy is the velocity gradient (rate of shearing strain).
- **No-slip condition:** fluid velocity at a solid wall equals the wall velocity. This is what generates the velocity gradient and therefore wall shear.
- **Non-Newtonian fluids:** shear-thinning (pseudoplastic — paint, blood), shear-thickening (dilatant — cornstarch slurry), Bingham plastic (yield stress — toothpaste, mud).
- Liquid viscosity *decreases* with temperature; gas viscosity *increases* with temperature (different molecular mechanisms — cohesion vs momentum exchange).

### 0.5 Compressibility, bulk modulus, speed of sound
```
E_v = rho * dP/drho        Speed of sound  c = sqrt(dP/drho)|_s = sqrt(k*R*T)  (ideal gas)
Mach number  Ma = V / c
```
- Ma < 0.3: flow treated as **incompressible** (density changes < ~5%).
- Ma ~ 1 transonic, Ma > 1 supersonic, Ma >> 1 hypersonic.

### 0.6 Surface tension and capillarity
- Pressure jump across a curved interface: droplet DP = 2*sigma/R, bubble (two surfaces) DP = 4*sigma/R, cylindrical jet DP = sigma/R.
- Capillary rise in a tube: h = 2*sigma*cos(theta) / (rho*g*R), where theta is the contact angle (theta < 90° wetting -> rise; > 90° -> depression, e.g. mercury).

### 0.7 Vapor pressure and cavitation
When local pressure drops to P_v, the liquid vaporizes locally — **cavitation**. The bubbles collapse violently downstream, eroding pump impellers and propellers. Avoided by keeping local P above P_v (quantified by the cavitation number / NPSH for pumps).

---

## 1. Fluid Statics

### 1.1 The hydrostatic pressure equation
In a fluid at rest, pressure varies only with depth (no shear because no motion):
```
dP/dz = -rho*g          (z measured upward)
```
For an **incompressible** fluid (constant rho):
```
P = P_0 + rho*g*h       (h = depth below the reference surface)
```
Key consequences:
- Pressure is the **same at all points at the same depth** in a connected fluid of constant density (Pascal).
- Pressure is **independent of container shape** (hydrostatic paradox).
- Pressure at a point acts **equally in all directions** (Pascal's law — proved from a fluid wedge force balance).

For a **compressible** fluid (e.g. atmosphere, isothermal ideal gas): integrate dP/P = -(g/(R*T)) dz to get P = P_0 * exp(-g*z/(R*T)).

### 1.2 Manometry
Walk through the manometer adding rho*g*h going down, subtracting going up:
```
P_1 + sum(rho_i * g * h_i, down) - sum(rho_j * g * h_j, up) = P_2
```
Differential manometer between two pipes: P_A - P_B = (rho_manometer - rho_fluid)*g*h.

### 1.3 Hydrostatic force on a plane surface
For a flat submerged plate:
```
F_R = P_C * A = rho*g*h_C * A         (h_C = depth of the centroid)
```
The resultant acts at the **center of pressure** (below the centroid):
```
y_CP = y_C + I_xc / (y_C * A)
```
where I_xc is the second moment of area about the centroidal x-axis, y measured along the plate from the free surface. The center of pressure is always below the centroid because pressure increases with depth.

### 1.4 Hydrostatic force on a curved surface
Decompose into components:
- **Horizontal component** = force on the vertical projection of the curved surface (use the plane-surface method).
- **Vertical component** = weight of the (real or virtual) fluid column above the surface up to the free surface.
- Resultant magnitude = sqrt(F_H^2 + F_V^2); line of action passes through where the two component lines intersect.

### 1.5 Buoyancy — Archimedes' principle
```
F_B = rho_fluid * g * V_displaced
```
The buoyant force acts upward through the **centroid of the displaced volume** (the center of buoyancy). A body floats when F_B = W; it is **neutrally buoyant** when rho_body = rho_fluid.

**Stability of a floating body:** stable if the **metacenter M** lies above the center of gravity G. Metacentric height GM = I_waterplane / V_submerged - GB. GM > 0 -> stable.

### 1.6 Rigid-body motion of fluids (no relative motion -> still "statics")
- **Linear acceleration a_x, a_z:** lines of constant pressure tilt; slope = -a_x/(g + a_z). Pressure gradient: del P = rho*(g_vector - a_vector).
- **Rigid-body rotation (omega):** free surface becomes a paraboloid, z = z_0 + omega^2 * r^2 / (2g). Pressure increases with r^2.

---

## 2. Fluid Kinematics

### 2.1 Lagrangian vs Eulerian description
- **Lagrangian** — follow individual fluid particles (like tracking cars).
- **Eulerian** — fix points in space and watch what flows through (like traffic cameras). Fluid mechanics is overwhelmingly Eulerian.

### 2.2 The material (substantial) derivative
The rate of change following a fluid particle, expressed in Eulerian terms:
```
D( )/Dt = d( )/dt + (V . del)( )
        = local (unsteady) part + convective part
e.g. acceleration  a = DV/Dt = dV/dt + (V.del)V
```
A flow can be steady (dV/dt = 0) yet still have particle acceleration through the convective term (e.g. steady flow through a nozzle).

### 2.3 Flow visualization lines
- **Streamline** — tangent to the velocity field at an instant. dx/u = dy/v = dz/w.
- **Pathline** — actual trajectory of one particle over time.
- **Streakline** — locus of all particles that passed through a fixed point (a dye trace).
In **steady flow** streamlines, pathlines, and streaklines coincide.

### 2.4 Rates of motion of a fluid element
A fluid element undergoes: translation, linear (volumetric) strain, rotation, and angular (shear) strain.
- **Volumetric strain rate** = del . V = du/dx + dv/dy + dw/dz (the divergence). For incompressible flow this is zero.
- **Vorticity** zeta = del x V = twice the angular velocity of a fluid element. **Irrotational flow** has zeta = 0.

### 2.5 The Reynolds Transport Theorem (RTT)
The bridge between a *system* (control mass) and a *control volume*. For any extensive property B with intensive counterpart b = B/m:
```
dB_sys/dt = d/dt( integral_CV rho*b dV ) + integral_CS rho*b*(V_rel . n) dA
```
Left side = rate of change following the matter; right side = rate of storage in the CV + net efflux through the control surface. Setting b = 1 (mass), b = V (momentum), b = e (energy) generates the three conservation laws.

---

## 3. Control-Volume Analysis (Integral Conservation Laws)

### 3.1 Conservation of mass (continuity)
From RTT with b = 1, and dm_sys/dt = 0:
```
d/dt( integral_CV rho dV ) + integral_CS rho*(V_rel . n) dA = 0
```
Steady flow:  sum(m_dot_out) = sum(m_dot_in),  where  m_dot = rho*A*V_avg.
Incompressible, single inlet/outlet:  A_1*V_1 = A_2*V_2 (the area–velocity relation: flow speeds up where the duct narrows).

### 3.2 Linear momentum equation
From RTT with b = V (Newton's second law for a CV):
```
sum(F) = d/dt( integral_CV rho*V dV ) + integral_CS V * rho*(V_rel . n) dA
```
Steady flow, uniform inlet/outlet profiles:
```
sum(F) = sum(m_dot*V)_out - sum(m_dot*V)_in
```
- **sum(F)** includes pressure forces on the control surface, body forces (weight), and reaction forces from solids (anchoring forces — usually the unknown).
- It is a **vector equation** — write separate x, y, z components.
- Use **gauge pressure** on the control surface (atmospheric cancels around a closed CS).
- For a moving CV, use velocities **relative to the CV**; for a deforming/accelerating CV, add the appropriate terms.

**Worked-example pattern (momentum):**
1. Draw the CV; choose it so unknown forces appear as surface forces.
2. Set a coordinate system; mark all inlet/outlet velocities and pressures.
3. Apply continuity to relate flow rates.
4. Write momentum in x and y; include pressure*area, weight, and the reaction force R.
5. Solve for R; the force on the *device* is -R (Newton's third law).

Classic applications: force on a pipe bend, force of a jet on a plate/vane, thrust of a rocket/jet, hydraulic jump, propeller/wind-turbine actuator disk.

### 3.3 Angular momentum equation
```
sum(M) = sum(r x m_dot*V)_out - sum(r x m_dot*V)_in
```
Basis for turbomachinery analysis — the **Euler turbomachine equation**: T_shaft = m_dot*(r_2*V_t2 - r_1*V_t1), where V_t is the tangential velocity component.

### 3.4 Energy equation for a control volume
From RTT with b = e = u + V^2/2 + g*z, combined with the first law:
```
Q_dot - W_dot_shaft = d/dt(integral_CV rho*e dV)
                      + integral_CS (h + V^2/2 + g*z) rho*(V_rel.n) dA
```
Steady, single inlet (1) / outlet (2), with the **head form** (divide by m_dot*g):
```
P_1/(rho*g) + alpha_1*V_1^2/(2g) + z_1 + h_pump
   = P_2/(rho*g) + alpha_2*V_2^2/(2g) + z_2 + h_turbine + h_L
```
- **h_pump** = energy head added by a pump; **h_turbine** = head extracted; **h_L** = head loss to friction (irreversibility).
- **alpha** = kinetic-energy correction factor accounting for a non-uniform velocity profile: alpha = 1 for uniform, alpha ≈ 2 for laminar pipe flow, alpha ≈ 1.05 for turbulent pipe flow.
- Pump power: W_dot_pump = rho*g*Q*h_pump / eta_pump.

---

## 4. The Bernoulli Equation

### 4.1 Statement and the five assumptions
Along a streamline:
```
P/(rho*g) + V^2/(2g) + z = constant      (head form)
P + (1/2)*rho*V^2 + rho*g*z = constant   (pressure form)
```
**Assumptions (memorize — every Bernoulli error traces to a violated assumption):**
1. Steady flow.
2. Incompressible flow.
3. **Frictionless / inviscid** (no head loss).
4. Along a single streamline (or everywhere, if the flow is also irrotational).
5. **No shaft work** (no pump/turbine) and no heat transfer between the two points.

Bernoulli is the energy equation stripped of h_L, h_pump, h_turbine — it is an *idealization*, valid over short distances away from walls, wakes, and machinery.

### 4.2 Physical interpretation
Bernoulli is conservation of mechanical energy per unit weight: **pressure head + velocity head + elevation head = constant.** Where the fluid speeds up, pressure drops (and vice versa).

### 4.3 Pressure terminology
- **Static pressure** P — the thermodynamic pressure.
- **Dynamic pressure** (1/2)*rho*V^2 — the pressure rise if the flow were brought to rest isentropically.
- **Stagnation (total) pressure** P_0 = P + (1/2)*rho*V^2 — measured by a pitot tube facing the flow.
- **Hydrostatic pressure** rho*g*z.

### 4.4 Classic applications
- **Pitot-static tube:** V = sqrt(2*(P_0 - P)/rho). Measures flow speed from the stagnation–static pressure difference.
- **Venturi / orifice / nozzle flow meters:** combine Bernoulli + continuity. Q_ideal = A_2 * sqrt( 2*(P_1 - P_2) / (rho*(1 - (A_2/A_1)^2)) ); multiply by a discharge coefficient C_d for the real meter.
- **Torricelli's theorem:** speed of efflux from a tank orifice at depth h is V = sqrt(2*g*h).
- **Siphons, free jets, draining tanks.**

### 4.5 HGL and EGL
- **Energy Grade Line (EGL):** plot of P/(rho*g) + V^2/(2g) + z. Drops in the direction of flow due to head loss; jumps up across a pump, down across a turbine.
- **Hydraulic Grade Line (HGL):** plot of P/(rho*g) + z (EGL minus the velocity head). The HGL sits a distance V^2/(2g) below the EGL. If the HGL drops below the pipe, the gauge pressure there is negative (suction — cavitation risk).

---

## 5. Differential Analysis — The Navier–Stokes Equations

### 5.1 Continuity (differential form)
From a mass balance on an infinitesimal element:
```
drho/dt + del . (rho*V) = 0
Incompressible:  del . V = 0   i.e.   du/dx + dv/dy + dw/dz = 0
```

### 5.2 The Navier–Stokes equations
Newton's second law applied to a fluid element. For an **incompressible, Newtonian fluid with constant viscosity**:
```
rho * DV/Dt = -del P + rho*g + mu * del^2 V
```
Term by term: (inertia) = (pressure gradient) + (gravity / body force) + (viscous diffusion).
Expanded (x-component):
```
rho*(du/dt + u*du/dx + v*du/dy + w*du/dz)
   = -dP/dx + rho*g_x + mu*(d2u/dx2 + d2u/dy2 + d2u/dz2)
```
Three momentum equations + continuity = four equations for four unknowns (u, v, w, P).

**Assumptions baked into this form:** Newtonian fluid, incompressible, constant mu. The compressible / variable-property version has extra terms.

### 5.3 Why Navier–Stokes is hard
- **Nonlinear** — the convective term (V.del)V makes superposition fail and admits turbulence and chaos.
- **Coupled** — pressure and the three velocity components are all entangled.
- Closed-form solutions exist only for a handful of simplified geometries.

### 5.4 Exact solutions (the canonical few)
- **Couette flow** — flow between two plates, one moving: linear velocity profile u(y) = U*y/h.
- **Plane / pipe Poiseuille flow** — pressure-driven flow in a channel/pipe: parabolic profile. For a circular pipe:
  ```
  u(r) = (DP/(4*mu*L)) * (R^2 - r^2)        u_max at the centerline
  V_avg = u_max / 2
  Q = pi*R^4*DP / (8*mu*L)                  (Hagen–Poiseuille law)
  ```
- **Fully developed flow in a duct, flow down an inclined plane, Stokes' first/second problem.**

### 5.5 The stream function and potential flow
- **Stream function psi** (2-D incompressible): u = dpsi/dy, v = -dpsi/dx. Automatically satisfies continuity; lines of constant psi are streamlines.
- **Velocity potential phi** (irrotational flow): V = del phi. Exists only when zeta = 0.
- **Potential flow** (incompressible + irrotational): del^2 phi = 0 (Laplace's equation — linear, superposable). Elementary solutions (uniform stream, source/sink, doublet, vortex) combine to model flow over bodies. Inviscid, so it predicts **zero drag** (d'Alembert's paradox) — the cue that viscosity, however small, cannot be ignored near walls.

### 5.6 The Euler equation
Navier–Stokes with mu = 0 (inviscid): rho*DV/Dt = -del P + rho*g. Integrating along a streamline recovers Bernoulli.

---

## 6. Dimensional Analysis and Similitude

### 6.1 Why
Reduces the number of variables in an experiment, enables scaling from a model to a prototype, and reveals the governing dimensionless groups.

### 6.2 The Buckingham Pi theorem
If a physical problem involves **n** variables expressible in **k** fundamental dimensions (M, L, T, Theta), it can be reduced to **n - k** independent dimensionless groups (Pi terms).
**Procedure:**
1. List all n variables and their dimensions.
2. Choose k **repeating variables** (must collectively span all k dimensions; do not include the variable you want to solve for; typically pick a length, a velocity, and a density).
3. Form each remaining variable into a Pi group by multiplying by the repeating variables raised to unknown powers; solve for the powers so the group is dimensionless.
4. Express the result as Pi_1 = f(Pi_2, Pi_3, ...).

### 6.3 The important dimensionless groups in fluid mechanics

| Group | Definition | Physical meaning (ratio of...) | Where it dominates |
|---|---|---|---|
| Reynolds number, Re | rho*V*L/mu = V*L/nu | inertia / viscous forces | all flows — sets laminar vs turbulent |
| Mach number, Ma | V/c | flow speed / sound speed; inertia / compressibility | compressible / high-speed flow |
| Froude number, Fr | V / sqrt(g*L) | inertia / gravity | free-surface flows, open channels, ship hulls |
| Euler number, Eu | DP / (rho*V^2) | pressure force / inertia | pressure-driven flows, cavitation |
| Weber number, We | rho*V^2*L/sigma | inertia / surface tension | droplets, sprays, thin films, bubbles |
| Strouhal number, St | f*L/V | unsteady / inertia | oscillating / vortex-shedding flows |
| Cavitation number, Ca | (P - P_v)/(0.5*rho*V^2) | pressure margin / dynamic pressure | pumps, propellers (cavitation onset) |
| Pressure / drag / lift coeff. | C_p, C_D, C_L | normalized force or pressure | external aerodynamics |
| Friction factor, f | (DP/L)*D / (0.5*rho*V^2) | wall shear / inertia | internal pipe flow |

### 6.4 Similitude — model testing
Three conditions for a model to predict the prototype:
1. **Geometric similarity** — model is a scaled replica (all length ratios equal).
2. **Kinematic similarity** — velocity fields are scaled copies (streamline patterns match).
3. **Dynamic similarity** — all relevant force ratios (dimensionless groups) are equal between model and prototype. Then the dependent Pi groups are also equal -> prediction.

**Pitfall — incompatible scaling:** matching Re *and* Fr simultaneously with the same fluid is usually impossible (Re wants high V or small nu; Fr wants V scaled with sqrt(L)). Engineers match the *dominant* group and correct for the rest, or use a different fluid.

---

## 7. Internal (Pipe) Flow

### 7.1 Laminar vs turbulent — the Reynolds number
For pipe flow (L = D, the diameter):
```
Re = rho*V_avg*D/mu = V_avg*D/nu
Re < ~2300        laminar
2300 < Re < 4000  transitional
Re > ~4000        turbulent
```
- **Laminar** — smooth, orderly layers; viscosity dominates; deterministic.
- **Turbulent** — chaotic, eddying, strong cross-stream mixing; flatter velocity profile; much higher wall shear and head loss.

### 7.2 Entrance region vs fully developed flow
Near the inlet the velocity profile is still developing (the boundary layers from the walls have not merged). **Hydrodynamic entry length:**
```
Laminar:    L_h / D ≈ 0.05 * Re
Turbulent:  L_h / D ≈ 10 to 60   (often taken ≈ 10)
```
Beyond L_h the profile no longer changes -> **fully developed flow**, where dP/dx is constant.

### 7.3 Head loss — the Darcy–Weisbach equation
```
h_L = f * (L/D) * V_avg^2 / (2g)
```
- **f** = the Darcy friction factor (dimensionless). (Beware: the *Fanning* friction factor f_F = f/4 — check which your source uses.)
- DP = f*(L/D)*(rho*V^2/2) for a horizontal pipe.

### 7.4 The friction factor

**Laminar flow** — exact result from integrating Navier–Stokes (Hagen–Poiseuille):
```
f = 64 / Re        (circular pipe; independent of roughness)
```

**Turbulent flow** — f depends on Re *and* relative roughness eps/D:
- **Colebrook equation** (implicit — the basis of the Moody chart):
  ```
  1/sqrt(f) = -2 * log10( (eps/D)/3.7 + 2.51/(Re*sqrt(f)) )
  ```
- **Haaland equation** (explicit approximation, within ~2% of Colebrook):
  ```
  1/sqrt(f) = -1.8 * log10( (eps/(3.7*D))^1.11 + 6.9/Re )
  ```
- **Fully rough regime** (high Re): f depends on eps/D only — the curves on the Moody chart go flat.
- **Smooth pipe** (eps -> 0): Blasius f = 0.316/Re^0.25 for Re < 1e5.

### 7.5 The Moody chart
A log-log plot of f versus Re, with a family of curves for different eps/D.
- Left region: a single straight line f = 64/Re (laminar — roughness irrelevant).
- Transition region (2300–4000): ill-defined, avoid designing here.
- Turbulent region: curves for each eps/D; they start sloping (smooth-pipe behavior) then flatten (fully rough).
**How to use it:** compute Re and eps/D, find the intersection, read f. (Or skip the chart and use Haaland.)

### 7.6 Minor losses
Losses from fittings, valves, bends, entrances, exits, and area changes:
```
h_L,minor = K_L * V^2 / (2g)
```
K_L is the loss coefficient (tabulated): sharp entrance ≈ 0.5, well-rounded entrance ≈ 0.04, pipe exit ≈ 1.0, fully open globe valve ≈ 10, 90° elbow ≈ 0.9, gate valve open ≈ 0.2. An equivalent length L_eq = K_L*D/f is sometimes used instead.

### 7.7 Total head loss and the system curve
```
h_L,total = sum( f*(L/D)*V^2/(2g) ) + sum( K_L*V^2/(2g) )
```
Plug into the CV energy equation (Section 3.4) to find pump head, flow rate, or pipe size. Pipes in series share the same Q (head losses add); pipes in parallel share the same h_L (flow rates add).

### 7.8 Worked-example patterns — pipe flow
- **Type 1 (find h_L or DP):** L, D, Q, fluid known -> compute V, Re, eps/D -> f -> h_L. Direct.
- **Type 2 (find Q):** h_L, L, D known, V unknown. f depends on Re which depends on V -> **iterate**: guess f (fully rough value), solve for V, recompute Re and f, repeat.
- **Type 3 (find D):** h_L, L, Q known. D appears everywhere -> iterate on D.

### 7.9 Noncircular ducts
Use the **hydraulic diameter** D_h = 4*A_c / P_wetted in Re and Darcy–Weisbach (A_c = cross-sectional area, P_wetted = wetted perimeter). Approximate for turbulent flow; laminar flow has shape-specific constants (e.g. f*Re = 56.9 for a square).

---

## 8. External Flow — Boundary Layers, Drag, and Lift

### 8.1 The boundary-layer concept (Prandtl)
At high Re, viscous effects are confined to a **thin boundary layer** adjacent to the surface (and the wake). Outside it, the flow behaves as inviscid (potential flow). This resolves d'Alembert's paradox: drag comes from the boundary layer and the wake, not from the inviscid outer flow.

### 8.2 Boundary-layer thickness and transition (flat plate)
- **Boundary-layer thickness delta(x)** — where u reaches 0.99*U_infinity.
- Reynolds number based on distance from the leading edge: Re_x = U*x/nu.
- **Transition** from laminar to turbulent BL near Re_x ≈ 5e5 (for a flat plate).
- **Laminar BL (Blasius solution):**
  ```
  delta/x = 5.0 / sqrt(Re_x)
  Local skin friction:  C_f,x = 0.664 / sqrt(Re_x)
  Average over length L: C_f = 1.328 / sqrt(Re_L)
  ```
- **Turbulent BL (1/7-power-law approximation):**
  ```
  delta/x = 0.16 / Re_x^(1/7)
  C_f,x = 0.027 / Re_x^(1/7)
  Average: C_f = 0.074 / Re_L^(1/5)   (5e5 < Re_L < 1e7)
  ```
A turbulent BL is thicker, has higher wall shear, but **resists separation better** (more momentum near the wall).

### 8.3 Flow separation
When the boundary layer meets an **adverse pressure gradient** (pressure rising in the flow direction, dP/dx > 0), near-wall fluid is decelerated, reverses, and the BL detaches -> **separation**. Separation creates a wide low-pressure wake and large **pressure (form) drag**. Streamlining delays separation; tripping the BL to turbulent (golf-ball dimples) also delays it.

### 8.4 Drag
Total drag = **friction (skin) drag** (integral of wall shear) + **pressure (form) drag** (integral of pressure over the frontal area).
```
F_D = C_D * (1/2) * rho * V^2 * A
```
- A is the **frontal area** for bluff bodies, the **planform area** for lifting surfaces — check the convention.
- Streamlined body (airfoil): friction drag dominates. Bluff body (cylinder, sphere, flat plate normal to flow): pressure drag dominates.
- **Sphere drag crisis:** C_D drops sharply near Re ≈ 3e5 when the BL goes turbulent and separation moves rearward.
- For a sphere at very low Re (Re < 1, creeping/Stokes flow): F_D = 3*pi*mu*D*V (Stokes' law), giving C_D = 24/Re.

### 8.5 Lift
```
F_L = C_L * (1/2) * rho * V^2 * A      (A = planform area)
```
- Lift is generated by circulation / the pressure difference between the suction (upper) and pressure (lower) surfaces.
- C_L rises ~linearly with angle of attack until **stall** — the angle where the boundary layer separates from the upper surface, C_L collapses, C_D spikes.
- **Induced drag** — a finite wing sheds tip vortices; the associated drag scales with C_L^2 / (aspect ratio).

### 8.6 Worked-example pattern — external flow
1. Identify the body and the relevant area (frontal vs planform).
2. Compute Re (based on chord, diameter, or plate length as appropriate).
3. Determine the flow regime (laminar/turbulent BL, separated or attached).
4. Get C_D and/or C_L from a chart/correlation for that geometry and Re.
5. Compute F_D, F_L; for vehicles, power to overcome drag = F_D * V.

---

## 9. Master List of Common Student Pitfalls

1. **Bernoulli misuse** — applying it across a pump, a turbine, a region with significant friction, or a wake. If any of the five assumptions fails, use the full energy equation with h_L.
2. **Gauge vs absolute pressure** — use gauge pressure on a control surface in momentum problems (atmospheric cancels); use absolute pressure in gas-law / cavitation calculations.
3. **Momentum is a vector** — always write separate component equations; sign of velocity matters.
4. **Relative vs absolute velocity** — for a moving CV, use velocities relative to the CV in continuity and momentum.
5. **Reynolds number length scale** — D for pipe flow, x or L for a flat plate, chord for an airfoil, D for a sphere. The transition value depends on the geometry; 2300 is pipes only.
6. **Darcy vs Fanning friction factor** — they differ by a factor of 4. f_Darcy = 64/Re laminar; f_Fanning = 16/Re.
7. **Center of pressure is not the centroid** — it lies below the centroid for a submerged plate.
8. **Forgetting minor losses** — in short pipe systems with many fittings, minor losses can exceed major losses.
9. **Iteration required** — Type-2 and Type-3 pipe problems and any problem where f depends on the unknown velocity need iteration; you cannot solve them in one pass.
10. **delta is not a streamline** — the boundary-layer edge is a conceptual locus, not a physical surface; fluid crosses it.
11. **Inviscid theory predicts zero drag** — never trust potential flow for drag; it has no boundary layer.
12. **Kinetic-energy correction factor alpha** — do not silently set alpha = 1 for laminar pipe flow (alpha = 2).
13. **Frontal vs planform area** — using the wrong area in the drag/lift equation is a factor-of-several error.
14. **Compressibility threshold** — Ma > 0.3 means density changes matter; incompressible relations no longer apply.
15. **Mixing up streamline / pathline / streakline** in unsteady flow — they only coincide when the flow is steady.
16. **No-slip is at the wall** — velocity is zero *at* the wall, maximum away from it; the gradient there sets the wall shear.

---

## Open-source sources used

- **Bar-Meir, Genick.** *Basics of Fluid Mechanics* (open textbook). Engineering LibreTexts. https://eng.libretexts.org/Bookshelves/Civil_Engineering/Fluid_Mechanics_(Bar-Meir) and Open Textbook Library https://open.umn.edu/opentextbooks/textbooks/85 — used for fluid statics, control-volume conservation laws, dimensional analysis, and the differential equations of motion.
- **OpenStax University Physics, Vol. 1, Ch. 14 — Fluid Mechanics.** Physics LibreTexts. https://phys.libretexts.org/Bookshelves/University_Physics/University_Physics_(OpenStax)/Book%3A_University_Physics_I_-_Mechanics_Sound_Oscillations_and_Waves_(OpenStax)/14%3A_Fluid_Mechanics — used for hydrostatics, buoyancy, continuity, and the Bernoulli equation fundamentals.
- **Intermediate Fluid Mechanics** (open textbook), Oregon State University. https://open.oregonstate.education/intermediate-fluid-mechanics/ and Open Textbook Library https://open.umn.edu/opentextbooks/textbooks/1077 — used for the Reynolds Transport Theorem, the Navier–Stokes equations, exact solutions, potential flow, and boundary-layer theory.
- **MIT OpenCourseWare**, 2.006 / 2.25 Fluid Mechanics course materials — cross-reference for boundary-layer scaling, drag/lift coefficients, and internal-flow (Moody chart) treatment.
- **Wikipedia** (cross-reference only, for the Colebrook and Haaland friction-factor forms and standard dimensionless-group definitions): "Darcy friction factor formulae," "Moody chart," "Reynolds number."
