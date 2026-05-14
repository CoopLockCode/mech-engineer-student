# Statics Reference

A graduate-level study companion for **ENGR 2214 — Statics**. Covers force systems, equilibrium of particles and rigid bodies, structural analysis (trusses, frames, machines), distributed loads, centroids, area moments of inertia, friction, and internal forces with shear/moment diagrams.

Statics is the branch of mechanics that studies bodies in **equilibrium** — at rest or moving with constant velocity — so that the net force and net moment acting on the body are both zero. Every problem in this course reduces to drawing a correct free-body diagram and applying ΣF = 0 and ΣM = 0.

---

## 1. Fundamental Concepts

### 1.1 Definitions

- **Particle** — a body whose size/shape is irrelevant to the problem; all forces act through a single point (concurrent force system). No moment equations needed.
- **Rigid body** — a body that does not deform; distances between internal points are fixed. Forces act at different points, so moments matter.
- **Force** — a vector quantity (push or pull) with magnitude, direction, line of action, and point of application. SI unit: newton (N). US unit: pound (lb).
- **Moment (torque)** — the tendency of a force to rotate a body about a point or axis. Units: N·m or lb·ft.
- **Couple** — two equal, opposite, non-collinear forces; produces pure rotation (a "free vector" moment), no net force.
- **Equilibrium** — the state in which the resultant force and resultant moment on a body are both zero.
- **Concentrated load** — a force idealized as acting at a point.
- **Distributed load** — a force spread over a length, area, or volume (e.g., N/m, Pa).

### 1.2 Newton's Laws (statics context)

1. **First Law** — A body in equilibrium remains in equilibrium. (Basis of all statics: ΣF = 0.)
2. **Second Law** — F = ma. In statics a = 0, so ΣF = 0.
3. **Third Law** — For every action there is an equal and opposite reaction. (Critical for FBDs of connected bodies — internal forces appear in equal-and-opposite pairs.)

### 1.3 Newton's Law of Gravitation / Weight

W = m·g, with g = 9.81 m/s² (or 32.2 ft/s²). Weight always acts vertically downward, through the body's **center of gravity**.

### 1.4 Units & Prefixes

| Quantity | SI | US Customary |
|---|---|---|
| Length | m | ft |
| Force | N | lb |
| Mass | kg | slug |
| Moment | N·m | lb·ft |
| Stress/Pressure | Pa (N/m²) | psi (lb/in²) |

1 N = 1 kg·m/s². 1 slug = 1 lb·s²/ft. Always carry units through; mismatched units are the #1 silent error.

### 1.5 Significant Figures Convention

Report results to 3 significant figures (engineering standard). Carry 4+ digits through intermediate steps to avoid round-off accumulation.

---

## 2. Vectors and Force Representation

### 2.1 Scalars vs. Vectors

- **Scalar** — magnitude only (mass, time, speed, temperature).
- **Vector** — magnitude + direction (force, moment, position, velocity).

### 2.2 Vector Operations

- **Addition (parallelogram / triangle rule):** R = A + B. Vectors add tip-to-tail.
- **Law of cosines** (for resultant magnitude): R² = A² + B² − 2AB·cos(θ_between supplement).
- **Law of sines** (for direction): A/sin α = B/sin β = R/sin γ.
- **Components:** any vector resolves into rectangular components along chosen axes.

### 2.3 Cartesian Vector Form (2D)

A = A_x **i** + A_y **j**

- A_x = A·cos θ, A_y = A·sin θ (θ measured from +x axis)
- Magnitude: A = √(A_x² + A_y²)
- Direction: θ = atan2(A_y, A_x)

### 2.4 Cartesian Vector Form (3D)

A = A_x **i** + A_y **j** + A_z **k**

- Magnitude: A = √(A_x² + A_y² + A_z²)
- **Unit vector:** **u** = A / |A| = (A_x/A)**i** + (A_y/A)**j** + (A_z/A)**k**
- **Direction cosines:** cos α = A_x/A, cos β = A_y/A, cos γ = A_z/A, with cos²α + cos²β + cos²γ = 1
- A force of magnitude F along a line: F = F·**u**, where **u** is the unit vector of that line.

### 2.5 Position Vectors

From point A(x_A, y_A, z_A) to point B(x_B, y_B, z_B):

**r**_AB = (x_B − x_A)**i** + (y_B − y_A)**j** + (z_B − z_A)**k**

Unit vector along AB: **u**_AB = **r**_AB / |**r**_AB|. This is how you express a force directed along a known geometric line (cables, members).

### 2.6 Dot Product

**A · B** = A_x B_x + A_y B_y + A_z B_z = |A||B| cos θ

Uses:
- **Angle between two vectors:** θ = cos⁻¹( (A·B) / (|A||B|) )
- **Projection of A onto a line with unit vector u:** A_∥ = A · **u** (a scalar); vector projection = (A·**u**)**u**
- Perpendicular component: A_⊥ = √(A² − A_∥²)

### 2.7 Cross Product

**A × B** = |A||B| sin θ **n** (n by right-hand rule). Determinant form:

```
        | i    j    k  |
A × B = | A_x  A_y  A_z |
        | B_x  B_y  B_z |
```

= (A_y B_z − A_z B_y)**i** − (A_x B_z − A_z B_x)**j** + (A_x B_y − A_y B_x)**k**

The cross product is the primary tool for computing moments in 2D and 3D.

**Pitfall:** the cross product is NOT commutative — A × B = −(B × A). Order matters: for a moment it is always **r × F**, position-then-force.

---

## 3. Moments and Couples

### 3.1 Moment of a Force About a Point

**Vector method (general, best for 3D):**

**M**_O = **r** × **F**

where **r** is the position vector from the moment point O to *any point on the line of action* of F.

**Scalar method (2D):**

M_O = F·d

where d is the **perpendicular distance** (moment arm) from O to the line of action of F.

**Sign convention (2D):** counterclockwise positive (+, out of page, +k); clockwise negative. Be consistent across the whole problem.

### 3.2 Principle of Moments (Varignon's Theorem)

The moment of a force about a point equals the sum of the moments of its components about that point:

M_O = Σ (M of each component) = x·F_y − y·F_x  (2D, with force components at point (x,y))

This lets you avoid finding perpendicular distances — resolve F into components and use their (often simpler) moment arms.

### 3.3 Moment of a Force About an Axis

The component of a moment along a specified axis. Used when a body can only rotate about a particular axis (e.g., a door hinge):

M_axis = **u**_axis · (**r** × **F**)

This is the **scalar triple product** — a determinant:

```
          | u_x  u_y  u_z |
M_axis =  | r_x  r_y  r_z |
          | F_x  F_y  F_z |
```

The moment **vector** about the axis is M_axis · **u**_axis.

### 3.4 Couples

A couple is two equal, opposite, parallel forces separated by distance d.

- **Couple moment magnitude:** M = F·d (d = perpendicular distance between the two forces)
- A couple is a **free vector** — its moment is the same about every point in space.
- Vector form: **M** = **r** × **F**, where **r** runs from any point on one force's line of action to any point on the other's.
- Couples can be added like vectors and moved anywhere on the body without changing the effect.

### 3.5 Equivalent Systems — Force-Couple Resultant

Any force system on a rigid body can be reduced to a single resultant force **R** acting at a chosen point O plus a single resultant couple **M**_O:

- **R** = Σ**F**
- **M**_O = Σ**M**_O = Σ(**r** × **F**) + Σ(applied couples)

**Moving a force:** to slide a force off its line of action to a new point, you must add a couple equal to the moment the force produced about the new point.

**Special reductions:**
- If **R** ≠ 0 and **R** ⊥ **M**_O → reduces to a single resultant force on a new line of action.
- 2D systems and parallel force systems always reduce to a single resultant force (unless R = 0, then a pure couple).
- A **wrench** (collinear force + couple) is the most general 3D reduction.

### 3.6 Distributed Loads → Equivalent Concentrated Force

For a line load w(x) (force per unit length) along a beam:

- **Resultant magnitude:** F_R = ∫ w(x) dx = **area under the load curve**
- **Location (line of action):** x̄ = [∫ x·w(x) dx] / [∫ w(x) dx] = **centroid of the load area**

Common cases:
| Load shape | Resultant magnitude | Location from one end |
|---|---|---|
| Uniform, intensity w₀ over length L | w₀·L | L/2 (centroid of rectangle) |
| Triangular, 0 → w₀ over length L | ½·w₀·L | 2L/3 from the zero end (L/3 from the max end) |
| Trapezoidal | split into rectangle + triangle | superpose the two resultants |

**Pitfall:** the resultant of a triangular load is at the centroid of the triangle (1/3 from the large end), NOT the midpoint.

---

## 4. Equilibrium of a Particle

### 4.1 Conditions

A particle is in equilibrium when the resultant of all forces is zero:

**ΣF = 0**

2D scalar equations: **ΣF_x = 0**, **ΣF_y = 0** → solves **2 unknowns**.

3D scalar equations: **ΣF_x = 0**, **ΣF_y = 0**, **ΣF_z = 0** → solves **3 unknowns**.

### 4.2 Free-Body Diagram (FBD) for a Particle

1. Isolate the particle (the point/joint).
2. Draw every force acting on it: applied loads, cable tensions (always pull *away* from the particle, along the cable), spring forces, weight, contact/normal forces.
3. Label magnitudes and angles.

### 4.3 Springs

Linear (Hookean) spring: **F_s = k·s**, where k = spring constant (N/m) and s = deformation from the natural (unstretched) length. F_s pulls if stretched, pushes if compressed.

### 4.4 Cables and Pulleys

- A continuous cable over a **frictionless** pulley has the **same tension** throughout.
- Cable tension always acts along the cable, pulling away from the body.

### 4.5 Solution Procedure (Particle Equilibrium)

1. Identify the particle to analyze.
2. Draw the FBD; establish x–y (or x–y–z) axes.
3. Write force equations: resolve each force into components.
4. Apply ΣF_x = 0, ΣF_y = 0 (and ΣF_z = 0 in 3D).
5. Solve the simultaneous equations.
6. Check: a negative result means the assumed direction was wrong (the force acts opposite to assumed) — the magnitude is still valid.

---

## 5. Equilibrium of a Rigid Body

### 5.1 Conditions for Equilibrium

Both the net force and the net moment must vanish:

**ΣF = 0**  and  **ΣM = 0** (about any point)

**2D (three independent equations):**
- ΣF_x = 0
- ΣF_y = 0
- ΣM_O = 0  (O = any point in the plane)

→ solves **3 unknowns**.

Alternative valid 2D equation sets:
- Two-force, one-moment: ΣF_x = 0, ΣM_A = 0, ΣM_B = 0 (A, B not on a line ⊥ to x)
- Three-moment: ΣM_A = 0, ΣM_B = 0, ΣM_C = 0 (A, B, C not collinear)

**3D (six independent equations):**
- ΣF_x = 0, ΣF_y = 0, ΣF_z = 0
- ΣM_x = 0, ΣM_y = 0, ΣM_z = 0

→ solves **6 unknowns**. Best handled with vectors: ΣF = 0 and ΣM_O = Σ(r × F) = 0.

### 5.2 Support Reactions (2D) — what each support provides

| Support type | Reactions provided | Unknowns |
|---|---|---|
| Cable / link / rod | 1 force along the cable/link | 1 |
| Roller / rocker / frictionless surface | 1 force ⊥ to surface | 1 |
| Smooth pin in slot | 1 force ⊥ to slot | 1 |
| Frictionless pin / hinge | 2 force components (no moment) | 2 |
| Rough surface | normal force + friction force | 2 |
| Fixed support (built-in / cantilever) | 2 force components + 1 couple moment | 3 |

**Rule of thumb:** a support resists translation in a direction → produces a force in that direction. A support resists rotation → produces a couple moment.

### 5.3 Support Reactions (3D)

| Support | Forces | Moments |
|---|---|---|
| Cable / smooth contact | 1 | 0 |
| Roller on surface | 1 | 0 |
| Ball-and-socket joint | 3 | 0 |
| Smooth pin / hinge | 2 (⊥ to axis) | 2 (⊥ to axis) — often 0 if other supports carry it |
| Smooth bearing / journal bearing | 2 | 2 |
| Fixed support | 3 | 3 |

### 5.4 Free-Body Diagram Methodology (Rigid Body) — 5 Steps

This is the single most important skill in statics. From *Engineering Statics (Baker & Haynes)*:

1. **Isolate the body.** Sketch the outline of the object as if floating in space, disconnected from all supports and other bodies.
2. **Establish a coordinate system.** Choose a right-handed x–y (–z) frame that simplifies the equations.
3. **Add applied forces and couples.** Draw all *known* loads, including the weight at the center of gravity if not negligible. Label with values or symbols.
4. **Replace each support with its reactions.** Wherever you "cut" a support to isolate the body, draw the force(s) and/or couple(s) that support provides (see tables 5.2/5.3). Assume directions for unknowns.
5. **Label everything.** Dimensions, angles, and every force/moment — known values or unknown symbols.

**FBD best practices:**
- Draw weight from the center of gravity, straight down.
- For a frictionless pin, you cannot know the reaction direction in advance — draw two perpendicular components (A_x, A_y).
- Internal forces between connected bodies do not appear on the FBD of the whole assembly; they only appear when you separate the bodies (Newton's 3rd law: equal & opposite pairs).
- If a member is a **two-force member**, draw its force along the line connecting the two pins.

### 5.5 Two-Force and Three-Force Members

- **Two-force member:** a body with forces applied at *only two points* and no couples. For equilibrium, the two forces must be **equal, opposite, and collinear** — directed along the line joining the two points. The member is in pure tension or pure compression. (Recognizing these massively simplifies frame/machine problems.)
- **Three-force member:** a body with forces at exactly three points. The three forces must be either **concurrent** (all lines of action meet at one point) or **parallel**. Using concurrency can replace moment equations with geometry.

### 5.6 Statical Determinacy

- **Statically determinate:** number of unknown reactions = number of independent equilibrium equations. Solvable with statics alone.
- **Statically indeterminate:** more unknowns than equations (redundant supports). Requires deformation/material relations (covered in Mechanics of Materials).
- **Improperly constrained (partial constraint):** too few or badly arranged supports → body can move. Watch for **concurrent reactions** (all reaction lines meet at a point → no resistance to rotation about that point) and **parallel reactions** (no resistance to a force perpendicular... actually parallel reactions cannot resist a transverse load).

### 5.7 Solution Procedure (Rigid Body Equilibrium)

1. Draw the FBD (5-step method above).
2. Choose coordinate axes.
3. **Write the moment equation first**, summing moments about a point where the *most unknowns intersect* — this eliminates them and often gives one unknown directly.
4. Write the force equations ΣF_x = 0, ΣF_y = 0.
5. Solve. Negative result → direction was assumed wrong.
6. Verify with an independent moment equation about a different point.

**Strategic tip:** picking the moment center wisely (where 2 of 3 unknowns pass through) turns a 3×3 system into three sequential single-unknown solves.

---

## 6. Structural Analysis — Trusses

### 6.1 Definitions and Assumptions

A **truss** is a structure of slender members connected at joints, designed to carry loads primarily as axial forces.

**Idealizing assumptions for a "simple truss":**
1. Members are connected by **frictionless pins** (joints transmit force, not moment).
2. Loads and reactions are applied **only at the joints**.
3. Member weight is negligible (or split half to each end joint).
4. Therefore **every member is a two-force member** — pure tension or pure compression.

**Sign convention:** **Tension (T) positive** — member pulls on the joint (force points away from joint, into the member). **Compression (C) negative** — member pushes on the joint.

### 6.2 Determinacy of Trusses

For a planar truss with *m* members, *r* reactions, *j* joints:
- m + r = 2j → statically determinate
- m + r > 2j → statically indeterminate
- m + r < 2j → unstable (mechanism)

(For space trusses: m + r vs. 3j.)

### 6.3 Method of Joints

Best when you need **all** member forces.

**Procedure:**
1. Find the support reactions using the FBD of the whole truss (3 equilibrium equations).
2. Select a joint with **at most 2 unknown member forces** (and known/solvable loads).
3. Draw the FBD of that joint (a particle — concurrent forces). Assume all unknown members are in **tension** (arrows pointing away from the joint).
4. Apply ΣF_x = 0 and ΣF_y = 0; solve the 2 unknowns.
5. Move to the next joint with ≤ 2 unknowns; repeat until all members are found.
6. Interpret signs: positive = tension (as assumed), negative = compression.

### 6.4 Zero-Force Members

Identify by inspection before computing — they carry no load (for the given loading) but provide stability/prevent buckling.

- **Rule 1:** At a joint with **only two non-collinear members** and **no external load/reaction**, both members are zero-force.
- **Rule 2:** At a joint with **three members**, where **two are collinear** and there is **no external load**, the third (non-collinear) member is zero-force.

### 6.5 Method of Sections

Best when you need the force in **one or a few specific members**.

**Procedure:**
1. Find the support reactions (FBD of whole truss).
2. Pass an imaginary **cut** through the truss, slicing through the member(s) of interest — ideally **no more than 3 unknown members** (3 equilibrium equations available).
3. Draw the FBD of one portion (the side with fewer forces). Replace each cut member with its axial force, assumed **in tension**.
4. Apply equilibrium: ΣF_x = 0, ΣF_y = 0, ΣM = 0.
5. **Strategic moment centers:** sum moments about the point where two of the three unknown members intersect → solve the third directly. Use ΣF for members that are parallel.
6. Interpret signs (positive = tension).

**Pitfall:** the cut must completely separate the truss into two parts. Members that are only partially cut, or a cut leaving >3 unknowns with no special geometry, cannot be solved by one section.

### 6.6 Combined Strategy

Often: use method of sections to get a few key members fast, then method of joints to fill in the rest. They are fully compatible.

---

## 7. Frames and Machines

### 7.1 Definitions

- **Frame** — a structure with **at least one multi-force member** (a member with forces at 3+ points or with applied couples), designed to be **stationary** and support loads.
- **Machine** — like a frame but contains **moving parts**, designed to transmit/modify forces (pliers, cranes, presses). Analyzed identically.

The key distinction from trusses: frames/machines contain **multi-force members**, so member forces are NOT simply axial — they have components and the line of action is unknown.

### 7.2 Analysis Procedure

1. **FBD of the entire structure** — find as many external reactions as possible (use 3 equilibrium equations). If determinate as a whole, get all reactions here.
2. **Dismember the structure** — draw a separate FBD for each member (or sub-assembly).
3. **Apply Newton's third law:** at every pin connecting two members, the forces are **equal and opposite** on the two members. Use the *same symbols* with reversed arrows.
4. **Identify two-force members first** — their force is along the line joining their two pins; this reduces 2 unknowns to 1 per such member.
5. Write equilibrium equations for each member's FBD (3 per member in 2D).
6. Solve the system. Choose moment centers wisely to decouple equations.

### 7.3 Critical Pitfalls

- **Consistency of pin force directions:** if you assume pin force at C on member AB points up-and-right, then on member BC it MUST point down-and-left. The most common frame error is breaking this consistency.
- **Don't double-count:** an external load applied *at a pin* goes on only one member's FBD (state which), or is handled at the pin — never on both.
- **Two-force member recognition:** a member that is pinned at two points only, with nothing else applied to it, is a two-force member even inside a frame. Drawing its force as two components instead of one axial force creates extra unknowns and often an unsolvable system.
- **Count unknowns vs. equations** before solving — confirm the problem is determinate.

---

## 8. Internal Forces in Members

### 8.1 The Three Internal Resultants (2D)

When you cut a member, the internal force system on the cut cross-section is represented by three resultants:

- **Normal force (N)** — axial; perpendicular to the cross-section. Tension positive.
- **Shear force (V)** — tangent to the cross-section (transverse).
- **Bending moment (M)** — couple about the centroidal axis of the section.

(In 3D add: two shear components, axial force, two bending moments, and torsion T.)

### 8.2 Finding Internal Forces at a Point — Procedure

1. Find the support reactions (FBD of whole member).
2. Make an imaginary cut at the section of interest.
3. Draw the FBD of one portion (choose the simpler side).
4. At the cut, draw N, V, M in their **positive sense** (see sign convention below).
5. Apply ΣF_x = 0 → N; ΣF_y = 0 → V; ΣM_cut = 0 → M.

### 8.3 Sign Convention for Beams (standard)

Consider the cut and look at the portion on the left:
- **Positive N:** tension (pulls the section apart).
- **Positive V:** acts **downward** on the right face of a left segment (rotates the segment clockwise); equivalently, V is positive if it tends to rotate the beam element clockwise.
- **Positive M:** **sagging** — concave up (compression on top fibers, tension on bottom fibers). "A smile is positive."

Consistency is everything: pick the convention and apply it the same way at every cut.

---

## 9. Shear and Moment Diagrams

The complete method — this is a guaranteed exam topic.

### 9.1 Purpose

Shear (V) and bending-moment (M) diagrams show how internal shear and moment vary along the length of a beam, identifying the critical sections for design (max |V|, max |M|).

### 9.2 Method 1 — Section Method (by equations)

1. Find all support reactions.
2. Identify **regions** between "events" — points where a concentrated load, reaction, applied couple, or a change in distributed-load function occurs. Each region needs its own equations.
3. In each region, make a cut at distance x; draw the FBD of the left (or right) portion.
4. Write V(x) from ΣF_y = 0 and M(x) from ΣM_cut = 0 as functions of x.
5. Plot V(x) and M(x) region by region.

### 9.3 Method 2 — Graphical Method (relationships between load, shear, moment)

This is faster and is the expected method for most exam problems. Governing differential/integral relationships:

**Slope relationships:**
- dV/dx = −w(x)  → the slope of the shear diagram at a point equals the negative of the distributed load intensity there.
- dM/dx = V(x)  → the slope of the moment diagram at a point equals the shear there.

**Area (integral) relationships:**
- ΔV = V₂ − V₁ = −∫ w dx = −(area under the load diagram between the two points)
- ΔM = M₂ − M₁ = ∫ V dx = (area under the shear diagram between the two points)

**Jump (discontinuity) rules:**
- A **downward concentrated force P** causes the shear diagram to **jump down by P** at that point.
- A **concentrated couple M₀** causes the moment diagram to **jump** at that point (jump down by M₀ for a CW applied couple, up for CCW — check convention).
- Concentrated forces do **not** create jumps in the moment diagram; concentrated couples do **not** create jumps in the shear diagram.

### 9.4 Step-by-Step Graphical Procedure

1. **Reactions** — solve the whole-beam FBD for all support reactions.
2. **Set up axes** — draw the beam to scale; put V diagram directly below it, M diagram below that, aligned.
3. **Build the V diagram left to right:**
   - Start at V = 0 to the left of the beam.
   - At each concentrated force/reaction, jump by that force (up for upward force).
   - Between loads: slope of V = −w. (No distributed load → V is horizontal/constant. Uniform load → V is a straight sloped line. Triangular load → V is a parabola.)
   - V must return to zero just past the right end (check).
4. **Build the M diagram left to right:**
   - Start at M = 0 at a simply-supported (pinned/roller) free end; for a cantilever's fixed end the moment equals the reaction couple.
   - Change in M between two points = area under the V diagram between them.
   - Slope of M = V. Where V is positive, M rises; where V is negative, M falls; where V = 0, M has a **local max or min**.
   - At a concentrated couple, jump M by the couple's magnitude.
   - M must return to zero at a free/simply-supported end (check).
5. **Locate the maximum moment** — it occurs where **V = 0** or where V crosses zero (or at a couple discontinuity). If V is a sloped line, find x where V = 0 by similar triangles, then compute M there.

### 9.5 Curve-Degree Rule (sanity check)

The diagrams increase in polynomial degree as you integrate:
| Load w(x) | Shear V(x) | Moment M(x) |
|---|---|---|
| Zero (no load) | Constant | Linear (sloped) |
| Constant (uniform) | Linear | Parabolic (2nd deg) |
| Linear (triangular) | Parabolic | Cubic (3rd deg) |

### 9.6 Common Pitfalls

- Forgetting that **dV/dx = −w** (sign on the load) — a downward load gives a *negative* shear slope.
- Missing the jump at a concentrated load or couple.
- Not checking that V and M close back to zero at the ends — a built-in check.
- Looking for max M only at concentrated loads; it can occur anywhere V = 0.
- Confusing the applied-couple jump direction in the M diagram — derive it from a cut if unsure.

---

## 10. Centroids and Centers of Gravity

### 10.1 Definitions

- **Center of gravity (CG)** — the point where the total weight of a body can be considered concentrated.
- **Center of mass (CM)** — same point assuming uniform gravity; depends on mass distribution.
- **Centroid** — the geometric center of a line, area, or volume; coincides with CG/CM when the body is homogeneous (uniform density) and of uniform thickness.

### 10.2 Centroid by Integration

For an area A:

x̄ = (∫ x_el dA) / (∫ dA),  ȳ = (∫ y_el dA) / (∫ dA)

where (x_el, y_el) is the centroid of the differential element dA. Choose the element (vertical strip, horizontal strip, or dA = dx dy) to make the integral easiest.

For a volume: x̄ = (∫ x dV)/(∫ dV), etc. For a line (wire): x̄ = (∫ x dL)/(∫ dL).

For a **composite body of different materials**, use weight or density: x̄ = Σ(x̄ᵢ Wᵢ)/ΣWᵢ.

### 10.3 Centroid by Composite Parts (Method of Composite Areas)

Break a complex shape into simple shapes with known centroids (from the table below). Treat **holes/cutouts as negative areas**.

x̄ = Σ(x̄ᵢ Aᵢ) / Σ Aᵢ,  ȳ = Σ(ȳᵢ Aᵢ) / Σ Aᵢ

**Procedure:**
1. Divide the shape into standard parts; number them.
2. Tabulate: part, Aᵢ, x̄ᵢ, ȳᵢ, Aᵢx̄ᵢ, Aᵢȳᵢ. Use negative area for holes.
3. Sum the columns.
4. x̄ = ΣAx̄ / ΣA, ȳ = ΣAȳ / ΣA.

### 10.4 Centroid Table — Common Areas

(Origin at the indicated reference; measure x̄, ȳ from the reference shown.)

| Shape | Area A | x̄ | ȳ |
|---|---|---|---|
| Rectangle (b wide, h tall, origin at corner) | b·h | b/2 | h/2 |
| Right triangle (base b, height h, right angle at origin) | b·h/2 | b/3 | h/3 |
| General triangle | b·h/2 | — | h/3 (from base) |
| Circle (radius r, origin at center) | π r² | 0 | 0 |
| Semicircle (radius r, flat side on x-axis) | π r²/2 | 0 | 4r/(3π) |
| Quarter circle (radius r, in first quadrant) | π r²/4 | 4r/(3π) | 4r/(3π) |
| Circular sector (radius r, half-angle α from x-axis) | α r² | (2r sin α)/(3α) | 0 |
| Circular arc (radius r, half-angle α) [line] | 2αr (length) | (r sin α)/α | 0 |
| Semicircular arc (radius r) [line] | πr (length) | 0 | 2r/π |
| Parabolic spandrel (y = kx², spans 0→b, 0→h) | b·h/3 | 3b/4 | 3h/10 |
| Parabolic area under y=kx² complement (the "filled" parabola, area = 2bh/3) | 2b·h/3 | 3b/8 | 3h/5 |
| Semiparabola (vertex at top) | 2b·h/3 | 3b/8 | 3h/5 |
| Quarter ellipse (semi-axes a, b) | π a b /4 | 4a/(3π) | 4b/(3π) |
| Exponential spandrel (y = h·eᵏˣ type) | — | use integration | use integration |

### 10.5 Centroid Table — Common Volumes / Lines

| Solid | Volume V | Centroid (from base/apex) |
|---|---|---|
| Hemisphere (radius r) | (2/3)π r³ | 3r/8 from flat face |
| Cone (radius r, height h) | (1/3)π r² h | h/4 from base |
| Pyramid (base area A, height h) | A·h/3 | h/4 from base |
| Paraboloid of revolution (radius r, height h) | ½π r² h | h/3 from base |

### 10.6 Theorems of Pappus and Guldinus

For a surface of revolution generated by rotating a **plane curve** of length L about a non-intersecting axis through angle θ (radians):

**Surface area:** A = θ·r̄·L,  where r̄ = distance from the axis to the curve's centroid.

For a volume of revolution generated by rotating a **plane area** A about a non-intersecting axis:

**Volume:** V = θ·r̄·A,  where r̄ = distance from the axis to the area's centroid.

(For a full revolution θ = 2π.) These give quick areas/volumes from centroid data and vice versa.

---

## 11. Area Moments of Inertia

### 11.1 Definitions

The **area moment of inertia** (second moment of area) quantifies how an area is distributed about an axis — it governs a beam's resistance to bending and a column's resistance to buckling.

- About x-axis: **I_x = ∫ y² dA**
- About y-axis: **I_y = ∫ x² dA**
- **Polar moment of inertia** (about z, ⊥ to the plane through O): **J_O = ∫ r² dA = I_x + I_y** (perpendicular axis theorem)
- **Product of inertia:** **I_xy = ∫ x·y dA** (zero if either axis is an axis of symmetry)

Units: length⁴ (m⁴, mm⁴, in⁴). Moment of inertia is always positive; product of inertia can be ±.

### 11.2 Parallel-Axis Theorem (Steiner's Theorem)

To shift a moment of inertia from a **centroidal axis** to a parallel axis:

**I = Ī + A·d²**

where Ī = moment of inertia about the centroidal axis, A = area, d = perpendicular distance between the two parallel axes.

For polar: J_O = J̄ + A·d². For product of inertia: I_xy = Ī_x'y' + A·d_x·d_y.

**Critical:** the parallel-axis theorem can only transfer **to or from the centroidal axis** — you cannot jump directly between two non-centroidal axes. To go from axis 1 to axis 2: bring it to the centroid first (subtract A·d₁²), then push out to axis 2 (add A·d₂²).

### 11.3 Radius of Gyration

The distance at which the entire area could be concentrated to give the same moment of inertia:

k_x = √(I_x / A),  k_y = √(I_y / A),  k_O = √(J_O / A),  with k_O² = k_x² + k_y²

### 11.4 Moment of Inertia by Composite Parts — Procedure

1. Divide the area into standard shapes (table below).
2. For each part, find its **centroidal** moment of inertia Ī from the table.
3. Find the distance d from each part's centroid to the **reference axis** for the whole shape.
4. Apply the parallel-axis theorem to each part: Iᵢ = Īᵢ + Aᵢ·dᵢ².
5. Sum: I_total = Σ Iᵢ. (Subtract for holes.)
6. Tabulate: part, Aᵢ, d, Īᵢ, Aᵢdᵢ², Iᵢ.

### 11.5 Moment-of-Inertia Table — Common Areas (about CENTROIDAL axes unless noted)

| Shape | Ī_x (centroidal) | Ī_y (centroidal) | Other |
|---|---|---|---|
| Rectangle (base b, height h) | b·h³ / 12 | h·b³ / 12 | About base edge: b·h³/3 |
| Right triangle (base b, height h) | b·h³ / 36 | h·b³ / 36 | About base edge: b·h³/12 |
| Circle (radius r) | π r⁴ / 4 | π r⁴ / 4 | J_O = π r⁴ / 2 |
| Hollow circle (R outer, r inner) | π(R⁴ − r⁴)/4 | π(R⁴ − r⁴)/4 | J = π(R⁴ − r⁴)/2 |
| Semicircle (radius r) | (π/8 − 8/(9π)) r⁴ ≈ 0.1098 r⁴ | π r⁴ / 8 | About flat base: π r⁴/8 |
| Quarter circle (radius r) | (π/16 − 4/(9π)) r⁴ ≈ 0.0549 r⁴ | same as Ī_x | About each straight edge: π r⁴/16 |
| Ellipse (semi-axes a horizontal, b vertical) | π a b³ / 4 | π b a³ / 4 | J_O = πab(a²+b²)/4 |
| Parabolic spandrel (b × h, y=kx²) | use integration | use integration | — |

(Semicircle/quarter-circle centroidal values come from applying the parallel-axis theorem to the about-the-diameter values, subtracting A·d² with d = 4r/3π.)

### 11.6 Mass Moment of Inertia (preview — used in Dynamics)

For rotational dynamics, the **mass** moment of inertia is **I = ∫ r² dm**. Common results (see Dynamics reference for the full table): thin rod about center = mL²/12; solid disk/cylinder about axis = mr²/2; solid sphere = (2/5)mr². The parallel-axis theorem also applies: I = I_cm + m·d².

### 11.7 Common Pitfalls

- Using a non-centroidal table value as if it were centroidal (or vice versa) — always confirm which axis the table entry references.
- Forgetting A·d² entirely, or using d² for the wrong distance (d is the ⊥ distance between the *parallel* axes).
- Trying to transfer directly between two non-centroidal axes.
- Mixing up I_x (uses y²) and I_y (uses x²).
- Unit inconsistency — I has units of length⁴; a factor-of-1000⁴ error from mm/m mixing is catastrophic.

---

## 12. Friction

### 12.1 Dry (Coulomb) Friction

Friction is the tangential resisting force between two surfaces in contact.

**Static friction** (no sliding yet): 0 ≤ F_s ≤ F_s,max, where

**F_s,max = μ_s · N**

μ_s = coefficient of static friction; N = normal force. Static friction adjusts itself to whatever is needed to maintain equilibrium, up to the maximum.

**Kinetic friction** (sliding occurring):

**F_k = μ_k · N**

with μ_k < μ_s (usually). Kinetic friction acts opposite to the direction of relative sliding motion and is essentially constant.

### 12.2 Angle of Friction

- **Angle of static friction:** φ_s = tan⁻¹(μ_s). The resultant of N and F_s,max makes angle φ_s with the surface normal.
- **Angle of kinetic friction:** φ_k = tan⁻¹(μ_k).
- **Angle of repose:** the steepest incline angle at which a block remains on the verge of sliding equals φ_s.

### 12.3 The Three Friction Problem Types

Friction problems are tricky because you don't always know if F = μN. Classify first:

1. **Equilibrium, no impending motion:** F is unknown; treat F as an ordinary unknown reaction. Solve equilibrium, then **check** F ≤ μ_s·N. If satisfied → body stays put.
2. **Impending motion (on the verge of slipping):** F = μ_s·N is an *additional equation*. Direction of F opposes impending motion.
3. **Motion / sliding:** F = μ_k·N, directed opposite to actual sliding velocity.

**Tipping vs. slipping:** a block on an incline or pushed horizontally may either slide or tip over. Check both:
- **Slipping** impends when F = μ_s·N.
- **Tipping** impends when the normal force N acts at the extreme edge of the contact base (the resultant of N moves to the corner).
- Whichever requires the *smaller* applied load governs — that's the actual failure mode.

### 12.4 Procedure (Friction Equilibrium)

1. Draw the FBD. Friction force direction: opposite to impending/actual motion.
2. Decide the problem type (above).
3. Write equilibrium equations (ΣF_x, ΣF_y, ΣM).
4. If impending motion: add F = μ_s·N for each surface that is slipping.
5. Solve. For "no impending motion," verify F ≤ μ_s·N at the end.
6. For multi-body problems, you may not know which surface slips first — try each assumption and check consistency.

### 12.5 Friction Applications

**Wedges:** Draw separate FBDs of the wedge and the body being moved. Friction acts on every contacting surface, opposing impending motion. With small angles, a wedge is self-locking (stays in place when the driving force is removed) if the friction angle exceeds the wedge angle.

**Square-threaded screws (and jacks):** A screw is an inclined plane wrapped around a cylinder. With lead angle θ (tan θ = L/(2πr), L = lead, r = mean radius):
- Moment to raise the load: M = W·r·tan(θ + φ_s)
- Moment to lower the load: M = W·r·tan(θ − φ_s)
- **Self-locking** if φ_s ≥ θ (screw won't unwind under load). If θ > φ_s, M to lower is negative (load drives the screw back).

**Belt friction (flat belt over a drum):** For a belt on the verge of slipping, the tensions on the two sides relate by:

**T₂ / T₁ = e^(μβ)**

where T₂ > T₁ (T₂ is the side toward which slipping impends / the "tight side"), μ = coefficient of friction, β = angle of contact/wrap **in radians**, e = 2.71828. Used for band brakes, capstans, belt drives.

**Pitfall:** β must be in radians; for a belt wrapping multiple times, β = 2πn + partial.

**Journal bearings (axle friction):** the shaft rides up the side of the bearing; the reaction acts at the contact point, tangent to the "friction circle" of radius r_f = r·sin φ_k ≈ r·μ_k.

**Disk friction / collar bearings, thrust bearings:** friction torque from a flat annular contact under axial load — integrate μ·p·r over the contact area; M = (2/3)μP·(R₂³−R₁³)/(R₂²−R₁²) for a hollow collar.

**Rolling resistance:** caused by deformation of the surface; the resultant normal force acts slightly ahead of the wheel's contact point by a distance *a* (coefficient of rolling resistance). P ≈ W·a/r to keep a wheel rolling at constant speed.

---

## 13. General Problem-Solving Strategy (Statics)

Every statics problem follows the same skeleton:

1. **Read carefully** — identify what's given, what's asked, the type of body (particle vs. rigid body), and the type of system.
2. **Idealize** — replace real supports with idealized ones; decide what's negligible (weight, friction).
3. **Draw the FBD(s)** — the make-or-break step. Isolate, axes, applied loads, support reactions, label everything.
4. **Count** unknowns vs. independent equations — confirm the problem is determinate.
5. **Choose smart equations** — sum moments about points that eliminate unknowns; pick axes that decouple components.
6. **Solve** — algebra/simultaneous equations or vector methods.
7. **Interpret** — negative magnitude = assumed direction was wrong; check tension/compression sense.
8. **Verify** — independent equilibrium equation, units, order-of-magnitude reasonableness.

**Universal pitfalls:**
- Forgetting a force on the FBD (especially weight, friction, or a reaction component).
- Sign errors in moments — fix a convention and never deviate.
- Treating a multi-force member as two-force, or missing a two-force member.
- Internal forces appearing on a whole-body FBD (they shouldn't) or missing the equal-and-opposite pair when dismembering.
- Unit inconsistency.
- Statically indeterminate problem attempted with statics alone.

---

## Open-source sources used

- **Engineering Statics: Open and Interactive** — Daniel W. Baker and William Haynes. Open Textbook Library / Engineering LibreTexts. https://engineeringstatics.org/ and https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Engineering_Statics:_Open_and_Interactive_(Baker_and_Haynes) — used for the five-step free-body-diagram methodology, support-reaction tables, equilibrium equation sets, method of joints / method of sections procedures, frames and machines analysis, centroid and moment-of-inertia tables.
- **Mechanics Map — Open Textbook Project** — Jacob Moore et al., Penn State. http://adaptivemap.ma.psu.edu/ and https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.) — used for the topical structure (concurrent vs. rigid-body equilibrium, statically equivalent systems, engineering structures, friction applications), internal forces, shear/moment diagram relationships, and the moment-integral appendix (centroids and area moments of inertia by integration and composite parts).
- **Engineering Mechanics: Statics** (UPEI Pressbooks adaptation of Mechanics Map) — https://pressbooks.library.upei.ca/statics/ — used for shear/moment diagram procedure and truss analysis cross-reference.
- **Engineering Mechanics — Statics/Structures (ENGR 261)**, Colorado Mesa University OER (CC0/public domain) — https://www.coloradomesa.edu/oer/ — used for introductory definitions and units cross-reference.
- **Engineering Mechanics – Statics (Osgood, Cameron, and Christensen)**, Engineering LibreTexts — used for the internal forces / shear-moment diagram chapter cross-reference.
