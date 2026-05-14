# Manufacturing Engineering Reference

PhD-level study companion for ME 3701 — Manufacturing Engineering.
Covers casting, bulk & sheet forming/forging, machining (turning, milling, drilling — cutting mechanics, tool life/Taylor's equation), joining & welding, powder metallurgy, additive manufacturing, metrology & GD&T, and process selection.

Math is in plain text: `x^2` = x squared, `sqrt(x)` = square root, subscripts inline (v_c).

---

## 1. Overview & Process Classification

### 1.1 The five major process families
| Family | Principle | Examples |
|--------|-----------|----------|
| **Casting / molding** | Liquid → solid in a mold cavity | Sand, investment, die, permanent-mold casting; injection molding |
| **Forming / deformation** | Plastic deformation of a solid; conserves mass | Forging, rolling, extrusion, drawing, sheet stamping, bending |
| **Material removal (machining)** | Remove material as chips/particles | Turning, milling, drilling, grinding, EDM, laser |
| **Joining** | Combine parts | Welding, brazing, soldering, adhesive bonding, fastening |
| **Additive / powder** | Build up material | Powder metallurgy, additive manufacturing (3D printing) |

### 1.2 Process-selection drivers
Geometry & complexity; size; material; tolerance & surface finish required; production volume (lot size); cost (tooling vs per-part); lead time; mechanical-property requirements; sustainability. Casting and forming favor high volume (high tooling cost amortized); machining favors low-to-medium volume and tight tolerances; AM favors complexity and very low volume / prototypes.

### 1.3 Cost model intuition
`Cost_per_part = (Fixed tooling cost / N) + Variable cost_per_part`
- High-volume processes (die casting, injection molding, stamping) have **high fixed**, **low variable** cost.
- Low-volume processes (sand casting, machining from stock, AM) have **low fixed**, **high variable** cost.
- The crossover volume determines the economic process choice.

---

## 2. Casting

### 2.1 Fundamentals
Pour molten metal into a mold cavity, solidify, remove. Capable of complex internal/external geometry and large parts; near-net-shape; wide alloy range. Limitations: porosity, dimensional accuracy, surface finish, generally lower mechanical properties than wrought (forged) parts.

### 2.2 Solidification physics
- **Pure metal** — solidifies at a single temperature; planar solidification front; a central shrinkage pipe.
- **Alloy** — solidifies over a freezing range (between liquidus and solidus); mushy zone; dendritic growth; microsegregation (coring).
- **Three shrinkage stages:** liquid contraction, solidification shrinkage, solid (thermal) contraction. The pattern is made oversized by a **shrinkage allowance** (pattern-maker's rule) to compensate.
- **Chvorinov's rule** — total solidification time:
  `t_s = B * (V / A)^n` with `n ≈ 2`, B = mold constant.
  - V/A = casting volume-to-surface-area ratio (the "modulus").
  - Design consequence: **risers (feeders) must solidify last**, so a riser is designed with a *larger* V/A than the casting section it feeds.
- **Directional solidification** — control cooling so solidification sweeps toward the riser, keeping a liquid path open to feed shrinkage.

### 2.3 Gating system & fluid flow
- **Gating system:** pouring cup → sprue → runner → gate → cavity; plus risers and vents.
- **Continuity:** `Q = A1*v1 = A2*v2`.
- **Bernoulli / Torricelli** — velocity at sprue base from pouring height h: `v = sqrt(2*g*h)`.
- Sprue is **tapered** (smaller at base) to keep the stream full and avoid aspiration of air.
- **Fluidity** — ability of melt to fill thin sections; improves with superheat, favorable composition (eutectics flow well), and mold conditions.

### 2.4 Casting processes

| Process | Mold | Pattern reuse | Tolerance/finish | Notes |
|---------|------|---------------|-----------------|-------|
| **Sand casting** | Expendable sand | Reusable pattern | Poor | Cheapest, any size/metal, low volume |
| **Investment (lost-wax)** | Expendable ceramic shell | Expendable wax pattern | Excellent | Fine detail, high-melting alloys, expensive |
| **Die casting** | Permanent steel die | — | Very good | High pressure, high volume, low-melt alloys (Al, Zn, Mg) |
| **Permanent-mold (gravity)** | Permanent metal mold | — | Good | Better properties than sand; nonferrous |
| **Centrifugal** | Rotating mold | — | Good | Pipes, cylinders; impurities driven inward |
| **Shell molding** | Resin-bonded sand shell | Reusable metal pattern | Good | Better finish/accuracy than green sand |

### 2.5 Casting defects
Porosity (gas — from dissolved gas/turbulence; shrinkage — from inadequate feeding); misruns and cold shuts (insufficient fluidity/temperature); inclusions and slag; hot tears (tensile stress during solidification at constrained sections); shrinkage cavities/pipes; segregation; sand defects (blows, scabs, penetration).

### 2.6 Pitfalls
- Forgetting that **the riser must solidify after the section it feeds** — getting V/A backwards starves the casting.
- Treating pure-metal and alloy solidification the same (single temperature vs freezing range).
- Ignoring directional solidification when placing risers/chills.

---

## 3. Bulk Deformation: Forming & Forging

### 3.1 Fundamentals of metal forming
- Plastic deformation, **mass and (approximately) volume conserved**: `A0*L0 = A1*L1`.
- **Flow stress** — instantaneous stress required to continue plastic deformation: `sigma_f = K * eps^n` (K = strength coefficient, n = strain-hardening exponent, eps = true strain).
- **Average flow stress** over a process: `sigma_f_avg = K * eps^n / (1 + n)`.
- **Cold working** (below recrystallization temp) — better finish/tolerance, strain hardening raises strength, but higher forces and limited ductility.
- **Hot working** (above recrystallization temp) — lower forces, large deformations, no strain hardening (dynamic recrystallization), but oxidation/scale, poorer tolerance.
- **Warm working** — intermediate compromise.

### 3.2 Forging
- Compressive shaping between dies. Produces favorable, continuous grain flow → superior fatigue/impact properties vs casting or machining.
- **Open-die forging** (upsetting) — simple dies, large parts, low volume. Ideal upsetting force: `F = sigma_f * A`; with friction, a **friction multiplier (forging shape factor)** `K_f = 1 + (0.4*mu*D)/h` raises the required force as the billet becomes squat (D/h large).
- **Impression-die (closed-die) forging** — die cavity shapes the part; **flash** forms at the parting line and is trimmed; force `F = K_f * sigma_f_avg * A` with empirical K_f (3–12 depending on complexity).
- **Flashless (precision) forging** — net-shape, no flash; demands precise billet volume.

### 3.3 Rolling
- Thickness reduction between rotating rolls.
- **Draft:** `d = t_0 - t_f`; **maximum draft** limited by friction: `d_max = mu^2 * R` (R = roll radius).
- **Contact length** `L = sqrt(R*d)`; rolling force `F = sigma_f_avg * w * L` (w = strip width).
- Flat rolling (plate, sheet), shape rolling (I-beams, rails), ring rolling, thread rolling.

### 3.4 Extrusion
- Force material through a die opening.
- **Direct (forward) extrusion** — ram and product move the same direction; billet slides against the container wall (high friction).
- **Indirect (backward) extrusion** — die moves into the billet; no billet-container relative motion (lower friction, more uniform).
- **Extrusion ratio** `r_x = A0/A_f`; ideal pressure `p = sigma_f_avg * ln(r_x)`; real pressure includes friction/redundant-work terms (Johnson equation: `eps_x = a + b*ln(r_x)`).

### 3.5 Wire / bar / tube drawing
- Pull stock through a converging die to reduce cross-section.
- **Reduction** `r = (A0 - A_f)/A0`; draw stress `sigma_d = sigma_f_avg * ln(A0/A_f)` (ideal). The draw stress **must stay below the yield strength of the exit material** or the wire necks/breaks — this caps reduction per pass (~ 0.3–0.5).

### 3.6 Sheet-metal forming
- **Shearing / blanking / punching** — shearing force `F = 0.7 * UTS * t * L` (t = sheet thickness, L = sheared perimeter); clearance set as a % of thickness.
- **Bending** — bend allowance `BA = 2*pi*(A/360)*(R + K_ba*t)`, K_ba ≈ 0.33–0.5 (neutral-axis position factor). **Springback** — elastic recovery; the bend angle opens up. Compensated by overbending or bottoming.
- **Deep drawing** — form a cup from a blank; **limiting drawing ratio (LDR)** = D_blank/D_punch ≈ 2.0 max; failure modes: tearing (excessive draw) and wrinkling (insufficient blank-holder force).
- **Formability** measured by tensile n and **r-value (plastic strain ratio)**; visualized with the **forming limit diagram (FLD)**.

### 3.7 Pitfalls
- Forgetting volume constancy when relating before/after dimensions.
- Ignoring springback in bending — designed angle ≠ formed angle.
- Confusing direct vs indirect extrusion friction behavior.

---

## 4. Machining (Material Removal)

### 4.1 Mechanics of chip formation — the orthogonal cutting model
- The workpiece is sheared along a **shear plane** at the **shear angle phi**.
- **Chip thickness ratio:** `r = t_0 / t_c` (t_0 = undeformed chip thickness/feed, t_c = deformed chip thickness). Always `r < 1` because the chip is thicker than the uncut layer.
- **Shear angle:** `tan(phi) = (r*cos(alpha)) / (1 - r*sin(alpha))` — alpha = tool rake angle.
- **Shear strain:** `gamma = cot(phi) + tan(phi - alpha)`.
- **Merchant's equation** (minimum-energy shear angle): `phi = 45 + alpha/2 - beta/2` — beta = friction angle, `tan(beta) = mu`. Predicts that increasing rake angle or decreasing friction *raises* phi → thinner chip, lower cutting force.

### 4.2 Cutting forces & power
- **Cutting force F_c** (along cutting velocity) and **thrust force F_t** (perpendicular). Resultant R.
- **Specific cutting energy / specific energy** `u = F_c / (w * t_0)` = F_c*v / MRR — energy per unit volume removed; depends mostly on the work material.
- **Material removal rate (MRR):**
  - Turning: `MRR = v * f * d` (v = cutting speed, f = feed/rev, d = depth of cut).
  - Milling: `MRR = w * d * f_r` (w = width, d = depth, f_r = table feed rate).
- **Cutting power:** `P_c = F_c * v`; **motor power** `P_m = P_c / efficiency`.
- Most of the cutting energy converts to heat — partitioned among chip (most), tool, and workpiece. Heat governs tool wear.

### 4.3 Chip types
- **Continuous** — ductile material, high speed, sharp tool, large rake: good finish but can tangle.
- **Built-up edge (BUE)** — work material welds to the tool tip at low speed; unstable, degrades finish; reduced by higher speed, coatings, coolant.
- **Discontinuous (segmented)** — brittle material or low rake/low speed.
- **Serrated** — semi-continuous, from difficult-to-machine alloys (Ti, Ni superalloys).

### 4.4 Tool wear & tool life — Taylor's equation
- **Wear modes:** flank wear (abrasion, on the relief face — the standard life criterion), crater wear (diffusion/adhesion on the rake face), notch wear, chipping, thermal cracking.
- **Taylor's tool-life equation:**
  `V * T^n = C`
  - V = cutting speed, T = tool life (minutes), n = Taylor exponent (material/tool dependent), C = constant = the cutting speed giving 1-minute tool life.
  - Typical n: HSS ≈ 0.1–0.15, carbide ≈ 0.2–0.3, ceramic ≈ 0.4–0.6. Higher n → tool life less sensitive to speed.
- **Extended (generalized) Taylor equation:** `V * T^n * f^a * d^b = C` — adds feed and depth-of-cut dependence (speed has the strongest effect on life, then feed, then depth).
- **Worked-example pattern:** given two (V, T) data pairs, solve `V1*T1^n = V2*T2^n` for n by taking logs; then compute C; then predict T at any V (or the V for a target T). For economic optimization, find the speed minimizing cost or maximizing production rate by balancing machining time against tool-change cost.

### 4.5 Tool materials (in order of increasing hardness/hot-hardness, decreasing toughness)
High-carbon/HSS → cast cobalt alloys → cemented carbides (WC-Co) → coated carbides (TiN, TiC, Al2O3 coatings) → cermets → ceramics (Al2O3, Si3N4) → CBN (cubic boron nitride) → polycrystalline diamond (PCD). Selection trades hot-hardness/wear resistance against toughness and cost.

### 4.6 Tool geometry
- **Rake angle** — positive reduces cutting force and improves finish but weakens the edge; negative strengthens the edge (good for interrupted cuts, hard materials).
- **Relief (clearance) angle** — prevents the flank rubbing the workpiece.
- Tool signature (ASA system) specifies back rake, side rake, end/side relief, end/side cutting-edge angles, and nose radius.

### 4.7 Surface finish
- Ideal roughness in turning (no BUE): `R_a ≈ f^2 / (32 * r_n)` — f = feed, r_n = nose radius.
- **Larger nose radius and smaller feed → better finish.** BUE, vibration/chatter, and tool wear degrade finish in practice.

### 4.8 Specific operations
- **Turning** — workpiece rotates, single-point tool; cylindrical features. `Cutting speed v = pi*D*N` (N = spindle speed); machining time `T_m = L / (f*N)`.
- **Milling** — rotating multi-tooth cutter, workpiece feeds.
  - **Up (conventional) milling** — chip starts thin, ends thick; tends to lift the work, more rubbing.
  - **Down (climb) milling** — chip starts thick; better finish, less tool wear, but needs a backlash-free machine.
  - Feed per tooth `f_t`, table feed `f_r = f_t * n_t * N` (n_t = number of teeth).
- **Drilling** — rotating two-flute drill, axial feed; `T_m = (L + allowance) / (f*N)`; the chisel edge does no cutting (mostly extrusion) — pre-drilling a pilot hole reduces thrust.
- **Grinding** — abrasive process; very fine finish and tight tolerance; high specific energy (small chip thickness, negative effective rake); wheel specified by abrasive type, grit size, grade, structure, bond.
- **Nontraditional:** EDM (electrical-discharge erosion — any conductive material, hard materials, complex cavities, no cutting force), ECM, laser/plasma/water-jet cutting, ultrasonic machining, chemical milling.

### 4.9 Pitfalls
- Inverting the chip-thickness ratio (r is always < 1; the chip is thicker than the cut).
- Forgetting to take logs to solve Taylor's equation for n.
- Confusing cutting speed (surface speed, m/min) with spindle speed (rev/min).
- Mixing up up-milling and down-milling chip-load behavior.

---

## 5. Joining & Welding

### 5.1 Classification
- **Fusion welding** — melt the base metal (with/without filler): arc welding (SMAW, GMAW/MIG, GTAW/TIG, SAW, FCAW), oxyfuel gas welding, resistance welding (spot, seam — uses I^2*R Joule heating), electron-beam, laser-beam welding.
- **Solid-state welding** — no melting of base metal: friction welding, friction-stir welding, ultrasonic, diffusion bonding, explosion welding, forge welding.
- **Brazing** (filler T > 450 °C) and **soldering** (filler T < 450 °C) — only the *filler* melts; joint by capillary action; base metal unmelted.
- **Adhesive bonding** and **mechanical fastening** (bolts, rivets, screws).

### 5.2 Weld physics
- **Heat input per unit length:** `H = (eta * V * I) / v` — eta = process efficiency, V = arc voltage, I = current, v = travel speed. Higher heat input → larger weld pool and heat-affected zone.
- **Weld zones:** fusion zone (melted + solidified, cast structure) → **heat-affected zone (HAZ)** (not melted but microstructurally altered — often the weakest/most-problematic region, e.g. grain coarsening or untempered martensite in steels) → unaffected base metal.
- **Weldability** depends on composition — **carbon equivalent (CE):** `CE = %C + %Mn/6 + (%Cr+%Mo+%V)/5 + (%Ni+%Cu)/15`. CE > ~0.4 → preheat and controlled cooling needed to avoid HAZ cracking.

### 5.3 Weld defects
Porosity (trapped gas — shielding loss, contamination); slag inclusions; incomplete fusion / incomplete penetration; undercut; cracks (hot/solidification cracks; cold/hydrogen-induced cracks in the HAZ); residual stresses and distortion (from non-uniform thermal contraction — managed by fixturing, preheat, peening, post-weld heat treatment, balanced welding sequence).

### 5.4 Pitfalls
- Treating the fusion zone as the weak link — it is usually the **HAZ**.
- Ignoring preheat requirements for high-carbon-equivalent steels.
- Forgetting that brazing/soldering do not melt the base metal.

---

## 6. Powder Metallurgy (PM)

### 6.1 Process sequence
1. **Powder production** — atomization, reduction, electrolysis, mechanical comminution.
2. **Blending/mixing** — powders + lubricant + alloying additions.
3. **Compaction** — pressed in a die (50–800 MPa) into a fragile **green compact**; density is non-uniform (die-wall friction).
4. **Sintering** — heat below the melting point of the major constituent; solid-state diffusion bonds particles, reduces porosity, increases strength. Driven by reduction of surface energy.
5. **Secondary operations** — sizing/coining, impregnation (oil-impregnated bearings), infiltration, machining, heat treatment, HIP (hot isostatic pressing).

### 6.2 Characteristics
- Excellent for: high-melting/refractory metals (W, Mo), tungsten carbide, porous parts (self-lubricating bearings, filters), tight composition control, high-volume small parts (gears, cams).
- Near-net-shape, minimal scrap, good dimensional control.
- Limitations: residual porosity lowers strength/ductility/toughness vs wrought; high tooling cost (volume-driven); size limited by press capacity; powder cost and handling (some powders pyrophoric).

### 6.3 Pitfalls
- Assuming PM parts match wrought properties — residual porosity is the limiting factor unless fully densified (HIP).
- Forgetting that compaction density is non-uniform because of die-wall friction.

---

## 7. Additive Manufacturing (AM / 3D Printing)

### 7.1 The seven ASTM/ISO process categories
| Category | Mechanism | Examples / materials |
|----------|-----------|----------------------|
| **Vat photopolymerization** | UV-cured liquid resin | SLA, DLP — photopolymers |
| **Material extrusion** | Extruded molten filament | FDM/FFF — thermoplastics |
| **Powder bed fusion** | Laser/electron beam fuses a powder bed | SLS (polymer), SLM/DMLS, EBM (metals) |
| **Binder jetting** | Liquid binder onto a powder bed | Metals, sand, ceramics |
| **Material jetting** | Droplets of material jetted & cured | Polymers, waxes |
| **Directed energy deposition (DED)** | Melt material as it is deposited | Metal repair, large parts |
| **Sheet lamination** | Bond and cut sheets | LOM — paper, metal, composite |

### 7.2 Workflow
CAD model → tessellate to STL/3MF → slice into layers + generate support structures and toolpaths → build layer-by-layer → remove supports, post-process (cure, debind/sinter, heat treat, machine critical surfaces, surface finish).

### 7.3 Advantages & limitations
- **Advantages:** geometric freedom (internal channels, lattices, topology-optimized parts), no part-specific tooling, mass customization, rapid prototyping, part consolidation, low-volume economy.
- **Limitations:** anisotropy (layer-direction-dependent properties — the build direction is usually weakest), surface roughness (stair-stepping), slow build rate, build-volume limits, residual stress/warping in metal PBF, qualification/repeatability challenges, support removal, material cost.

### 7.4 Pitfalls
- Designing without accounting for build-direction anisotropy and support access.
- Assuming AM is always cheaper — it wins at low volume and high complexity, not at high volume.

---

## 8. Metrology, Tolerancing & GD&T

### 8.1 Measurement fundamentals
- **Accuracy** (closeness to true value) vs **precision** (repeatability/scatter) — independent properties.
- **Resolution** — smallest increment an instrument can display.
- Instruments: steel rule, vernier/dial/digital caliper, micrometer (finer than caliper), dial indicator, gauge blocks (length standards), gauge pins, sine bar (angles), surface plate, optical comparator, **coordinate-measuring machine (CMM)**, surface profilometer (R_a).
- **The 10:1 (gauge-maker's) rule** — measuring instrument resolution should be ~1/10 of the tolerance being checked.

### 8.2 Conventional (limit) tolerancing
- **Tolerance** = total permissible variation = (upper limit − lower limit).
- **Bilateral** (±) vs **unilateral** (one-sided) tolerances.
- **Fits** between mating parts: **clearance fit** (always a gap), **interference (press) fit** (always overlap), **transition fit** (could be either).
- **Allowance** = the *intentional* difference between mating parts = tightest possible fit (minimum clearance, or maximum interference).
- **Tolerance stack-up** — accumulation of individual tolerances along a dimension chain; worst-case (arithmetic sum) vs statistical (RSS) analysis.

### 8.3 Geometric Dimensioning & Tolerancing (GD&T) — ASME Y14.5
GD&T defines tolerance *zones* for geometric characteristics and ties them to **datums**, communicating design intent far more precisely than coordinate tolerancing alone. It allows **bonus tolerance** under material-condition modifiers, increasing manufacturing yield without sacrificing function.

#### The 14 GD&T symbols
| Symbol | Name | Category | Datum required? | MMC/LMC allowed? |
|--------|------|----------|-----------------|------------------|
| ⏤ | Straightness | Form | No | Yes (on a feature of size) |
| ⏥ | Flatness | Form | No | No |
| ○ | Circularity (roundness) | Form | No | No |
| ⌭ | Cylindricity | Form | No | No |
| ⌒ | Profile of a line | Profile | Sometimes | No |
| ⌓ | Profile of a surface | Profile | Sometimes | No |
| ∠ | Angularity | Orientation | Yes | Yes |
| ⊥ | Perpendicularity | Orientation | Yes | Yes |
| ∥ | Parallelism | Orientation | Yes | Yes |
| ⌖ | Position (true position) | Location | Usually | Yes |
| ◎ | Concentricity (deprecated in Y14.5-2018) | Location | Yes | No |
| ⌯ | Symmetry (deprecated in Y14.5-2018) | Location | Yes | No |
| ↗ | Circular runout | Runout | Yes | No |
| ⌰ | Total runout | Runout | Yes | No |

- **Form** controls (4) — never reference a datum (a feature's form is relative to itself).
- **Orientation** controls (3) — always reference a datum (define an angular relationship).
- **Runout** controls (2) — always reference a datum axis; runout combines form + orientation + location error as seen on a rotating part.
- **Profile** (2) — the most versatile; can control size, form, orientation, and location of a surface against datums.
- **Location** (3) — Position is the workhorse; Concentricity/Symmetry are deprecated in favor of Position or Profile.

#### Material-condition modifiers
| Modifier | Symbol | Meaning |
|----------|--------|---------|
| Maximum Material Condition | Ⓜ (MMC) | Feature contains the most material (largest pin / smallest hole). Allows **bonus tolerance** as the feature departs from MMC. |
| Least Material Condition | Ⓛ (LMC) | Feature contains the least material (smallest pin / largest hole). |
| Regardless of Feature Size | (RFS) | Default in Y14.5-2009+; tolerance is fixed, no bonus, regardless of actual size. |
| Projected Tolerance Zone | Ⓟ | Tolerance zone projected above the surface (for threaded/press-fit holes — controls the mating part's protrusion). |
| Free State | Ⓕ | Applies to non-rigid parts in their unrestrained state. |
| Tangent Plane | Ⓣ | Tolerance applies to a plane tangent to the high points of the surface. |

- **Bonus tolerance** = |actual feature size − MMC size|. Added to the stated geometric tolerance when Ⓜ is invoked — rewards parts made away from worst-case material.
- **Virtual condition** = the worst-case boundary a feature can violate = MMC ± geometric tolerance (sign depends on internal/external feature). Used for functional gauging and fit analysis.

#### The feature control frame (read left to right)
`[ geometric symbol | tolerance zone shape (⌀ if cylindrical) + tolerance value + material modifier | primary datum + modifier | secondary datum | tertiary datum ]`
- The leader/arrow points to the controlled feature (surface → controls the surface; on a size dimension → controls the axis/centerplane).
- **Datum Reference Frame (DRF)** — three mutually perpendicular datum planes establishing a coordinate system; datums are called out **primary, secondary, tertiary** (constrain 3, then 2, then 1 degrees of freedom — the **3-2-1 rule** of part location).
- Datum features are labeled with a **datum feature symbol** (a letter in a box with a triangle).

### 8.4 Surface finish
- **R_a** (arithmetic average roughness) is the most common parameter; also R_q (RMS), R_z.
- Specified with a surface-texture symbol indicating R_a value, lay direction, machining allowance, and process if required.

### 8.5 Pitfalls
- Putting a datum reference on a form control — form tolerances never use datums.
- Forgetting bonus tolerance when MMC is specified (under-using available tolerance, or failing a good part).
- Confusing **allowance** (intentional, the tightest fit) with **tolerance** (permitted variation).
- Mis-ordering datums in the feature control frame — order = precedence, not alphabetical.

---

## 9. Process Selection & Design for Manufacturing (DFM)

### 9.1 Selection logic
1. **Material** narrows the field (e.g. high-melting refractory → PM or specialized casting; thermoplastic → injection molding).
2. **Geometry** — complexity, internal features, thin walls, undercuts.
3. **Size** — press/mold/build-volume limits.
4. **Tolerance & finish** — machining/grinding for tight tolerances; casting/forming for looser.
5. **Volume** — drives the fixed-vs-variable cost trade-off (see §1.3).
6. **Properties** — forging for fatigue-critical parts; casting for complex non-critical shapes; AM for low-volume complexity.

### 9.2 DFM guidelines (general)
- Minimize part count (consolidate).
- Use standard features, tooling, and stock sizes.
- Design for the chosen process: uniform wall thickness and generous fillets/draft for casting and molding; avoid deep narrow pockets and sharp internal corners for machining; design for accessible support removal in AM; avoid tight tolerances unless functionally required (cost rises sharply).
- Specify the **loosest tolerance** and **roughest finish** that still works — both drive cost nonlinearly.

### 9.3 Pitfalls
- Over-specifying tolerance/finish "to be safe" — directly inflates cost.
- Selecting a process on geometry alone and ignoring the volume/cost crossover.

---

## Quick-Reference Equation Sheet

| Quantity | Equation |
|----------|----------|
| Chvorinov's rule | t_s = B*(V/A)^n, n ≈ 2 |
| Continuity | Q = A1*v1 = A2*v2 |
| Sprue velocity | v = sqrt(2*g*h) |
| Flow stress | sigma_f = K*eps^n |
| Avg flow stress | sigma_f_avg = K*eps^n/(1+n) |
| Volume constancy | A0*L0 = A1*L1 |
| Max rolling draft | d_max = mu^2*R |
| Rolling contact length | L = sqrt(R*d) |
| Extrusion pressure (ideal) | p = sigma_f_avg*ln(A0/A_f) |
| Drawing stress (ideal) | sigma_d = sigma_f_avg*ln(A0/A_f) |
| Shearing force | F = 0.7*UTS*t*L |
| Chip thickness ratio | r = t_0/t_c (< 1) |
| Shear angle | tan(phi) = r*cos(alpha)/(1 - r*sin(alpha)) |
| Merchant's equation | phi = 45 + alpha/2 - beta/2 |
| Shear strain (cutting) | gamma = cot(phi) + tan(phi - alpha) |
| Specific cutting energy | u = F_c/(w*t_0) |
| MRR (turning) | MRR = v*f*d |
| Cutting power | P_c = F_c*v |
| Cutting speed | v = pi*D*N |
| Machining time (turning) | T_m = L/(f*N) |
| Taylor tool life | V*T^n = C |
| Extended Taylor | V*T^n*f^a*d^b = C |
| Turning surface roughness | R_a ≈ f^2/(32*r_n) |
| Weld heat input | H = eta*V*I/v |
| Carbon equivalent | CE = %C + %Mn/6 + (%Cr+%Mo+%V)/5 + (%Ni+%Cu)/15 |
| Bonus tolerance | bonus = |actual size − MMC size| |
| Virtual condition | VC = MMC ± geometric tolerance |

---

## Open-source sources used

- **OpenLearn, The Open University — "Manufacturing"** free course (casting, forming, machining and cutting mechanics, tool materials, joining/welding). https://www.open.edu/openlearn/science-maths-technology/design-innovation/manufacturing/content-section-0
- **"Manufacturing Processes and Materials: Exercises"** — open educational resource (casting, forming, machining, joining fundamentals and worked exercises). Open-textbook / OER repositories.
- **Open courseware lecture material on machining fundamentals** (orthogonal cutting, Merchant's model, Taylor tool-life equation) from public university repositories aligned with Kalpakjian/Groover texts.
- **GD&T Basics — GD&T Symbols reference guide** (the 14 ASME Y14.5 symbols, feature control frame, datums, material-condition modifiers). https://www.gdandtbasics.com/gdt-symbols/
- **Tec-Ease GD&T free resource glossary** (GD&T terms, datum reference frame, modifiers). https://www.tec-ease.com/gdt-symbols-terms.php
- **MIT OpenCourseWare 2.810 — Manufacturing Processes and Systems** (process physics, process selection, DFM). https://ocw.mit.edu/courses/2-810-manufacturing-processes-and-systems-fall-2004/
