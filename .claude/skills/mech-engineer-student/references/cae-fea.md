# Computer-Aided Engineering / Finite Element Analysis Reference

PhD-level study companion for ME 4250 — Computer-Aided Engineering / Finite Element Analysis, Kennesaw State University.
Covers FEA theory (discretization, shape functions, stiffness matrices, assembly, boundary conditions), the direct stiffness method, variational/weak formulations, element types, meshing best practices, convergence, interpreting results, sources of error, and the CAD/CAE workflow.

Math is in plain text: `[K]` = stiffness matrix, `{u}` = displacement vector, `^T` = transpose, `x^2` = x squared, `d/dx` = derivative, integral notation written `INT(...)dx`.

---

## 1. What FEA Is — and Is Not

### 1.1 Definition
The **Finite Element Method (FEM)** is a numerical technique for obtaining approximate solutions to boundary-value problems governed by partial differential equations. It works by **discretizing** a continuous domain (infinite degrees of freedom) into a finite number of **elements** connected at **nodes** (finite degrees of freedom), approximating the field variable within each element with simple **shape (interpolation) functions**, deriving element-level equations, assembling them into a global system, applying boundary conditions, and solving.

A finite element method is characterized by four ingredients: a **variational (or weak) formulation**, a **discretization strategy**, one or more **solution algorithms**, and **post-processing procedures**.

### 1.2 What FEA gives you
Approximate nodal values of the primary field variable (displacement in structural problems, temperature in thermal, etc.), from which derived quantities (stress, strain, heat flux, reactions) are computed. **It is an approximation** — the quality depends entirely on the model (mesh, elements, BCs, material model, loads). FEA does not "find the answer"; it solves *the model you built*. Garbage in, garbage out.

### 1.3 Common student misconception
FEA does not replace engineering judgment, hand calculations, or experiment. Hand calcs validate the FEA; FEA extends hand calcs to geometry/loading too complex to solve analytically.

---

## 2. The Direct Stiffness Method (DSM) — the Structural Backbone

### 2.1 The spring/bar element — the fundamental building block
A 1-D linear spring element with stiffness k, nodes i and j, axial displacements u_i and u_j, and nodal forces f_i and f_j.

Element equilibrium:
```
[ k   -k ] { u_i }   { f_i }
[ -k   k ] { u_j } = { f_j }
```
So the **element stiffness matrix** is:
`[k_e] = k * [ 1  -1 ; -1  1 ]`

Key properties of every stiffness matrix:
- **Symmetric** — `[K] = [K]^T` (a consequence of the reciprocal theorem / Maxwell-Betti).
- **Singular before BCs** — rows/columns sum to zero; rigid-body motion is unrestrained, so `[K]` cannot be inverted until enough DOF are constrained.
- **Positive definite after sufficient BCs** — guaranteeing a unique, stable solution.
- **Diagonal terms are positive** — pushing a node in a direction requires a force in that direction.
- **Sparse and banded** — each node only couples to its immediate neighbors.

### 2.2 The 1-D bar (truss) element
A uniform elastic bar: length L, cross-sectional area A, Young's modulus E. Its axial stiffness is `k = A*E/L`, so:
`[k_e] = (A*E/L) * [ 1  -1 ; -1  1 ]`

For a **2-D truss element** oriented at angle theta, each node has 2 DOF (x, y). The local stiffness is transformed to global coordinates with the rotation/transformation matrix `[T]`:
`[k_global] = [T]^T [k_local] [T]`
With `c = cos(theta)`, `s = sin(theta)`, the 4x4 global element stiffness is:
`[k_e] = (A*E/L) * [ c^2  cs  -c^2  -cs ; cs  s^2  -cs  -s^2 ; -c^2  -cs  c^2  cs ; -cs  -s^2  cs  s^2 ]`

### 2.3 The DSM solution sequence
1. **Discretize** the structure into elements and number the nodes/DOF.
2. **Form each element stiffness matrix** `[k_e]` (in global coordinates).
3. **Assemble** into the global stiffness matrix `[K]` (Section 4).
4. **Build the global system** `[K]{U} = {F}`.
5. **Apply boundary conditions** (constraints and loads) — Section 5.
6. **Solve** the reduced system for the unknown nodal displacements `{U}`.
7. **Recover** reactions, element forces, stresses, strains (post-processing).

---

## 3. Shape (Interpolation) Functions

### 3.1 Concept
Within an element, the field variable is approximated as a linear combination of **shape functions** N_i weighted by the nodal values:
`u(x) = sum( N_i(x) * u_i )` — or in matrix form `u(x) = [N]{d}`, where {d} is the vector of nodal DOF.

### 3.2 Required properties of shape functions
- **Kronecker delta (interpolation) property:** `N_i = 1` at node i, and `N_i = 0` at every other node. This makes nodal DOF the actual field values at the nodes.
- **Partition of unity:** `sum(N_i) = 1` everywhere in the element — guarantees the element can represent a rigid-body (constant) field.
- **Completeness:** the shape functions must be able to represent constant strain (constant first derivatives) — required for convergence.
- **Compatibility (conformity):** the field is continuous across element boundaries (C^0 continuity for most structural elements; C^1 for beam/plate elements that need slope continuity).
- **Polynomial form** — chosen so the number of terms matches the number of nodal DOF.

### 3.3 The linear 1-D (2-node) bar element
With a natural coordinate `xi` running -1 to +1 across the element:
- `N_1 = (1 - xi)/2`
- `N_2 = (1 + xi)/2`
In physical coordinates (node 1 at x=0, node 2 at x=L):
- `N_1 = 1 - x/L`, `N_2 = x/L`

### 3.4 Quadratic 1-D (3-node) element
With nodes at xi = -1, 0, +1:
- `N_1 = xi*(xi - 1)/2`
- `N_2 = (1 - xi^2)`
- `N_3 = xi*(xi + 1)/2`
Quadratic shape functions can represent a linearly varying strain field within the element — more accurate per element, the basis of "higher-order" elements.

### 3.5 The strain-displacement matrix [B]
Strain is the derivative of displacement: `{epsilon} = [B]{d}`, where `[B]` contains the spatial derivatives of the shape functions. For the 2-node bar, `[B] = (1/L)[ -1  1 ]` (constant — hence "constant-strain" element).

### 3.6 The general element stiffness matrix (from the weak form)
For an elastic element:
`[k_e] = INT_over_volume( [B]^T [D] [B] ) dV`
- `[B]` = strain-displacement matrix (derivatives of shape functions).
- `[D]` = constitutive (material) matrix — relates stress to strain (Hooke's law in matrix form).
This single equation generates the stiffness matrix for *any* element type once `[N]`, `[B]`, and `[D]` are defined. For the bar it reduces to `(AE/L)[1 -1; -1 1]`.

### 3.7 Pitfalls
- Forgetting that shape functions must satisfy partition of unity and completeness — otherwise the element cannot converge.
- Confusing the natural coordinate xi (-1 to 1) with physical coordinate x.

---

## 4. Assembly of the Global Stiffness Matrix

### 4.1 The principle
The global stiffness matrix `[K]` is assembled by **superposition**: each element's stiffness terms are added into the global matrix at the rows/columns corresponding to that element's global DOF numbers. **Where elements share a node, their stiffness contributions to that node are summed.** This is the discrete statement of equilibrium and compatibility at every node.

### 4.2 The connectivity (element-to-global) map
Each element has a **connectivity array** mapping local node numbers (1, 2, ...) to global DOF numbers. Assembly walks every element, and for each pair of local DOF (i, j) adds `k_e[i][j]` into `K[global(i)][global(j)]`.

### 4.3 Worked-example pattern (3 springs in series, 4 nodes)
- Element 1 connects DOF 1-2, element 2 connects DOF 2-3, element 3 connects DOF 3-4.
- The global `[K]` is 4x4. Element 1 contributes to the (1,1),(1,2),(2,1),(2,2) block; element 2 to the (2,2),(2,3),(3,2),(3,3) block — note (2,2) receives contributions from **both** elements 1 and 2 and they add.
- Result: a **tridiagonal, symmetric, banded** global matrix.

### 4.4 Properties of the assembled global matrix
Symmetric, sparse, banded (bandwidth depends on node numbering — good numbering minimizes bandwidth and solve cost), and **singular until boundary conditions are applied** (it still permits rigid-body motion).

### 4.5 Pitfalls
- Mis-mapping local to global DOF — the single most common assembly bug.
- Forgetting to *add* (not overwrite) shared-node contributions.

---

## 5. Boundary Conditions

### 5.1 Two kinds
- **Essential (Dirichlet) BCs** — prescribed values of the *primary* variable: fixed/known displacements (supports), known temperatures. These make `[K]` non-singular and are *required* for a unique solution.
- **Natural (Neumann) BCs** — prescribed values of the *derivative* quantity: applied forces/tractions, prescribed heat flux. These enter through the load vector `{F}`. A traction-free surface is a "natural" do-nothing BC.

### 5.2 The constrained system
After assembly, `[K]{U} = {F}` is singular. Applying essential BCs removes the rigid-body modes:
- **Elimination (partitioning)** method — delete the rows/columns of constrained DOF, solve the reduced system for the free DOF, then back-substitute to recover reaction forces.
- **Penalty method** — add a very large stiffness on the diagonal of the constrained DOF, forcing it toward the prescribed value (simple, but conditioning-sensitive).
- **Lagrange multiplier** method — append constraint equations; exact, adds DOF, used for multipoint/contact constraints.

### 5.3 Loads
Concentrated nodal forces go directly into `{F}`. Distributed loads (pressure, body force, thermal load) are converted to **equivalent (consistent) nodal loads** by `{f_e} = INT([N]^T * traction) dS` — work-equivalent, not just "split the total in half."

### 5.4 Pitfalls
- **Under-constraining** — leaving rigid-body modes → singular `[K]`, solver fails or returns garbage/huge displacements.
- **Over-constraining** — adding artificial stiffness, suppressing real deformation, producing fictitious stresses.
- Applying a point load and then reading the (infinite, mesh-dependent) stress *at* that point — point-load stress singularities are not real.
- Lumping a distributed load as equal halves to the end nodes for higher-order elements — use consistent nodal loads.

---

## 6. The Weak (Variational) Formulation — Why It Works

### 6.1 Strong vs weak form
- **Strong form** — the governing PDE plus BCs, requiring high-order continuity of the exact solution.
- **Weak form** — multiply the PDE residual by a test/weight function, integrate over the domain, and integrate by parts. This **lowers the continuity requirement** on the trial solution (e.g. from C^1 to C^0) and naturally incorporates the natural BCs — exactly what makes simple polynomial shape functions usable.

### 6.2 Two routes to the same element equations
- **Principle of Minimum Potential Energy (variational)** — for structural problems, the true displacement field minimizes the total potential energy `Pi = U_strain - W_external`. Discretizing and setting `dPi/d{d} = 0` yields `[K]{d} = {F}`.
- **Method of Weighted Residuals (Galerkin)** — choose the weight functions equal to the shape functions; enforce that the weighted integral of the PDE residual vanishes. Galerkin's method gives the *same* `[K]{d}={F}` and applies to non-structural problems (heat, fluid) where no energy functional exists.

### 6.3 Why this matters
The weak form is the reason FEA is general: any field problem with a PDE can be cast in weak form and discretized with the same machinery. The Galerkin route is what extends FEA beyond structures.

---

## 7. Element Library

### 7.1 By dimensionality and DOF
| Element | Dim | Typical nodes | DOF/node | Use |
|---------|-----|---------------|----------|-----|
| Spring / bar (truss) | 1-D | 2 | 1–3 (translations) | Axial members, trusses |
| Beam / frame | 1-D | 2 | up to 6 (transl. + rotations) | Bending members, frames |
| CST (constant-strain triangle) | 2-D | 3 | 2 | Plane stress/strain — stiff, low accuracy |
| LST (linear-strain triangle) | 2-D | 6 | 2 | Better accuracy than CST |
| Quad4 (bilinear quadrilateral) | 2-D | 4 | 2 | Plane problems — good general-purpose |
| Quad8 / Quad9 (quadratic) | 2-D | 8–9 | 2 | Higher accuracy, curved edges |
| Tet4 (linear tetrahedron) | 3-D | 4 | 3 | Auto-meshable solids — overly stiff |
| Tet10 (quadratic tetrahedron) | 3-D | 10 | 3 | Standard for complex 3-D solids |
| Hex8 (linear brick) | 3-D | 8 | 3 | Accurate, efficient — needs structured mesh |
| Hex20 (quadratic brick) | 3-D | 20 | 3 | High accuracy 3-D |
| Shell / plate | 2-D in 3-D space | 3–8 | 5–6 | Thin-walled structures |

### 7.2 Linear vs higher-order (quadratic)
- **Linear elements** — straight/flat edges, constant strain (1-D bar, CST) or bilinear strain (Quad4). Cheap per element but need fine meshes; can be overly stiff (especially linear tets — "shear locking" / "volumetric locking").
- **Quadratic elements** — mid-side nodes, curved edges, linearly varying strain. Far more accurate per DOF, capture curved geometry and stress gradients well. Preferred for stress analysis.

### 7.3 Isoparametric formulation
Most modern elements are **isoparametric** — the *same* shape functions interpolate both the geometry and the field variable, mapping a distorted physical element to a regular "parent" element in natural coordinates (xi, eta, zeta). Integration is done numerically over the parent element by **Gauss (Gaussian) quadrature**, with the **Jacobian** `[J]` handling the coordinate mapping. A badly distorted element produces a near-singular Jacobian → inaccurate or failed integration.

### 7.4 Pitfalls
- Using linear tets for stress analysis — they lock and underpredict deflection; prefer quadratic tets or hex elements.
- Using truss elements where bending matters (truss elements carry no moment).
- Highly distorted/skewed elements (poor aspect ratio, large skew) — bad Jacobian, poor accuracy.

---

## 8. Meshing Best Practices

### 8.1 General guidelines
- **Refine where gradients are steep** — fillets, holes, notches, contact zones, load/support regions. Use a coarse mesh in low-gradient regions to save cost.
- **Element quality metrics** — aspect ratio (keep near 1, avoid > ~5–10), skew, taper, Jacobian, warpage. Most preprocessors report a quality histogram — check it.
- **Smooth transitions** — gradual size change between coarse and fine regions; avoid abrupt jumps that distort elements.
- **Mesh the physics, not just the geometry** — capture expected stress gradients and mode shapes.
- **Capture curved geometry** — use higher-order elements or enough linear elements so faceting error is acceptable.
- **Symmetry** — exploit geometric + load + BC symmetry to mesh only a fraction of the model (apply symmetry BCs on the cut planes). Saves enormous cost. (Caution: symmetry of geometry alone is not enough — loads and BCs must also be symmetric; never use it for buckling/modal where antisymmetric modes exist.)
- **Hex over tet** when geometry permits — hex meshes are more accurate and efficient per DOF.

### 8.2 Mesh controls
Global element size, local refinement/sizing, biased/graded meshing toward features, edge seeding, sweep/structured meshing for prismatic geometry, defeaturing (remove tiny fillets/holes irrelevant to the result — but never defeature a stress-critical feature).

### 8.3 Pitfalls
- One element through a bending thickness — cannot represent the bending strain gradient; use several through-thickness elements or shell elements.
- Failing to defeature irrelevant small geometry → huge element counts and tiny elements that throttle the solver.
- Defeaturing a feature that *is* the stress concentration of interest.

---

## 9. Convergence

### 9.1 What convergence means
As the mesh is refined, the FEA solution should approach the exact solution of the mathematical model. A **mesh convergence study** confirms the result is not an artifact of mesh density: refine, re-solve, compare a key quantity (peak stress, max deflection, natural frequency); when the change between successive refinements drops below an acceptance threshold (commonly ~2–5%), the mesh is **converged**.

### 9.2 Convergence behavior
- **Displacements** converge faster than **stresses** (stress is a derivative of displacement — one order less accurate). Always run the convergence study on the *quantity of interest*, usually stress.
- The **displacement-based FEM is generally stiffer than reality** — it tends to **underpredict displacement** and converges to the true value from below as the mesh is refined.

### 9.3 Refinement strategies
| Method | What changes | Notes |
|--------|--------------|-------|
| **h-refinement** | Reduce element *size* (subdivide elements; more, smaller elements) | Simple, universal; the most common approach |
| **p-refinement** | Increase the *polynomial order* of the elements (mesh unchanged) | For smooth problems the p-version's asymptotic convergence rate is at least twice the h-version's |
| **hp-refinement** | Combine both | Can give **exponential** convergence when h and p are refined in a suitable combination |
| **r-refinement** | *Relocate* nodes (adaptive node positioning) without adding DOF | Less common standalone |
- **Adaptive meshing** uses an a-posteriori **error estimator** to automatically refine only where local error is high.

### 9.4 Stress singularities — convergence's failure case
At re-entrant sharp corners, point loads, and point supports, the *mathematical* stress is **infinite**. The FEA stress there does **not converge** — it just keeps rising as you refine. This is a modeling artifact, not a physical result. Fixes: model a realistic fillet radius, use distributed loads/supports, or evaluate stress at a defined distance away from the singularity (e.g. structural stress / hot-spot methods).

### 9.5 Pitfalls
- Running a single mesh and trusting the number — without a convergence study you do not know the discretization error.
- Refining a model that contains a stress singularity and chasing a number that will never converge.
- Checking convergence on displacement when the design driver is stress.

---

## 10. Interpreting Results & Verification/Validation

### 10.1 Sanity checks (do these before believing any contour plot)
- **Deformed-shape check** — does it deflect the way physics says it should? Wrong deformed shape ⇒ wrong BCs/loads.
- **Reaction-force check** — do the reaction forces sum to the applied loads (global equilibrium)? If not, the model is wrong.
- **Order-of-magnitude / hand-calc check** — compare peak stress and max deflection to a simplified closed-form estimate.
- **Units consistency** — FEA solvers are unit-agnostic; the user must keep a consistent unit set (e.g. N, mm, MPa, tonne). A units error is the classic source of wildly wrong results.

### 10.2 Stress quantities
- **von Mises (equivalent) stress** — the standard ductile-failure criterion; compare to yield strength.
- **Principal stresses** — relevant for brittle materials and crack analysis.
- **Stress averaging** — solvers compute stress at integration (Gauss) points and extrapolate/average to nodes. Large differences between **averaged (nodal)** and **unaveraged (element)** stress at a location indicate the mesh is too coarse there — a built-in convergence indicator.

### 10.3 Verification vs Validation
- **Verification** — "are we solving the equations right?" (mesh convergence, comparison to analytical solutions, code checks). Math correctness.
- **Validation** — "are we solving the right equations?" (comparison to physical experiment). Model correctness.

### 10.4 Pitfalls
- Reading peak stress at a singularity and treating it as a real value.
- Trusting smooth contour plots — averaging hides element-to-element jumps; check unaveraged stress.
- Skipping the reaction-force equilibrium check.

---

## 11. Sources of Error in FEA

| Error type | Cause | Mitigation |
|------------|-------|------------|
| **Discretization error** | Mesh too coarse to capture the true field/gradients | Mesh convergence study; refine where gradients are high |
| **Geometry / faceting error** | Curved boundaries approximated by straight element edges | Higher-order elements; finer mesh on curves |
| **Element-formulation error** | Locking (shear/volumetric), hourglassing, poor element shapes | Use appropriate element types; reduced/selective integration with hourglass control; quality checks |
| **Numerical-integration error** | Insufficient Gauss points; distorted Jacobian | Adequate quadrature order; avoid distorted elements |
| **Round-off error** | Finite machine precision; ill-conditioned `[K]` | Good node numbering; scaled units; avoid huge stiffness ratios |
| **Boundary-condition / modeling error** | Wrong constraints, wrong load representation, wrong material model | Verify deformed shape & reactions; consistent nodal loads; validate material data |
| **User error** | Inconsistent units, mis-applied loads, wrong connectivity | Sanity checks, hand-calc comparison, peer review |

The **discretization error** is the only one a convergence study addresses — the rest are modeling decisions the analyst must get right.

---

## 12. The CAD/CAE Workflow

### 12.1 End-to-end process
1. **Define the problem** — physics (static structural, modal, thermal, nonlinear, dynamic, fatigue), objectives, required accuracy.
2. **CAD model / geometry prep** — build or import geometry; **defeature** (remove cosmetic fillets, logos, tiny holes irrelevant to the result); use **midsurfacing** for thin-walled parts (→ shell elements); exploit **symmetry**.
3. **Material definition** — assign properties (E, nu, density, yield; nonlinear or temperature-dependent data as needed).
4. **Meshing** — choose element type and size, set local refinement, check mesh quality.
5. **Boundary conditions & loads** — apply supports (essential BCs), forces/pressures/thermal loads (natural BCs), contacts, connections.
6. **Solve** — select the analysis type and solver (direct vs iterative); the solver factorizes/solves `[K]{U}={F}`.
7. **Post-process** — contour plots, deformed shapes, reaction forces, derived quantities.
8. **Verify & validate** — sanity checks, hand-calc comparison, mesh convergence study, comparison to test data.
9. **Iterate / optimize** — design changes, parametric studies, topology/shape optimization, then re-run.

### 12.2 Analysis types (typical course coverage)
- **Linear static** — small displacements, linear-elastic material, static loads; `[K]{U}={F}` solved once.
- **Modal / eigenvalue** — natural frequencies and mode shapes: `([K] - omega^2*[M]){phi} = 0` (M = mass matrix).
- **Buckling** — linear eigenvalue buckling: `([K] + lambda*[K_geometric]){phi} = 0`.
- **Thermal** — steady-state or transient conduction; the "stiffness" matrix becomes the conductance matrix.
- **Nonlinear** — geometric nonlinearity (large deflection), material nonlinearity (plasticity), contact; solved iteratively (Newton-Raphson).
- **Dynamic / transient** — time integration of `[M]{U_ddot} + [C]{U_dot} + [K]{U} = {F(t)}`.

### 12.3 Pitfalls
- Meshing the as-designed CAD model with all cosmetic detail — explodes element count.
- Importing geometry with gaps/slivers from CAD translation — meshing fails or produces bad elements.
- Choosing the wrong analysis type for the physics (e.g. linear static when large deflection or contact dominates).

---

## Quick-Reference Equation Sheet

| Quantity | Equation |
|----------|----------|
| Global system | [K]{U} = {F} |
| Spring/bar element stiffness | [k_e] = (AE/L)[1 -1; -1 1] |
| Bar axial stiffness | k = AE/L |
| 2-D truss transform | [k_global] = [T]^T [k_local] [T] |
| Field interpolation | u(x) = [N]{d} |
| Linear bar shape functions | N_1 = 1 - x/L, N_2 = x/L |
| Natural-coord linear shapes | N_1 = (1-xi)/2, N_2 = (1+xi)/2 |
| Partition of unity | sum(N_i) = 1 |
| Strain-displacement | {epsilon} = [B]{d} |
| Bar [B] matrix | [B] = (1/L)[-1 1] |
| General element stiffness | [k_e] = INT([B]^T [D] [B]) dV |
| Consistent nodal loads | {f_e} = INT([N]^T * traction) dS |
| Min. potential energy | Pi = U_strain - W_ext ; dPi/d{d} = 0 |
| Modal eigenproblem | ([K] - omega^2 [M]){phi} = 0 |
| Buckling eigenproblem | ([K] + lambda [K_g]){phi} = 0 |
| Transient dynamics | [M]{U_ddot} + [C]{U_dot} + [K]{U} = {F(t)} |

---

## Open-source sources used

- **Felippa, C. A., *Introduction to Finite Element Methods* (IFEM)** — University of Colorado Boulder, freely available online (Direct Stiffness Method chapters 1–11; variational/element formulation chapters 12–19; shape functions, isoparametric elements, Gauss quadrature). Hosted at quickfem.com, vulcanhammer.net, and the author's course pages. https://quickfem.com/wp-content/uploads/IFEM.Ch00.pdf and https://vulcanhammer.net/wp-content/uploads/2017/01/ifem.pdf
- **Roylance, D., *Finite Element Analysis* module** — MIT OpenCourseWare 3.11 Mechanics of Materials. https://web.mit.edu/course/3/3.11/www/modules/fea.pdf
- **Nikishkov, G. P., *Introduction to the Finite Element Method*** — open lecture notes (IITG hosting). https://www.iitg.ac.in/mech/documents/128/introfem.pdf
- **IISc Mechanical Engineering open FEM notes** — Ananthasuresh "Shape Functions" (Ch. 4) and C. S. Jog "Introduction to the Finite Element Method." https://mecheng.iisc.ac.in/suresh/me237/feaNotes/Chapter4.pdf
- **DoITPoMS, University of Cambridge — "The Finite Element Method" TLP** (direct stiffness method, global stiffness matrix assembly). https://www.doitpoms.ac.uk/tlplib/fem/stiffness.php
- **MIT OpenCourseWare 2.092 / 16.810 — finite element analysis courses** (solution procedure, element types, convergence, meshing). https://ocw.mit.edu/
- **University of Victoria MECH 410 — "Introduction to FEA" lecture notes** (FEA theory and workflow). https://www.engr.uvic.ca/~mech410/lectures/FEA_Theory.pdf
- Wikipedia "Finite element method," "hp-FEM," "p-FEM" — for the characterization of FEM ingredients and h-/p-/hp-refinement convergence rates (cross-checked against the open textbooks above).
