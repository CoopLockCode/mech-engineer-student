# Dynamics Reference

A graduate-level study companion for **Dynamics**. Covers kinematics and kinetics of particles and rigid bodies, Newton-Euler equations, work-energy methods, impulse-momentum methods, rotational dynamics, relative motion, and an introduction to vibrations.

Dynamics studies bodies **in motion** and the forces causing that motion. It splits into two halves:
- **Kinematics** — the geometry of motion: position, velocity, acceleration. No forces involved.
- **Kinetics** — relates the forces/moments to the motion they produce, via Newton's second law (and its integrated forms: work-energy and impulse-momentum).

There are **three master methods** of kinetics, and choosing the right one is half the skill:
1. **Newton-Euler (F = ma):** instantaneous — relates forces to acceleration at an instant.
2. **Work-Energy:** integrates F·ds — relates force, displacement, and speed; eliminates time and acceleration.
3. **Impulse-Momentum:** integrates F·dt — relates force, time, and velocity; ideal for impacts and short-duration forces.

---

## 1. Particle Kinematics

### 1.1 Rectilinear (Straight-Line) Motion

Position s(t); velocity and acceleration are derivatives:

- **Velocity:** v = ds/dt
- **Acceleration:** a = dv/dt = d²s/dt²
- **Eliminating time** (chain rule, extremely useful): **a ds = v dv**

**Constant-acceleration equations** (a = constant only):
- v = v₀ + a·t
- s = s₀ + v₀·t + ½·a·t²
- v² = v₀² + 2·a·(s − s₀)

**Variable acceleration** — integrate from the relationship that's given:
- a = f(t): integrate a dt to get v, then v dt to get s.
- a = f(v): use a = dv/dt → dt = dv/a, or a = v dv/ds.
- a = f(s): use a ds = v dv → ∫a ds = ∫v dv.

**Erratic motion (graphical):** slope and area relationships —
- Slope of s–t = v; slope of v–t = a.
- Area under a–t = Δv; area under v–t = Δs.

### 1.2 Curvilinear Motion — Rectangular (Cartesian) Coordinates

Position **r** = x**i** + y**j** + z**k**
- **v** = ẋ**i** + ẏ**j** + ż**k**; speed = |v|
- **a** = ẍ**i** + ÿ**j** + z̈**k**

Each component is an independent rectilinear-motion problem. Best for **projectile motion**:
- Horizontal: a_x = 0 → x = x₀ + (v₀ cos θ)t
- Vertical: a_y = −g → v_y = v₀ sin θ − g·t, y = y₀ + (v₀ sin θ)t − ½g·t²

### 1.3 Curvilinear Motion — Normal & Tangential (n–t) Coordinates

Used when the **path** is known. Axes move with the particle: **t** tangent to the path (direction of motion), **n** points toward the center of curvature.

- **Velocity:** **v** = v·**u_t** (always tangent), v = ds/dt
- **Acceleration:** **a** = a_t·**u_t** + a_n·**u_n**
  - **Tangential:** a_t = dv/dt = v·dv/ds — changes the *speed*.
  - **Normal (centripetal):** a_n = v²/ρ — changes the *direction*; always points toward the center of curvature. ρ = radius of curvature.
- **Magnitude:** a = √(a_t² + a_n²)
- For a path y = f(x): ρ = [1 + (dy/dx)²]^(3/2) / |d²y/dx²|

**Key insight:** constant speed does NOT mean zero acceleration — a_n still exists if the path is curved.

### 1.4 Curvilinear Motion — Polar (Cylindrical) Coordinates

Used for motion described by a radius r and angle θ (radial arms, central-force problems).

- **Position:** **r** = r·**u_r**
- **Velocity:** **v** = ṙ·**u_r** + r·θ̇·**u_θ**
  - radial component v_r = ṙ; transverse component v_θ = r·θ̇
- **Acceleration:** **a** = (r̈ − r·θ̇²)·**u_r** + (r·θ̈ + 2·ṙ·θ̇)·**u_θ**
  - radial a_r = r̈ − r·θ̇²; transverse a_θ = r·θ̈ + 2·ṙ·θ̇
  - The **2ṙθ̇** term is the **Coriolis acceleration**; **−rθ̇²** is the centripetal term.
- For 3D cylindrical: add a_z = z̈.

### 1.5 Dependent Motion (Constrained / Pulley Systems)

When two particles are connected by an inextensible cable over pulleys, their motions are related by the constant total cable length.

**Procedure:**
1. Define position coordinates for each body from a *fixed* datum, measured along the direction of motion.
2. Write the length constraint: Σ(segment lengths) = total cable length L = constant.
3. Differentiate once → velocity relation; twice → acceleration relation.
4. Watch signs — coordinates increasing in opposite directions give opposite-sign velocities.

### 1.6 Relative Motion of Two Particles (Translating Axes)

For two particles A and B observed from a non-rotating (translating) frame:

- **r_B = r_A + r_B/A**
- **v_B = v_A + v_B/A**
- **a_B = a_A + a_B/A**

where r_B/A is the position of B *relative to* A. Solve as vector equations (components or vector triangle). Used heavily for two vehicles, two aircraft, etc.

---

## 2. Particle Kinetics — Newton's Second Law (Force & Acceleration)

### 2.1 Newton's Second Law

**ΣF = m·a**

The resultant external force on a particle equals its mass times its acceleration; **a** is measured relative to an **inertial (non-accelerating) reference frame**.

### 2.2 Equations of Motion in Each Coordinate System

| System | Equations |
|---|---|
| Rectangular | ΣF_x = m·a_x, ΣF_y = m·a_y, ΣF_z = m·a_z |
| Normal–Tangential | ΣF_t = m·a_t = m·(dv/dt), ΣF_n = m·a_n = m·(v²/ρ), ΣF_b = 0 |
| Polar/Cylindrical | ΣF_r = m·(r̈ − rθ̇²), ΣF_θ = m·(rθ̈ + 2ṙθ̇), ΣF_z = m·z̈ |

### 2.3 Procedure (Equations of Motion for a Particle)

1. Choose the coordinate system that fits the problem (rectangular for projectile-like, n–t for known paths, polar for arms/central force).
2. Draw the **free-body diagram (FBD)** — all real external forces (weight, normal, friction, tension, applied, spring).
3. Draw the **kinetic diagram** — the m·a vector(s). (FBD = kinetic diagram is the statement of Newton's law.)
4. Write ΣF = m·a component by component.
5. If needed, add **kinematic equations** (e.g., a_n = v²/ρ, constraint relations) — these supply extra equations.
6. Solve. The number of equations must match the unknowns.

### 2.4 Key Force Models

- **Weight:** W = m·g, downward.
- **Friction:** kinetic F = μ_k·N, opposing motion; static F ≤ μ_s·N.
- **Spring:** F_s = k·s (s = stretch/compression from natural length).
- **Normal force N:** perpendicular to the contact surface; an unknown to be solved for, not always equal to weight.

### 2.5 Common Pitfalls

- Using a non-inertial frame without correction.
- Assuming N = W on an incline or in vertical circular motion — N must be solved from ΣF.
- Forgetting a_n = v²/ρ exists even at constant speed.
- Sign errors: define a positive direction and keep a, F, and v consistent with it.
- Mixing kinetics coordinate systems mid-problem without re-deriving.

---

## 3. Particle Kinetics — Work and Energy

### 3.1 Work of a Force

**U = ∫ F·dr = ∫ F cos θ ds**

Work is a scalar; θ is the angle between the force and the displacement.

- **Work of a constant force** over displacement Δr: U = F·Δr = F cos θ · |Δr|
- **Work of weight:** U = −W·Δy (positive if the body descends; depends only on vertical drop, not path).
- **Work of a spring:** U = −(½k·s₂² − ½k·s₁²) — negative when the spring is being stretched/compressed by the body.
- A force **perpendicular to motion does zero work** (normal force, centripetal force).
- **Friction (kinetic)** does negative work: U_f = −F·d = −μ_k·N·d.

### 3.2 Principle of Work and Energy

**T₁ + ΣU₁→₂ = T₂**

where **kinetic energy T = ½·m·v²** (always positive scalar). The total work done by all forces equals the change in kinetic energy.

**Why use it:** eliminates acceleration and time; directly relates **force, displacement, and speed**. Ideal when you want a speed at a position, or a distance to stop.

### 3.3 Conservative Forces and Potential Energy

A force is **conservative** if its work is path-independent (gravity, springs). For conservative forces, work = decrease in potential energy: U_cons = −ΔV.

- **Gravitational PE:** V_g = W·y = m·g·y (y measured up from a datum).
- **Elastic PE:** V_e = ½·k·s².

### 3.4 Conservation of Energy

When **only conservative forces** do work:

**T₁ + V₁ = T₂ + V₂**

If non-conservative forces (friction, applied forces) also act:

**T₁ + V₁ + ΣU₁→₂(non-cons) = T₂ + V₂**

### 3.5 Power and Efficiency

- **Power:** P = dU/dt = **F·v** (instantaneous). Units: watt (W = J/s), or horsepower (1 hp = 746 W).
- **Mechanical efficiency:** ε = P_out / P_in = U_out / U_in < 1 (always, due to friction losses).

### 3.6 Procedure (Work-Energy for a Particle)

1. Identify the two states (1 and 2) — positions and speeds.
2. Draw the FBD to identify all forces that do work over the path.
3. Compute T₁ = ½mv₁² and T₂ = ½mv₂².
4. Compute ΣU₁→₂ for each force (or use V if conservative).
5. Apply T₁ + ΣU₁→₂ = T₂ (or T₁ + V₁ + U_noncons = T₂ + V₂).
6. Solve for the unknown (usually v₂ or a distance).

### 3.7 Pitfalls

- Including the normal force's "work" — it's zero (⊥ to motion).
- Sign of weight's work: negative going up, positive going down.
- Double-counting: if you use gravitational PE (V_g), do NOT also include weight in ΣU.
- Spring work sign: stretching the spring takes energy *from* the body (negative U on the body).
- Work-energy gives speed (scalar) — it cannot give direction or individual force components at an instant; use F=ma for that.

---

## 4. Particle Kinetics — Impulse and Momentum

### 4.1 Linear Impulse and Linear Momentum

- **Linear momentum:** **L** = m·**v** (vector).
- **Linear impulse** of a force: **I** = ∫F dt (vector); for a constant force, **I** = F·Δt.

**Principle of Linear Impulse and Momentum:**

**m·v₁ + Σ∫F dt = m·v₂**

Written component-wise. **Why use it:** relates **force, time, and velocity**; eliminates the need to know acceleration as a function of position. Ideal for forces acting over a known time interval, and for sudden/impulsive forces.

### 4.2 Conservation of Linear Momentum

If the resultant external impulse in a direction is zero (ΣF = 0 in that direction, or the impulse is negligible compared to internal impulses):

**Σm·v₁ = Σm·v₂**  (in that direction)

For a system of particles, internal forces cancel (Newton's 3rd law), so momentum is conserved when no *external* impulse acts.

### 4.3 Impact

**Impact** = collision; very large forces over a very short time. Two phases: deformation, then restitution.

- **Line of impact:** the normal to the contact surfaces, through the mass centers.
- **Central impact:** velocities of both bodies are along the line of impact.
- **Oblique impact:** velocities are at angles to the line of impact.

**Two governing equations for central impact:**

1. **Conservation of momentum** along the line of impact: m_A v_A1 + m_B v_B1 = m_A v_A2 + m_B v_B2
2. **Coefficient of restitution:** **e = (v_B2 − v_A2) / (v_A1 − v_B1)** = (relative velocity of separation) / (relative velocity of approach), along the line of impact.

- **e = 1:** perfectly elastic (kinetic energy conserved).
- **e = 0:** perfectly plastic (bodies move together after; max KE lost).
- 0 < e < 1: real-world inelastic impact; some KE is lost.

**Oblique impact:** along the line of impact, use the two equations above. Perpendicular to the line of impact, each body's momentum component is **unchanged** (no impulsive force in that direction, assuming smooth surfaces) — gives two more equations. Total 4 equations, 4 unknown velocity components.

### 4.4 Angular Momentum and Angular Impulse (Particle)

- **Angular momentum about point O:** **H_O = r × m·v** (moment of linear momentum). Magnitude in 2D: H_O = m·v·d (d = ⊥ distance from O to the velocity line).
- **Principle:** Σ**M_O** = d**H_O**/dt, integrated: **H_O1 + Σ∫M_O dt = H_O2**.
- **Conservation of angular momentum:** if ΣM_O = 0, then H_O1 = H_O2. Key for central-force motion (orbits) and a particle on a string being reeled in (r decreases → v increases).

### 4.5 Steady Mass Flow (Fluid Streams)

For a steady stream deflected by a vane/pipe, the resultant force on the device:

ΣF = ṁ·(v_out − v_in), where ṁ = dm/dt = ρ·Q = ρ·A·v (mass flow rate).

### 4.6 Procedure (Impulse-Momentum)

1. Identify states 1 and 2 and the time interval.
2. Draw the FBD / impulse diagram for the interval — note impulsive vs. non-impulsive forces (during impact, gravity and normal forces are often negligible compared to the impact impulse).
3. Decide: is momentum conserved (no external impulse in some direction)? If so, use conservation; if not, use the full impulse-momentum equation.
4. For impact, add the restitution equation.
5. Write component equations; solve for the unknown velocities.

### 4.7 Pitfalls

- Treating momentum as a scalar — it's a vector; apply per direction.
- Forgetting that KE is NOT conserved in impact unless e = 1.
- Using restitution equation across the wrong axis in oblique impact (it applies only along the line of impact).
- Sign errors — assign a positive direction and keep all velocities consistent.

---

## 5. Method Selection Guide (Particle Kinetics)

| If you want... | And you know... | Use |
|---|---|---|
| Acceleration / force at an instant | Forces at an instant | **F = ma** |
| Speed at a position, or stopping distance | Forces over a displacement | **Work-Energy** |
| Velocity after a time interval | Forces over time | **Impulse-Momentum** |
| Velocities after a collision | Masses, e, pre-impact velocities | **Impulse-Momentum + restitution** |
| Speed in a frictionless / conservative system | Geometry only | **Conservation of Energy** |
| Velocity change with no external impulse | System of interacting bodies | **Conservation of Linear Momentum** |
| Velocity of a particle on a string being reeled in | No moment about a center | **Conservation of Angular Momentum** |

---

## 6. Rigid Body Kinematics (Planar)

A rigid body's motion combines translation of a reference point with rotation of the body.

### 6.1 Types of Planar Rigid-Body Motion

- **Translation** (rectilinear or curvilinear): every point has the same velocity and acceleration; no rotation.
- **Rotation about a fixed axis:** every point moves in a circle about the axis.
- **General plane motion:** translation + rotation combined (e.g., a rolling wheel).

### 6.2 Rotation About a Fixed Axis

Angular kinematics (analogous to rectilinear):
- ω = dθ/dt, α = dω/dt = d²θ/dt², and **α dθ = ω dω**
- Constant α: ω = ω₀ + α·t; θ = θ₀ + ω₀t + ½α·t²; ω² = ω₀² + 2α(θ − θ₀)

For a point at distance r from the axis:
- **Velocity:** v = ω·r (tangent to the circular path); **v** = **ω** × **r**
- **Acceleration:** a_t = α·r (tangential), a_n = ω²·r = v²/r (toward the axis). **a** = **α** × **r** − ω²**r** (planar).

### 6.3 Absolute General Plane Motion (Constraint Method)

Relate the body's motion to coordinates using geometry, then differentiate. Define position variables, write the geometric constraint equations, differentiate once for velocity and twice for acceleration. Useful for linkages, sliding rods, ladders.

### 6.4 Relative Motion Analysis — Velocity

For two points A and B on the **same rigid body** (B is the point you want, A is the reference):

**v_B = v_A + v_B/A = v_A + ω × r_B/A**

- v_A = velocity of the reference point.
- ω × r_B/A = velocity of B relative to A; this term has magnitude ω·r_B/A and is **perpendicular to r_B/A** (rotation only — the body is rigid so B can only circle A).
- ω is the angular velocity of the body (the same for every point on the body).

Solve as a vector equation: pick components, or draw the vector triangle.

### 6.5 Instantaneous Center of Zero Velocity (IC)

At any instant, there is a point (the **IC**) about which the entire body appears to be in pure rotation — the point with zero velocity at that instant.

- Once the IC is located, **v = ω·r** for any point, where r is the distance from that point to the IC, and v is **perpendicular to the line from the point to the IC**.

**Locating the IC:**
- If the velocity directions of two points are known, the IC is at the intersection of the two lines drawn **perpendicular** to those velocities.
- If two points have parallel velocities and their magnitudes are known, use similar triangles (the IC lies on the line through both points).
- For a wheel rolling without slipping, the IC is the **contact point** with the ground.

**Caution:** the IC has zero *velocity* but generally NOT zero *acceleration* — never use it for acceleration analysis.

### 6.6 Relative Motion Analysis — Acceleration

For two points A and B on the same rigid body:

**a_B = a_A + α × r_B/A − ω²·r_B/A**

- a_A = acceleration of the reference point.
- **α × r_B/A** = tangential component of B relative to A; magnitude α·r_B/A, perpendicular to r_B/A.
- **−ω²·r_B/A** = normal component; magnitude ω²·r_B/A, directed from B toward A.

Solve as a vector equation (typically 2 scalar equations in 2D → 2 unknowns).

### 6.7 Rolling Without Slipping

A wheel of radius r rolling without slipping on a fixed surface:
- The contact point is the **instantaneous center** (v_contact = 0).
- **Center velocity:** v_G = ω·r
- **Center acceleration:** a_G = α·r (only the tangential part; the center moves in a straight line so it has no a_n)
- The contact point has zero velocity but a **nonzero acceleration** = ω²·r, directed toward the wheel center.

**Rolling vs. slipping check:** rolling without slipping requires the friction force F ≤ μ_s·N. If the required F exceeds this, the wheel slips, the v_G = ωr constraint breaks, and you must use F = μ_k·N with a_G and α independent.

### 6.8 Relative Motion Using Rotating Reference Frames

When a particle moves *along* a path that is itself on a rotating body (e.g., a collar sliding on a rotating arm), use a rotating frame:

- **v_B = v_A + Ω × r_B/A + v_rel**
- **a_B = a_A + Ω̇ × r_B/A + Ω × (Ω × r_B/A) + 2·Ω × v_rel + a_rel**

where Ω = angular velocity of the rotating frame, v_rel and a_rel are measured *relative to the rotating frame*, and **2·Ω × v_rel** is the **Coriolis acceleration**. Essential for slotted-arm and mechanism problems where one part slides relative to another.

### 6.9 Procedure (Rigid-Body Velocity/Acceleration)

1. Identify the type of motion and the body's angular velocity/acceleration (ω, α).
2. Choose a reference point A whose motion is known (often a pin or a center).
3. Write the relative-motion vector equation (velocity, then acceleration).
4. Express each term in components; the relative terms are ⊥ (tangential) and along (normal) r_B/A.
5. Solve the scalar equations. For systems, link multiple bodies through shared points (pins) — the velocity/acceleration of a pin is the same for both connected bodies.
6. The IC method is a fast shortcut for velocities only.

### 6.10 Pitfalls

- Forgetting that ω and α are the **same for every point** on a rigid body.
- Using the IC for acceleration — invalid.
- Dropping the **−ω²r** normal term in acceleration analysis.
- Omitting the **Coriolis term** when there is sliding relative to a rotating frame.
- Sign of ω/α (counterclockwise positive) inconsistent with the cross-product setup.

---

## 7. Rigid Body Kinetics — Newton-Euler Equations (Force & Acceleration)

### 7.1 Mass Moment of Inertia

The rotational analog of mass — resistance to angular acceleration:

**I = ∫ r² dm**

where r = perpendicular distance from the mass element to the rotation axis. Units: kg·m² or slug·ft².

**Parallel-axis theorem:** **I = I_G + m·d²**, where I_G is about the centroidal axis and d is the distance to the parallel axis.

**Radius of gyration:** k = √(I/m), so I = m·k².

### 7.2 Mass Moment of Inertia Table (about the centroidal axis through G, ⊥ to the plane unless noted)

| Body | I_G |
|---|---|
| Thin rod, length L, about center (⊥ to rod) | (1/12)·m·L² |
| Thin rod, length L, about one end | (1/3)·m·L² |
| Thin rectangular plate (a × b), about axis ⊥ to plate through center | (1/12)·m·(a² + b²) |
| Solid disk / cylinder, radius r, about its axis | (1/2)·m·r² |
| Solid cylinder, length L, about a transverse centroidal axis | (1/12)·m·(3r² + L²) |
| Thin ring / hoop / thin-walled cylinder, radius r, about its axis | m·r² |
| Hollow cylinder (R outer, r inner), about its axis | (1/2)·m·(R² + r²) |
| Solid sphere, radius r, about a diameter | (2/5)·m·r² |
| Thin spherical shell, radius r, about a diameter | (2/3)·m·r² |
| Solid cone, radius r, about its axis | (3/10)·m·r² |
| Slender rod / general body | use I = m·k² with given radius of gyration k |

### 7.3 The Equations of Motion (Planar)

For a rigid body in general plane motion, with mass center G:

- **Translation:** ΣF_x = m·(a_G)_x and ΣF_y = m·(a_G)_y
- **Rotation:** **ΣM_G = I_G·α**  (moments about the mass center)

These three scalar equations are the **Newton-Euler equations** for planar motion.

**Alternative moment equation** — about an arbitrary point P:
ΣM_P = I_G·α + (moment of m·a_G about P) = Σ(M_k)_P
The right side is the sum of the moments of the **kinetic** vectors (m·a_G components and I_G·α) about P. Choosing P wisely (where unknown forces intersect) decouples the equations.

### 7.4 Special Cases

- **Pure translation** (α = 0): ΣF = m·a_G, ΣM_G = 0. The body's "inertia couple" vanishes; ΣM about any point = moment of m·a_G about that point.
- **Rotation about a fixed axis through O:** ΣM_O = I_O·α (where I_O = I_G + m·d², by parallel-axis theorem). Also ΣF_n = m·ω²·r_G and ΣF_t = m·α·r_G for the pin reactions.
- **General plane motion:** all three equations are active. Often paired with a kinematic constraint (e.g., a_G = α·r for rolling without slipping).

### 7.5 Procedure (Rigid-Body Equations of Motion)

1. Establish an inertial coordinate system; identify the body's I_G (use the table + parallel-axis theorem as needed).
2. Draw the **free-body diagram** — all external forces and couples.
3. Draw the **kinetic diagram** — the m·a_G vector(s) at G and the I_G·α couple.
4. Write ΣF_x = m(a_G)_x, ΣF_y = m(a_G)_y, ΣM_G = I_G·α. (Or use ΣM_P with the kinetic-moment sum.)
5. Add **kinematic constraint equations** if needed (rolling: a_G = αr; linkage constraints; a_n = ω²r).
6. Solve the simultaneous equations. Check the friction assumption for rolling problems (F ≤ μ_s·N).

### 7.6 Pitfalls

- Using ΣM_G = I_G·α with I about the wrong axis — for moments about G, use I_G; about a fixed pin O, use I_O.
- Forgetting the I_G·α term on the kinetic diagram when summing moments about a point other than G.
- Assuming rolling without slipping without checking F ≤ μ_s·N.
- For a body rotating about a fixed axis not through G, forgetting the pin reaction has both normal (m·ω²·r_G) and tangential (m·α·r_G) parts.
- Treating the kinetic diagram terms as "real forces" — they are not; they are the m·a effect.

---

## 8. Rigid Body Kinetics — Work and Energy

### 8.1 Kinetic Energy of a Rigid Body

- **Translation:** T = ½·m·v_G²
- **Rotation about a fixed axis O:** T = ½·I_O·ω²
- **General plane motion:** **T = ½·m·v_G² + ½·I_G·ω²** (translational KE of the mass center + rotational KE about G)
  - Equivalently, T = ½·I_IC·ω² using the instantaneous center.

### 8.2 Work of Forces and Couples on a Rigid Body

- **Work of a force:** U = ∫F·dr (same as for a particle — use the displacement of the force's point of application).
- **Work of a couple moment M:** **U = ∫M dθ** = M·Δθ for a constant couple (Δθ in radians).
- **Work of weight:** U = −W·Δy_G (vertical drop of the mass center).
- **Work of a spring:** U = −(½k·s₂² − ½k·s₁²).
- **A force at the instantaneous center / contact point of a rolling body does zero work** — because that point has zero velocity, hence zero displacement at that instant. This is why friction does no work on a body rolling without slipping.

### 8.3 Principle of Work and Energy (Rigid Body)

**T₁ + ΣU₁→₂ = T₂**

Sum the work of all external forces and couples. For a system of connected bodies, internal forces at frictionless pins do no net work (equal-and-opposite forces, same displacement), so apply the principle to the whole system.

### 8.4 Conservation of Energy (Rigid Body)

When only conservative forces do work:

**T₁ + V₁ = T₂ + V₂**

with V = V_g + V_e = m·g·y_G + ½·k·s². Add ΣU_noncons if friction or applied forces do work.

### 8.5 Procedure (Work-Energy for a Rigid Body)

1. Identify states 1 and 2.
2. Compute T₁ and T₂ using ½mv_G² + ½I_Gω² (relate v_G and ω through kinematics — e.g., v_G = ωr for rolling).
3. Compute the work of every force and couple, or use potential energy for conservative ones.
4. Apply T₁ + ΣU₁→₂ = T₂ (or the conservation form).
5. Solve — typically for ω₂ or v_G2 at a position.

### 8.6 Pitfalls

- Forgetting the rotational term ½I_Gω² — a rolling body has both.
- Not relating v_G and ω with the correct kinematic constraint.
- Counting friction's work on a rolling-without-slipping body (it's zero).
- Including weight in both ΣU and V — pick one.
- Using I about the wrong axis in ½Iω².

---

## 9. Rigid Body Kinetics — Impulse and Momentum

### 9.1 Linear and Angular Momentum of a Rigid Body

- **Linear momentum:** **L** = m·**v_G** (acts through the mass center).
- **Angular momentum about the mass center G:** **H_G** = I_G·ω.
- **Angular momentum about a fixed point O:** H_O = I_G·ω + (m·v_G)·d = I_O·ω if O is the fixed rotation axis. In general H_O = I_G·ω + moment of L about O.

### 9.2 Principle of Linear Impulse and Momentum

**m·(v_G)₁ + Σ∫F dt = m·(v_G)₂**  (component-wise)

### 9.3 Principle of Angular Impulse and Momentum

About the mass center G:
**I_G·ω₁ + Σ∫M_G dt = I_G·ω₂**

About a fixed point O (fixed-axis rotation):
**I_O·ω₁ + Σ∫M_O dt = I_O·ω₂**

### 9.4 Conservation Laws

- **Conservation of linear momentum:** if Σ∫F dt = 0 in a direction → m(v_G)₁ = m(v_G)₂ in that direction.
- **Conservation of angular momentum:** if Σ∫M dt = 0 about a point → angular momentum about that point is conserved. Common for a body struck off-center, or a system with only internal impulses.

### 9.5 Eccentric Impact

Impact where the line of impact does **not** pass through the mass centers of the colliding bodies. Combine:
1. Conservation of angular momentum of the system (or of each body about the right point) — internal impact impulses cancel.
2. Coefficient of restitution applied to the **velocity components of the contact points along the line of impact**:
   **e = [(v_B)_n2 − (v_A)_n2] / [(v_A)_n1 − (v_B)_n1]**, where these are the velocities of the *contact points*, not the mass centers.
3. Kinematic relations linking each contact point's velocity to its body's v_G and ω.

### 9.6 Procedure (Impulse-Momentum for a Rigid Body)

1. Identify states 1 and 2 and the time interval; note impulsive vs. non-impulsive forces.
2. Draw the impulse-momentum diagram: initial momenta (m·v_G, I_G·ω), the impulses, and final momenta.
3. Decide whether linear and/or angular momentum is conserved.
4. Write the linear and angular impulse-momentum equations (and restitution for impact).
5. Add kinematic relations as needed; solve.

### 9.7 Pitfalls

- Using I_G·ω when the body rotates about a fixed pin — choose the moment point consistently (use I_O about O, or carry the moment of L about O).
- Forgetting that an off-center impulse changes **both** v_G and ω.
- In eccentric impact, applying restitution to mass-center velocities instead of contact-point velocities.
- Treating angular momentum as conserved when an external impulsive moment acts.

---

## 10. Method Selection Guide (Rigid-Body Kinetics)

| If you want... | Use |
|---|---|
| Angular/linear acceleration or a force/reaction at an instant | **Newton-Euler (ΣF = ma_G, ΣM_G = I_Gα)** |
| Angular velocity or speed at a position; distance/angle to stop | **Work-Energy** |
| Final velocities after a time interval or an impact | **Impulse-Momentum** |
| Result of an eccentric collision | **Angular-momentum conservation + restitution** |
| Speed in a frictionless / rolling-without-slip conservative system | **Conservation of Energy** |

---

## 11. Introduction to Vibrations (One Degree of Freedom)

### 11.1 Undamped Free Vibration

A mass-spring system with no damping and no forcing. From ΣF = ma:

**m·ẍ + k·x = 0**  →  **ẍ + ω_n²·x = 0**

- **Natural circular frequency:** ω_n = √(k/m) (rad/s)
- **Natural period:** τ = 2π/ω_n = 2π·√(m/k)
- **Natural frequency:** f = 1/τ = ω_n/(2π) (Hz)
- **General solution:** x(t) = C·sin(ω_n·t + φ), where C = amplitude and φ = phase angle, both set by initial conditions x₀ and ẋ₀:
  - C = √(x₀² + (ẋ₀/ω_n)²),  tan φ = (x₀·ω_n)/ẋ₀

**Energy method** (alternative derivation): for a conservative 1-DOF system, d/dt(T + V) = 0 yields the equation of motion directly — often the fastest route for systems with rotation (use it to find ω_n without drawing FBDs).

For a **simple pendulum** (length L, small angle): ω_n = √(g/L). For a **compound (physical) pendulum**: ω_n = √(m·g·d / I_O), d = distance from pivot O to G.

### 11.2 Undamped Forced Vibration

Harmonic forcing F₀·sin(ω·t):

**m·ẍ + k·x = F₀·sin(ω·t)**

- **Steady-state amplitude:** X = (F₀/k) / |1 − (ω/ω_n)²|
- **Magnification factor:** MF = 1 / |1 − (ω/ω_n)²|
- **Resonance:** when ω → ω_n, the amplitude grows without bound (in the undamped ideal). The forcing frequency ratio ω/ω_n governs the response.

### 11.3 Damped Free Vibration

Viscous damping (damper constant c):

**m·ẍ + c·ẋ + k·x = 0**

- **Critical damping coefficient:** c_c = 2·m·ω_n = 2·√(k·m)
- **Damping ratio:** ζ = c/c_c
- Three regimes:
  - **ζ > 1 — overdamped:** returns to equilibrium slowly, no oscillation.
  - **ζ = 1 — critically damped:** returns fastest without oscillating.
  - **ζ < 1 — underdamped:** oscillates with decaying amplitude; **damped natural frequency** ω_d = ω_n·√(1 − ζ²).

### 11.4 Damped Forced Vibration

m·ẍ + c·ẋ + k·x = F₀·sin(ω·t). Steady-state amplitude:

X = (F₀/k) / √([1 − (ω/ω_n)²]² + [2·ζ·(ω/ω_n)]²)

Damping limits the amplitude at resonance to a finite value; the peak shifts slightly below ω_n.

### 11.5 Procedure (Vibrations)

1. Draw the FBD at a general displaced position x (or angle θ); measure displacement from the **static equilibrium** position — this cancels gravity/static spring force.
2. Apply ΣF = ma (or ΣM = Iα for rotational systems) to get the equation of motion.
3. Put it in standard form ẍ + 2ζω_n·ẋ + ω_n²·x = (forcing). Read off ω_n and ζ.
4. Identify the case (free/forced, damped/undamped) and write the solution.
5. Apply initial conditions for free vibration; compute amplitude/MF for forced vibration.

### 11.6 Pitfalls

- Not measuring x from the static-equilibrium position — then gravity appears in the equation unnecessarily.
- Mixing up ω (forcing frequency) and ω_n (natural frequency).
- Forgetting that ω_d ≠ ω_n when damping is present.
- For rotational vibration, using the wrong moment of inertia or forgetting to include the spring's moment arm (effective torsional stiffness).

---

## 12. General Problem-Solving Strategy (Dynamics)

1. **Classify the problem:** kinematics or kinetics? Particle or rigid body? Which method (F=ma, work-energy, impulse-momentum)?
2. **Choose coordinates:** rectangular, n–t, polar (kinematics); FBD axes (kinetics).
3. **Kinematics first:** establish relationships between positions, velocities, accelerations (including constraints — pulleys, rolling, linkages).
4. **Draw the FBD and (for kinetics) the kinetic diagram.**
5. **Write the governing equations** for the chosen method; add kinematic constraint equations to match unknowns.
6. **Solve** the simultaneous equations.
7. **Check:** units, signs, limiting cases, order-of-magnitude reasonableness. A negative acceleration/force means the assumed direction was opposite.

**Universal pitfalls:**
- Choosing the wrong method (using F=ma for a problem that wants speed-vs-position — work-energy is far easier, and vice versa).
- Forgetting kinematic constraints (rolling without slipping, pulley relations) — these are extra equations you need.
- Non-inertial reference frame without the proper correction terms (Coriolis).
- Sign inconsistency between position, velocity, acceleration, and force.
- Confusing mass moment of inertia axes (I_G vs I_O).
- Constant-acceleration formulas applied when acceleration is not constant.
- a_n = v²/ρ forgotten for curved paths even at constant speed.

---

## Open-source sources used

- **Mechanics Map — Open Textbook Project** — Jacob Moore et al., Penn State. http://adaptivemap.ma.psu.edu/ and https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.) — used for the chapter structure and content of particle kinematics, Newton's second law for particles, work and energy in particles, impulse and momentum in particles, rigid body kinematics (including relative motion analysis), Newton's second law for rigid bodies, work and energy in rigid bodies, impulse and momentum in rigid bodies, and vibrations with one degree of freedom.
- **Mechanics Map — Relative Motion Analysis** — https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.)/11:_Rigid_Body_Kinematics/11.4:_Relative_Motion_Analysis — used for the rigid-body relative velocity/acceleration equations and rotating-frame (Coriolis) analysis.
- **Mechanics Map — Impulse and Momentum for a Rigid Body System** — https://mechanicsmap.psu.edu/websites/15_impulse_momentum_rigid_body/ — used for linear/angular momentum of rigid bodies and eccentric impact.
- **Engineering Statics: Open and Interactive** — Daniel W. Baker and William Haynes. https://engineeringstatics.org/ — used for the shared free-body-diagram methodology, mass moment of inertia / parallel-axis theorem foundation, and the kinematics of normal-tangential and polar coordinate systems (cross-referenced for consistency with the statics companion).
- **Engineering Mechanics: Dynamics** (open-access adaptations of Mechanics Map in the Open Textbook Library / LibreTexts ecosystem) — used for the method-selection framing and worked-example problem patterns across the three kinetics methods.
