# NCEES FE Reference Handbook — Alignment Guide

Maps the skill's references to the actual FE Reference Handbook structure, so the skill solves exam problems with the notation and formula forms the exam expects.

This file is a transformative study/index document. It is **not** a copy of the Handbook. The Handbook itself is copyrighted by NCEES; you must download your own copy from your MyNCEES account. This guide tells you where things live, what notation the Handbook uses, what tables are provided, and what is conspicuously absent.

---

## Handbook Edition Cited

Edition **10.0.1**, Copyright 2020 by NCEES (ISBN 978-1-947801-11-0). 471-page main body plus index and exam specifications. NCEES periodically revises; the live PDF in the exam room may be a later minor revision (e.g., 10.x). Structure and notation have been stable across recent minor versions; revisions tend to add or correct individual equations rather than reorganize sections. Verify the current edition at https://account.ncees.org before sitting the exam.

The Handbook is the **only** reference allowed during the FE exam. There is one Handbook used across all FE disciplines; there is not a separate "FE Mechanical edition." The discipline-specific sections (Chemical, Civil, Environmental, Electrical & Computer, Industrial & Systems, Mechanical) sit at the back; everything before them is shared.

---

## 1. Handbook Structure Map

Section order in the 10.0.1 Handbook, with the page where each section begins, what it covers, and which file in this skill's `references/` directory maps to it.

| # | Handbook Section | Starts pg. | Mapped skill file(s) |
|---|------------------|-----------|----------------------|
| 1 | Units and Conversion Factors | 1 | `formula-reference.md` (general); used by every solver |
| 2 | Ethics and Professional Practice | 4 | `ethics-and-professional-practice.md` |
| 3 | Safety | 13 | (no dedicated file — overlaps `materials-science.md`, `chemistry.md`) |
| 4 | Mathematics | 34 | `calculus.md`, `differential-equations.md`, `numerical-methods.md` |
| 5 | Engineering Probability and Statistics | 63 | `probability-statistics.md` |
| 6 | Chemistry and Biology | 85 | `chemistry.md` |
| 7 | Materials Science / Structure of Matter | 94 | `materials-science.md` |
| 8 | Statics | 107 | `statics.md` |
| 9 | Dynamics | 114 | `dynamics.md`, `machine-kinematics.md`, `vibrations.md` |
| 10 | Mechanics of Materials | 130 | `strength-of-materials.md` |
| 11 | Thermodynamics | 143 | `thermodynamics.md` |
| 12 | Fluid Mechanics | 177 | `fluid-mechanics.md` |
| 13 | Heat Transfer | 204 | `heat-transfer.md` |
| 14 | Instrumentation, Measurement, and Control | 220 | `controls.md` (plus measurement portions used in design problems) |
| 15 | Engineering Economics | 230 | `engineering-economics.md` |
| 16 | Chemical Engineering | 238 | (not relevant for FE Mechanical) |
| 17 | Civil Engineering | 259 | (not relevant for FE Mechanical) |
| 18 | Environmental Engineering | 310 | (not relevant for FE Mechanical) |
| 19 | Electrical and Computer Engineering | 355 | `physics-em.md`, `circuits.md` (FE Mechanical uses a subset only) |
| 20 | Industrial and Systems Engineering | 417 | (not relevant for FE Mechanical) |
| 21 | **Mechanical Engineering** | 431 | `machine-design.md`, `manufacturing.md`, `engineering-graphics.md`, parts of `vibrations.md` |
| — | Index | 461 | — |
| — | FE Exam Specifications | 471 | (see Section 8 of this guide) |

Sections 16, 17, 18, 20 exist for other disciplines and will not be drawn from on a Mechanical exam. Section 19 (Electrical/Computer) is large but the Mechanical exam only pulls from its first few pages — DC/AC fundamentals, Kirchhoff/Ohm, basic motors/generators. The discipline-specific Mechanical section (21) is the dense one: ~30 pages of pure machine-design formulas with no narrative.

Files in this skill not mapped to a single Handbook section (`physics-mechanics.md`, `cae-fea.md`, `worked-examples-*.md`) are pedagogical scaffolding — they cover background the Handbook assumes you already know, or worked solutions the Handbook explicitly omits.

---

## 2. Notation Cheat Sheet

The Handbook has specific conventions. The skill should adopt these so the student is reading the same symbols on the exam as in their answers.

### Force/mass in USCS
- Handbook uses both **SI** and **USCS** in parallel; many formulas state both forms or the conversion.
- **`gc = 32.174 lbm·ft/(lbf·sec²)`** is the force-unit conversion factor in USCS. Distinct from the local gravity `g`. Handbook writes Newton's law as `F = ma/gc`, kinetic energy `KE = mv²/(2gc)`, fluid pressure `p = ρgh/gc`, shear stress `τ = (μ/gc)(dv/dy)`.
- When solving in SI, drop `gc`; it's `1` and dimensionless effectively. When solving in USCS with pounds-mass and pounds-force in the same expression, **carry `gc` explicitly**.

### Thermodynamics
- **`k` (not γ)** is the specific heat ratio: `k = cp/cv`. The Handbook never uses gamma.
- Lowercase `cp, cv` are mass-basis specific heats `[kJ/(kg·K)]` or `[Btu/(lbm·°R)]`.
- Uppercase `Cp, Cv` are molar-basis specific heats `[kJ/(kmol·K)]`.
- `R̄` (R-bar) is the **universal** gas constant. `R` (no bar) is the **specific** gas constant `R = R̄/M`.
- State properties use `T, P, v, u, h, s`. Subscripts: `f` saturated liquid, `g` saturated vapor, `fg` difference (vapor − liquid). E.g., `hfg = hg − hf` is enthalpy of vaporization.
- Quality: `x = mvapor/mtotal`, used as `h = hf + x·hfg`.

### Fluid mechanics
- Reynolds number written `Re = ρVD/μ = VD/ν` (NOT `NRe`).
- Friction factor: Handbook uses the **Darcy friction factor `f`** (sometimes written `fD`) — not the Fanning factor. Head loss: `hf = f·(L/D)·V²/(2g)`. If the student is used to Fanning (`fF = fD/4`), warn them.
- Pump/fan power: `Ẇ = ρ·g·Q·h / η` (SI). `γ = ρg` (specific weight) is sometimes carried separately.
- Bernoulli with units of head: `P/(ρg) + V²/(2g) + z = const`.

### Mechanics of materials
- Normal stress `σ`, shear stress `τ`. Strain `ε` (normal), `γ` (shear).
- Modulus `E` (Young's), `G` (shear), bulk `K`. Poisson `ν`.
- Section modulus `S = I/c`. Bending stress `σ = Mc/I = M/S`.
- Mohr's circle: Handbook plots **shear positive downward on the right face**, opposite of the convention some textbooks use. Result is the same; rotation direction matches physical rotation. Note this when reading Handbook Mohr diagrams.

### Dynamics & vibrations
- `ω` is angular velocity (rad/s). `ωn` is natural frequency (rad/s). `f` (no subscript) reserved for cyclic frequency `f = ω/(2π)` [Hz].
- Damping ratio `ζ` (zeta). Damped natural frequency `ωd = ωn·√(1−ζ²)`.
- Mass-normalized stiffness: `ωn = √(k/m)`.

### Statics
- Resultant force `R`, moment `M`. Centroid `(x̄, ȳ)`. Second moment of area `I` (the Handbook may also call this "moment of inertia of area" — same thing).
- Friction: `μs` static, `μk` kinetic. Impending motion: `F = μs·N`.

### Machine design (Section 21)
- Spring rate `k`. Spring index `C = D/d` (mean coil dia / wire dia). Wahl/Bergstr factor `Ks = (2C+1)/(2C)` for shear correction in helical springs.
- Bearings: basic load rating `C`, design load `P`, life `L` in millions of revolutions, exponent `a = 3` (ball), `a = 10/3` (roller).
- Bolt preload `Fi`, stiffness ratio `C = kb/(kb+km)`, proof strength `Sp`.

### Controls
- Transfer function in `s` (Laplace). The Handbook uses standard block-diagram form `Y(s)/R(s) = G(s)/(1+G(s)H(s))`.
- PID form: `Gc(s) = Kc·[1 + 1/(TI·s) + TD·s]` — `TI`, `TD` are time constants (seconds), not gains. Watch for this; some textbooks use `Ki = Kc/TI` and `Kd = Kc·TD` as separate gains.

### Probability & statistics
- Mean `μ` or `X̄`. Std deviation: `σ` (population), `s` (sample). Variance is the square.
- Coefficient of variation `CV = s/X̄`.
- Confidence interval uses `z` for known σ, `t` (with `n−1` dof) for unknown σ.

### Engineering economics
- Cash-flow factor notation: `(F/P, i, n)`, `(P/A, i, n)`, etc. The slash reads "given the second, find the first." `(P/F, i, n)` = present worth given future amount.

---

## 3. Equation Locator

Most-tested equations, where they live in the Handbook, and how the Handbook formats them.

| Equation | Handbook section | Notes / Handbook form |
|----------|-----------------|----------------------|
| **Bernoulli (energy form)** | Fluid Mechanics, around the Principles of One-Dimensional Fluid Flow subsection | Written as heads: `P/γ + V²/(2g) + z = const`. Energy line and hydraulic grade line are defined next to it. |
| **First law, open system (control volume)** | Thermodynamics, "First Law of Thermodynamics" | `Q̇ − Ẇ = Σmout(h + V²/2 + gz)out − Σmin(...)in + dE/dt`. Steady-state forms drop the `dE/dt`. |
| **First law, closed system** | Thermodynamics | `Q − W = ΔU` (per unit mass: `q − w = Δu`). |
| **Reynolds number** | Fluid Mechanics | `Re = ρVD/μ`. For non-circular conduit, hydraulic diameter `Dh = 4A/P`. |
| **Darcy-Weisbach head loss** | Fluid Mechanics | `hf = f·(L/D)·V²/(2g)`. Moody diagram is provided (use it; do not guess `f`). |
| **LMTD (heat exchanger)** | Heat Transfer | `q = U·A·F·ΔTlm`. `ΔTlm = (ΔT1 − ΔT2)/ln(ΔT1/ΔT2)`. F-factor charts for shell-and-tube provided in Heat Transfer section. |
| **NTU-effectiveness** | Heat Transfer | `q = ε·Cmin·(Th,in − Tc,in)`. ε-NTU equations and charts for parallel, counter, cross flow given. |
| **Conduction (Fourier)** | Heat Transfer | `q̇ = −kA·dT/dx`. Steady, plane wall: `q = kAΔT/L`. Thermal resistance series/parallel network described. |
| **Convection (Newton's law)** | Heat Transfer | `q = hA·ΔT`. |
| **Radiation** | Heat Transfer | `q = εσA(T1⁴ − T2⁴)`, Stefan-Boltzmann `σ = 5.67×10⁻⁸ W/(m²·K⁴)` listed in fundamental constants (pg. 2). |
| **Mohr's circle (2D stress)** | Mechanics of Materials | Center at `(σx+σy)/2`, radius `R = √[((σx−σy)/2)² + τxy²]`. Principal stresses `σ1,2 = center ± R`. Max in-plane shear = R. |
| **Beam deflection formulas** | Mechanics of Materials | Tables for cantilever and simply supported beams with point load, UDL, moment. Memorize `δmax = PL³/(48EI)` for simply supported center load and `δmax = PL³/(3EI)` for cantilever tip; rest are in the table. |
| **Euler column buckling** | Mechanics of Materials, "Columns" subsection | `Pcr = π²EI/(K·L)²`. Effective length factors: K = 0.5 (fixed-fixed), 0.7 (fixed-pinned), 1.0 (pinned-pinned), 2.0 (fixed-free). |
| **Carnot efficiency** | Thermodynamics, Second Law | `η = 1 − TL/TH` (absolute temperatures). |
| **Carnot COP (refrigerator)** | Thermodynamics | `COPref = TL/(TH−TL)`. Heat pump: `COPhp = TH/(TH−TL) = COPref + 1`. |
| **Ideal gas law** | Thermodynamics | `Pv = RT` (specific), `PV = nR̄T` (molar). Polytropic: `Pvⁿ = const`. |
| **Isentropic relations** | Thermodynamics | `T2/T1 = (P2/P1)^((k−1)/k) = (v1/v2)^(k−1)`. Uses `k`, not γ. |
| **Marin endurance modifiers** | **NOT in the Handbook** | This is the major gotcha. The Handbook gives basic fatigue concepts (endurance limit definition, S-N concept, Basquin) but **does not list the full Marin surface/size/load/temperature/reliability factor tables**. If a problem asks for a Marin-corrected endurance limit, expect either the factors to be provided in the question or to be tested on the concept only. See section 6 below. |
| **Helical spring stress/deflection** | Mechanical Engineering (Sec 21), "Springs" | `τ = Ks·8FD/(πd³)`, `k = d⁴G/(8D³N)`. `Ks = (2C+1)/(2C)` where `C = D/d`. |
| **Bearing life** | Mechanical Engineering, "Bearings" | `C = P·L^(1/a)` where `L` is in millions of revolutions, `a = 3` ball, `a = 10/3` roller. |
| **Bolted joint** | Mechanical Engineering | Stiffness ratio `C = kb/(kb+km)`. Bolt load factor `nb = (Sp·At − Fi)/(C·P)`. Tightening torque `T ≈ 0.2·Fi·d` (steel on steel). |
| **PV factors (econ)** | Engineering Economics | All in factor tables for `i = 0.5%, 1, 1.5, 2, 4, 6, 8, 10, 12, 18%`. Use the table, do not compute from formulas during the exam. |
| **Capacitor / inductor impedance** | Electrical & Computer Engineering | `ZC = 1/(jωC)`, `ZL = jωL`. Use phasor form. |
| **Vibration (undamped 1-DOF)** | Dynamics or Mechanical Engineering Vibrations subsection | `ωn = √(k/m)`. Damped: `ωd = ωn·√(1−ζ²)`. Critical damping `cc = 2√(km)`. |
| **Transfer function, 1st order** | Instrumentation, Measurement, and Control | `G(s) = K/(τs+1)`. Time constant `τ`, settling time ≈ `4τ`. |
| **Transfer function, 2nd order** | Same | `G(s) = ωn²/(s² + 2ζωn·s + ωn²)`. Overshoot, settling time formulas listed. |
| **Continuity** | Fluid Mechanics | `ρ1A1V1 = ρ2A2V2`. Incompressible: `A1V1 = A2V2`. |
| **Drag force** | Fluid Mechanics, "Consequences of Fluid Flow" | `FD = CD·ρV²A/2`. CD curves vs. Re for sphere, cylinder, flat plate provided. |

When solving an exam problem, **state the Handbook section** you're pulling from in the reasoning. Example: *"From the Handbook Heat Transfer section, LMTD form: ΔTlm = (ΔT1 − ΔT2)/ln(ΔT1/ΔT2)."* This matches the discipline the exam expects.

---

## 4. Tables in the Handbook

These tables are **available to you on exam day**. Do not memorize their contents; know where they are and how to read them.

### Units & Conversion (front matter)
- Metric prefixes (atto through exa).
- Common equivalents (weight of water per gallon/ft³/in³, etc.).
- Temperature conversion formulas (°F↔°C, °R, K).
- Fundamental constants: e, F (Faraday), R̄ (in 4 unit systems), G, g (SI & USCS), molar volume of ideal gas, c, Stefan-Boltzmann σ.
- **Long multiply/divide conversion table** — 4+ pages of factor conversions for every common unit. Searchable by either column.

### Mathematics
- Laplace transform pairs table.
- Common Fourier and z-transform pairs.
- Standard derivative and integral table (selected).
- Trig identities (sum, double-angle, product, etc.).
- Cylindrical and spherical coordinate transformations.

### Probability & Statistics
- Standard normal distribution table (z-table).
- Student's t distribution values (selected).
- F distribution selected values.
- Chi-square selected values.
- Common probability density functions and their means/variances.

### Chemistry & Biology
- **Periodic table** (full).
- Standard electrode potentials (selected).
- Activity series of metals.

### Materials Science
- Properties of metals table (density, melting point, specific heat, thermal/electrical conductivity for a few dozen metals).
- ASTM/SAE alloy designations referenced.
- Phase diagrams: iron-carbon (full), several binary alloy diagrams.
- Stress-strain comparison curves for common materials.

### Statics
- Centroid and moment of inertia formulas for standard shapes (rectangle, triangle, circle, semicircle, quarter circle, etc.) — both `Ix` (centroidal) and parallel axis form.
- Friction coefficient table (typical static and kinetic μ for common material pairs).

### Dynamics
- Mass moment of inertia for standard solids (rod, disk, sphere, cylinder, thin shell).
- Standard kinematics constants (gravity, etc., from front matter).

### Mechanics of Materials
- Beam deflection and slope formulas for cantilever and simply supported beams under standard loadings.
- Stress concentration factor charts for selected geometries (shaft with fillet, plate with hole, etc.).
- Column effective length K factors.

### Thermodynamics
- **Saturated water table** (by temperature and by pressure) — `vf, vg, hf, hg, hfg, sf, sg, sfg, uf, ug`.
- **Superheated steam table**.
- **Compressed liquid water table** (sparse — usually use saturated liquid at same T as approximation).
- **R-134a tables**: saturated and superheated, plus P-h diagram.
- **R-410A tables**: saturated and superheated, plus P-h diagram.
- **Ideal gas table** for air (T, h, Pr, u, vr, s°) — used for variable-specific-heat air problems.
- Specific heats `cp, cv, k` at room temperature for common gases (air, N2, O2, CO2, He, H2O vapor, Ar).
- **Psychrometric chart** (SI and US units versions).
- Heats of formation for common compounds.

### Fluid Mechanics
- **Moody diagram** (friction factor vs. Re, ε/D).
- Loss coefficients K for fittings (elbow, tee, valve, contraction, expansion).
- Drag coefficients CD vs. Re for sphere, smooth cylinder, flat plate.
- Pipe roughness ε for steel, cast iron, concrete, drawn tubing, etc.
- Water properties (ρ, μ, ν, σ, Pv) vs. temperature.
- Air properties (ρ, μ, ν, cp, k) vs. temperature.

### Heat Transfer
- Thermal conductivity table for common materials.
- Nusselt-number correlations (with their applicable Re ranges and Pr conditions) for flat plate, cylinder, sphere, internal pipe flow, natural convection.
- LMTD correction-factor charts F for shell-and-tube and cross-flow heat exchangers.
- Effectiveness-NTU charts for parallel, counter, cross-flow.
- Emissivity values for selected surfaces.
- View factor diagrams for standard geometries (parallel rectangles, perpendicular, concentric cylinders).

### Instrumentation, Measurement, Control
- RTD α coefficient and tolerance class table.
- Thermocouple type vs. temperature range.
- Strain gauge bridge configurations.
- Common transfer-function block diagrams.

### Engineering Economics
- **Compound interest factor tables** for `i = 0.5, 1, 1.5, 2, 4, 6, 8, 10, 12, 18%`, each showing `(F/P)`, `(P/F)`, `(F/A)`, `(A/F)`, `(P/A)`, `(A/P)` for `n = 1` to large `n`. **Use these tables on exam day. Do not compute from `(1+i)^n` formulas.**

### Mechanical Engineering (Sec 21)
- Spring material constants `A` and `m` for the tensile-strength relation `Sut = A/d^m` (music wire, oil-tempered, hard-drawn, chrome-vanadium, chrome-silicon).
- Compression spring end-condition geometry table (plain, plain+ground, squared, squared+ground).
- Bolted joint member stiffness coefficients `A, b` for steel, aluminum, copper, gray cast iron.
- Standard fits and tolerances (limits & fits table — basic deviations, IT grade applicability).
- Selected GD&T symbol references.

---

## 5. The "Use What's There" Discipline

Rules for how the skill should operate on exam-style problems:

1. **Identify the Handbook section first.** Before deriving anything, name the section the problem lives in (e.g., "this is a Heat Transfer / LMTD problem"). State it in the reasoning. This forces the right formula form.

2. **Prefer the Handbook's form of an equation.** If the Handbook writes the Carnot efficiency as `η = 1 − TL/TH`, use that exact form. Do not rewrite it as `η = (TH − TL)/TH` unless the algebra demands it; the grader's mental model is the Handbook form.

3. **Prefer Handbook table values over memorized constants.** Air `cp = 1.005 kJ/(kg·K)` if the Handbook table says so; do not use `cp = 1.0` from a textbook rule-of-thumb. Water `ρ = 1000 kg/m³` at 4°C is the standard but the Handbook gives `ρ(T)` curves; use the curve value if the problem specifies temperature.

4. **For pipe flow, look up the friction factor on the Moody diagram.** Do not compute the Colebrook equation iteratively — the Moody chart is provided for a reason.

5. **For econ, use the factor tables.** Look up `(P/A, 8%, 10)` directly. Don't compute `[(1.08)^10 − 1]/[0.08·(1.08)^10]` longhand.

6. **For thermo state lookups, use steam/refrigerant tables.** If `T = 100°C, x = 0.5`, look up `hf, hfg` from the saturated water table, then `h = hf + 0.5·hfg`. Do not approximate.

7. **Cite the Handbook section in the answer's reasoning when relevant.** Example output style:
   > Section: Thermodynamics → First Law, Open System (Handbook pg. ~143–150). Assume steady-state, single-inlet, single-exit, adiabatic, neglect KE/PE. Energy balance simplifies to `Ẇ = ṁ(h1 − h2)`. From the Handbook superheated steam table at P1, T1: `h1 = ...`. Quality at exit gives `h2 = hf + x·hfg = ...`.

8. **Carry units through every step.** The Handbook always shows units in brackets next to the symbol; match that. `[kg/s]`, `[kJ/(kg·K)]`, `[W/(m²·K)]`.

9. **Sanity-check against Handbook table extremes.** If your computed value of friction factor is `f = 0.0001`, the Moody diagram floor is around `f = 0.008` for smooth pipes at very high Re — you made an arithmetic error.

---

## 6. What the Handbook Does NOT Contain

Critical for calibration. Students often expect content here that simply isn't.

### Universally absent
- **Worked examples.** No solved problems anywhere. The Handbook is formulas, tables, and charts only.
- **Derivations or proofs.** It tells you `q = h·A·ΔT` without explaining why.
- **Conceptual narrative.** No "intuition" paragraphs. No "physically, this means..." commentary.
- **Step-by-step solution procedures.** No flowcharts for "how to solve a beam problem." You bring the procedure; the Handbook supplies the formulas.
- **Glossary or term definitions** (except a handful in Ethics and Safety). Concepts like "factor of safety," "endurance limit," "strain hardening" are referenced but not defined.

### Subject-specific gaps (FE Mechanical relevance)

**Mechanical design / fatigue:**
- **No Marin factor tables.** Surface finish factor `ka`, size factor `kb`, load factor `kc`, temperature factor `kd`, reliability factor `ke`, miscellaneous factor `kf` — none of these are tabulated. The Handbook acknowledges fatigue and the endurance limit concept (around pg. 5893 in 10.0.1, in the Materials section) but stops short of the modifier framework that Shigley's textbook uses. If an exam problem requires a Marin-modified endurance limit, the modifiers will be given in the problem statement.
- **No Goodman/Soderberg/Gerber diagrams as graphs.** The fatigue criterion equations may be present in concept; the visual diagram and worked region-of-failure is not.
- **No detailed gear stress (Lewis/AGMA) tables.** Spur gear basics (geometry, ratio, contact force) are in the ME section; full bending and contact stress analysis is not.
- **No detailed weld throat tables.** Welding is mentioned as a joining method; specific allowable stresses and electrode strengths come from the problem.

**Manufacturing:**
- No machinability data. No specific cutting speeds, feeds, or tool-life Taylor equation constants beyond the equation form.
- No detailed process selection charts.

**Materials:**
- Iron-carbon diagram is present; **TTT and CCT diagrams are not** in detail (concept and a sample diagram may appear, but not tables of transformation rates).
- No detailed heat-treatment hardenability (Jominy) tables.

**Thermodynamics:**
- **No combustion tables.** The Handbook gives stoichiometric combustion equations and heats of formation for selected fuels; it does not give complete fuel property tables. Air/fuel ratios are computed from the basic chemistry, not looked up.
- No detailed psychrometric process equations beyond the chart. Mixing of two streams, cooling/dehumidification, etc., are read off the chart.

**Heat transfer:**
- **No comprehensive Nu correlation reference.** A handful of standard correlations are given (Dittus-Boelter for turbulent internal flow, Churchill for natural convection cylinder, etc.); obscure geometries or transitional-flow correlations may not be there.
- No detailed insulation thickness optimization tables.

**Controls:**
- **No Bode, Nyquist, or root-locus construction recipes.** The transfer-function definitions and standard 1st/2nd-order forms are given; how to draw a Bode plot from scratch is not. The exam tests this conceptually rather than by full graph construction.
- **No Routh-Hurwitz table walkthrough** (the criterion is named; how to fill the table is on the student).
- No Ziegler-Nichols tuning rules.

**Math:**
- **No comprehensive integral table.** Selected common integrals are given (~1 page). Anything exotic is on the student.
- No Bessel functions or special-function tables.

**Vibrations:**
- **No mode-shape diagrams** beyond the 1-DOF case. Multi-DOF systems are referenced; modal-analysis numeric examples are absent.

If a problem appears to need content that isn't in the Handbook, **one of two things is true**: (a) the missing data will be supplied in the problem stem, or (b) the problem is testing a concept-level question that doesn't require the missing data. Don't panic if the table you wanted isn't there.

---

## 7. Section-by-Section Brief (Mechanical-Relevant Sections)

### 7.1 Mathematics (pg. 34)
**What's in it:** algebra and trig identities, analytic geometry (straight line, conics, distance formulas), differential calculus (derivative rules, partials, gradient), integral calculus (selected integrals, integration by parts, partial fractions setup), single ODE solution patterns (1st-order linear, 2nd-order constant-coefficient), Laplace transform pairs, linear algebra (matrix ops, determinants, eigenvalues), vector calculus (div, grad, curl), numerical methods (Newton's, trapezoidal, Simpson's, Euler), Taylor series, Fourier series form. Discrete math basics (sets, logic).
**What's not in it:** detailed integral table, special functions, deep numerical-method error analysis, full ODE solution catalog.
**Common exam patterns:** apply a Laplace pair to solve an ODE; identify the form of a series; compute a derivative or definite integral; solve a small matrix system; find eigenvalues of a 2x2 or 3x3.
**Gotchas:** the Handbook uses `s` for the Laplace variable (standard). Inverse-Laplace problems require pattern-matching against the table — practice this. Watch for ODE problems where the "Laplace" approach is faster than direct integration.

### 7.2 Probability and Statistics (pg. 63)
**What's in it:** common distributions (normal, binomial, Poisson, exponential, uniform) with PDF, mean, variance; combinatorics; expected value; confidence intervals (both σ-known z and σ-unknown t); linear regression with R²; ANOVA basics; control chart formulas (`±3σ`); reliability basics (`R(t) = e^(−λt)` for constant hazard).
**What's not in it:** Bayesian analysis, design of experiments details, time-series forecasting.
**Common exam patterns:** look up a z-value, compute a confidence interval, identify which distribution applies, compute mean/variance from data, regression slope and R².
**Gotchas:** the Handbook uses `X̄` and `s` (sample); `μ` and `σ` (population). Don't mix. For confidence intervals with `n < 30` and σ unknown, use t (not z).

### 7.3 Statics (pg. 107)
**What's in it:** force resultants and components in 2D/3D; equilibrium equations (`ΣF = 0`, `ΣM = 0`); centroids by integration and composite-section formulas; second moments of area `Ix, Iy` and parallel-axis theorem; friction (`F ≤ μs·N`, impending motion); truss analysis (method of joints, method of sections); frames (multi-force members).
**What's not in it:** elaborate cable-and-pulley arrangements, 3D-truss solution algorithms, detailed friction-on-belt derivations (the `T1/T2 = e^(μθ)` belt-friction formula is given but not extensively).
**Common exam patterns:** find reactions on a beam; find force in a specific truss member by sections; locate the centroid of a composite shape; determine whether a block on an incline slips or tips first.
**Gotchas:** Sign conventions are stated in the figures; follow them. The Handbook's truss diagrams show pin and roller supports clearly — match the reaction directions to the actual support type.

### 7.4 Dynamics (pg. 114)
**What's in it:** particle kinematics (rectilinear, projectile, polar); kinetics with `F = ma` and `M = Iα`; work-energy theorem; conservative forces and PE; impulse-momentum (linear and angular); restitution coefficient for impact; rigid-body kinematics (instantaneous center, rolling without slipping); rigid-body kinetics; mass moment of inertia table.
**What's not in it:** Lagrangian or Hamiltonian mechanics; orbital mechanics; detailed gyroscope analysis.
**Common exam patterns:** projectile range/time/height; spring-mass collision with restitution; rolling-disk acceleration on incline; angular velocity of a four-bar linkage; impulse of a finite force over a time interval.
**Gotchas:** distinguish `g` (gravity, 9.81 m/s² or 32.2 ft/s²) from `gc` (USCS conversion factor). Rotational analogs: `KE_rot = ½·I·ω²`, parallel-axis `I = Icm + m·d²`.

### 7.5 Mechanics of Materials (pg. 130)
**What's in it:** axial stress/strain; thermal strain `ε = α·ΔT`; torsion of circular shafts (`τ = Tc/J`, `θ = TL/(JG)`); bending (`σ = Mc/I`); transverse shear (`τ = VQ/(Ib)`); combined loading; pressure vessels (thin-wall `σ_hoop = Pr/t`, `σ_axial = Pr/(2t)`; thick-wall Lamé); beam deflection table; Mohr's circle (2D); Euler buckling; statically indeterminate basics.
**What's not in it:** energy methods (Castigliano's theorem) in detail; plasticity; fracture mechanics K-factors in depth.
**Common exam patterns:** combined axial + bending stress on a shaft; Mohr's circle for principal stresses; beam deflection at a point from the table; column buckling with end-condition factor; thin-wall pressure vessel stresses.
**Gotchas:** `J = πd⁴/32` for solid circular shaft (not `πd⁴/64` — that's `I`). Shear in beams is `VQ/(Ib)`, where `Q` is the first moment of the area outside the cut. For Mohr's circle, watch the sign convention on the Handbook diagram.

### 7.6 Thermodynamics (pg. 143)
**What's in it:** state postulate; closed and open system first law; second law (Kelvin-Planck, Clausius); entropy balance; Carnot efficiency and COP; ideal gas relations (`Pv=RT`, polytropic, isentropic); ideal gas mixtures (Dalton, Amagat); Rankine, Otto, Diesel, Brayton, refrigeration cycles; psychrometrics (chart provided); combustion stoichiometry; full steam, R-134a, R-410a, air ideal-gas tables.
**What's not in it:** detailed exergy analysis; advanced cycles (regeneration, reheat are shown but extensive cycle variants are not); detailed combustion adiabatic-flame-temperature procedure tables.
**Common exam patterns:** find state property from steam table given two others; compute Rankine cycle efficiency; quality at turbine exit; refrigerant COP; isentropic compression work; psychrometric process (cooling, humidifying, mixing).
**Gotchas:** `k = cp/cv`, NOT γ. For isentropic of ideal gas use relations with `k`, or use `Pr/vr` from the air table for variable-specific-heat. For wet steam, `h = hf + x·hfg`; if entropy is the constraint, use `s = sf + x·sfg` to find `x` first, then `h`. Closed vs. open system first law signs (work out vs. in) — check the Handbook's sign convention every time.

### 7.7 Fluid Mechanics (pg. 177)
**What's in it:** fluid statics (manometer, hydrostatic force on a plane and curved surface, buoyancy); Bernoulli and energy equations; continuity; Reynolds number; Moody diagram; minor losses with K-factors; pipe-network basics; momentum equation (forces on pipe bends, jet impingement); pumps (basic, NPSH); pump and fan affinity laws; dimensional analysis (Buckingham Pi); drag and lift; basic compressible flow (Mach number, stagnation, normal shock).
**What's not in it:** boundary-layer differential equations; turbulence modeling; detailed compressible flow with friction (Fanno/Rayleigh) — only the basics.
**Common exam patterns:** find head loss in a pipe; find pump power; manometer reading; force on a pipe bend; identify flow regime; compute drag on a sphere; affinity-law scaling of a pump.
**Gotchas:** Darcy friction factor `f`, NOT Fanning `fF`. They differ by factor of 4. Watch units in head-loss equation (head in meters of fluid, not pressure). For pumps in series vs. parallel: series adds head, parallel adds flow.

### 7.8 Heat Transfer (pg. 204)
**What's in it:** Fourier conduction; thermal resistance circuits (plane wall, cylinder, sphere); fins (efficiency, effectiveness); transient lumped capacitance (Biot number test); Heisler charts conceptually; Newton's law of cooling; convection correlations (Dittus-Boelter, Sieder-Tate, Churchill-Chu, flat plate); radiation (Stefan-Boltzmann, view factors for standard geometries, gray-surface enclosure); heat exchangers (LMTD with F-factor charts, ε-NTU charts).
**What's not in it:** boundary-layer integral methods in depth; multimode radiation with absorbing media; detailed boiling/condensation correlations beyond the basics.
**Common exam patterns:** thermal resistance through a composite wall; convection coefficient from a correlation; fin temperature distribution or efficiency; sizing a heat exchanger (LMTD); effectiveness of a counter-flow HX given NTU; radiation between two surfaces.
**Gotchas:** for the LMTD method, the correction factor `F` is only needed for shell-and-tube or cross-flow (`F = 1` for pure counter or pure parallel). When in doubt about a correlation's applicability range (Re or Pr), check the Handbook's stated range — using a correlation outside its valid range is a common trap.

### 7.9 Instrumentation, Measurement, and Control (pg. 220)
**What's in it:** RTD, thermocouple, thermistor relations; strain gauges (gauge factor, Wheatstone bridge); pressure transducer types; flow measurement (orifice, Venturi, pitot); accuracy/precision/uncertainty propagation; signal conditioning basics; transfer functions; block-diagram algebra; 1st-order and 2nd-order system response; PID controller form; closed-loop characteristic equation.
**What's not in it:** detailed Bode, Nyquist, or root-locus plotting; full state-space methods; digital control / z-transform applications.
**Common exam patterns:** identify time constant of a 1st-order response; classify a 2nd-order system as underdamped/overdamped; reduce a block diagram to a single transfer function; identify PID gains from a controller equation; compute uncertainty propagation from individual component uncertainties.
**Gotchas:** PID is given as `Gc = Kc[1 + 1/(TI·s) + TD·s]`. `TI` is reset time (seconds), not integral gain — divide `Kc/TI` to get integral gain in the alternative form.

### 7.10 Engineering Economics (pg. 230)
**What's in it:** simple and compound interest; equivalence (P/F, F/P, P/A, A/P, F/A, A/F factors); arithmetic and geometric gradient factors; rate-of-return concept; net present worth, equivalent annual worth; benefit-cost ratio; payback period; break-even analysis; depreciation (straight-line, MACRS table); inflation.
**Tables:** factor tables at 0.5%, 1, 1.5, 2, 4, 6, 8, 10, 12, 18%.
**What's not in it:** Monte Carlo, real-options, sensitivity-analysis methodology (concepts mentioned but no procedures).
**Common exam patterns:** compute PW of an alternative; find equivalent annual cost; choose between two alternatives by NPW; rate of return on a project; depreciation schedule by MACRS for a given recovery period.
**Gotchas:** when the exam interest rate is not on a factor-table page, you have to interpolate or compute from the factor formula. The factor formulas are listed at the start of the section — know `(P/A) = [(1+i)^n − 1]/[i(1+i)^n]` as a backup.

### 7.11 Mechanical Engineering (pg. 431) — discipline-specific
**What's in it:** springs (helical compression, torsion, leaf — stress and rate equations); bearings (ball/roller life equation with the `a` exponent, equivalent radial load); power screws (raise/lower torque, efficiency, self-locking criterion); shafts (combined stress, simple design equations); flat belts and V-belts (basic geometry, slip); clutches and brakes (uniform pressure vs. uniform wear); bolted joints (stiffness ratio, preload, fatigue loading, tightening torque); welded joints (basic shear-throat sizing concept); press/shrink fits (Lamé-based interface pressure); limits and fits (definitions of basic size, deviation, tolerance, IT grade); GD&T symbols; manufacturability basics; quality and reliability (sample size, AQL idea); mechanism kinematics review (four-bar, slider-crank).
**What's not in it:** AGMA gear stress equations in full; Marin endurance modifier tables (see Section 6 above); detailed cam-profile equations; comprehensive welding-electrode property tables.
**Common exam patterns:** spring deflection given F, D, d, N; bearing life or required basic load rating; bolt preload and the resulting separation factor; power screw raising torque and efficiency; press-fit interface pressure or transmissible torque; recognize a GD&T symbol.
**Gotchas:** The Handbook's spring rate `k = d⁴G/(8D³N)` is for the **active coil count** `N`, not total coils. Bearing exponent `a = 3` for ball, `a = 10/3` for roller — easy to swap. For power screw, the **lead** is the axial distance per revolution (single-start: lead = pitch; multi-start: lead = n·pitch).

### 7.12 Electrical and Computer Engineering (pg. 355) — only the front portion is FE-Mechanical relevant
**What's in it (relevant subset):** charge, current, voltage, resistance, power; Ohm's and Kirchhoff's laws; series/parallel resistance, capacitance, inductance combination; RC and RL transients (time constant `τ = RC` or `L/R`); AC steady-state with phasors; impedance `Z`, real/reactive/apparent power; basics of DC and AC motors and generators (no machine design); transformer turns ratio.
**Common exam patterns:** find current through a resistor in a multi-loop DC circuit; compute time-constant of an RC charge or discharge; find impedance of a series RLC circuit; identify motor type from torque-speed shape.
**Gotchas:** the FE Mechanical's electrical questions are conceptual and small-circuit; they will not require the full power-systems content that occupies most of the EE section. Don't get sucked into deeper EE material than the question requires.

---

## 8. FE Mechanical Exam Specifications (Official Summary)

For reference (effective from the 2020 specification revision, still current as of the cited edition):

- **110 questions total** over **5 hours 20 minutes** of testing time (within a 6-hour seat time including tutorial and break).
- Closed book; the Handbook PDF is the only reference, with search functionality.
- Both SI and USCS units appear; expect ~half of each.
- Knowledge areas and approximate question counts:

| # | Knowledge Area | Questions | Maps mostly to Handbook section(s) |
|---|---------------|-----------|-----------------------------------|
| 1 | Mathematics | 6–9 | Mathematics |
| 2 | Probability and Statistics | 4–6 | Engineering Probability and Statistics |
| 3 | Ethics and Professional Practice | 4–6 | Ethics and Professional Practice |
| 4 | Engineering Economics | 4–6 | Engineering Economics |
| 5 | Electricity and Magnetism | 5–8 | Electrical and Computer Engineering (front portion) |
| 6 | Statics | 9–14 | Statics |
| 7 | Dynamics, Kinematics, and Vibrations | 10–15 | Dynamics + Mechanical Engineering (vibrations subsection) |
| 8 | Mechanics of Materials | 9–14 | Mechanics of Materials |
| 9 | Material Properties and Processing | 7–11 | Materials Science + Mechanical Engineering (manufacturing) |
| 10 | Fluid Mechanics | 10–15 | Fluid Mechanics |
| 11 | Thermodynamics | 10–15 | Thermodynamics |
| 12 | Heat Transfer | 7–11 | Heat Transfer |
| 13 | Measurements, Instrumentation, and Controls | 5–8 | Instrumentation, Measurement, and Control |
| 14 | Mechanical Design and Analysis | 10–15 | Mechanical Engineering (Sec 21) |

The heavy hitters in order are: Dynamics+Vibrations, Fluid Mechanics, Thermodynamics, Mechanical Design (each 10–15 Qs). Together those four are ~40–60 of the 110 questions. Statics and Mechanics of Materials follow closely. Math, Probability, Ethics, Econ are small but high-leverage (the questions are usually fast).

---

## 9. How the Skill Should Use This Guide

When a student asks the skill an FE-style question:

1. **Identify the Handbook section** the problem maps to from the table in Section 1 above.
2. **State the relevant equation in Handbook form** (Section 3 above is the lookup).
3. **Call out Handbook table values** the student should pull (Section 4) rather than asking them to memorize.
4. **Apply the Handbook's notation** (Section 2) so the student is reading the same symbols on exam day.
5. **Flag gotchas** for that section (Section 7) — the common traps that catch test-takers.
6. **If the needed data isn't in the Handbook** (Section 6), say so explicitly: "The Marin factors aren't in the Handbook; if this were an exam problem, the modifiers would be given in the question stem."

The skill defaults to TUTOR MODE, so the answer should walk through the section identification and equation selection out loud, not just produce a number. The student is calibrating their *exam process*, not just getting an answer.

---

## Sources

- **NCEES FE Reference Handbook**, edition 10.0.1, copyright 2020 by NCEES. ISBN 978-1-947801-11-0. Downloaded from a public mirror at `cee.msstate.edu` for this analysis; the current authoritative copy is available free at https://account.ncees.org after creating a MyNCEES account. See also https://help.ncees.org/article/87-ncees-exam-reference-handbooks for the publisher's distribution page.
- **FE Mechanical CBT Exam Specifications**, NCEES, effective beginning with the July 2020 examinations. Retrieved from https://ncees.org/wp-content/uploads/FE-Mechanical-CBT-specs.pdf .
- **NCEES exam study materials portal**, https://ncees.org/exams/study-materials/ (canonical page for the latest Handbook edition — may show a newer minor revision than 10.0.1 by the time the student sits).

Structural mapping, notation cheat sheet, equation locator, table inventory, and section briefs in this file are summaries and indexes derived from inspecting the cited Handbook; no portion of the Handbook is reproduced verbatim. Where notation or equation form is quoted, it is the standard symbolic form (e.g., `η = 1 − TL/TH`) that is universal across engineering thermodynamics references and not specific creative expression of NCEES.
