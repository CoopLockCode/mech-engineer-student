# Machine Design Reference

A graduate-level study companion for Machine Design I (ME 4141). Covers design for
static failure, design for fatigue failure, failure theories (MSST/Tresca,
DET/von Mises, MNST/Coulomb-Mohr), stress concentration, shaft design, fasteners and
bolted joints, welded joints, springs, bearings, gears, and design factors of safety.
Plain-text math notation: `^` = power, `*` = multiply, `sqrt()` = square root,
`pi` = 3.14159..., subscripts written inline (sigma_a, S_e, K_f).

This reference assumes the Strength of Materials reference (stress analysis, stress
transformation, combined loading) as background — Machine Design takes those stresses
and decides whether a real component made of a real material survives real loading.

---

## 0. The Machine Design Mindset

### 0.1 Analysis vs. design

- **Analysis:** geometry and loads are known → find stresses and factor of safety.
- **Design:** loads and a target factor of safety are known → *find the geometry*
  (size the shaft diameter, choose the bolt, pick the spring wire). Design is
  iterative: assume → analyze → check → resize → repeat.

### 0.2 The design factor of safety n

```
n = (strength) / (stress)        or, in design form,   required strength = n * stress
```

Selecting n is engineering judgment, balancing uncertainty in loads, material
properties, manufacturing, environment, and the consequences of failure. Pugsley's
method and similar build n from sub-factors. Typical ranges:

| Situation | n (on yield, ductile) |
|---|---|
| Loads & material well known, controlled environment | 1.25 – 1.5 |
| Average conditions, ordinary materials | 2.0 – 2.5 |
| Uncertain loads or environment, brittle materials, life-safety | 3.0 – 4.0+ |

Distinguish **design factor n_d** (the target you design to) from **factor of safety
n** (what the finished design actually achieves — must be >= n_d).

### 0.3 Material strength quantities

- **S_y** — yield strength (tension; S_yc in compression — equal for ductile metals,
  larger for brittle).
- **S_ut, S_uc** — ultimate tensile / compressive strength.
- **S_sy** — shear yield strength. By DET, S_sy = 0.577·S_y; by MSST, S_sy = 0.5·S_y.
- **S_e' / S_e** — rotating-beam endurance limit (test) / corrected endurance limit
  (the actual part). For steels, S_e' ≈ 0.5·S_ut (capped at ~700 MPa / 100 ksi). For
  materials with no endurance limit (aluminum, copper), use the **fatigue strength
  S_f at a specified life** (e.g., 5×10^8 cycles).
- **HB** — Brinell hardness. For steels, S_ut ≈ 3.4·HB (MPa) ≈ 0.5·HB (ksi).

### 0.4 Ductile vs. brittle — the master fork

This single distinction drives almost every failure-theory decision:

- **Ductile** (elongation at fracture >= ~5%): fails by **yielding** (shear-driven
  slip). Use MSST or DET. Roughly equal strength in tension and compression. Static
  stress concentration usually neglected (local yielding redistributes).
- **Brittle** (elongation < ~5%): fails by **fracture** (separation across a plane,
  tension-driven). Use MNST or Coulomb-Mohr / modified Mohr. Much stronger in
  compression than tension. Stress concentration **must** be kept even for static loads.

---

## 1. Static Failure Theories

A failure theory maps a multiaxial stress state (sigma_1, sigma_2, sigma_3) onto a
single equivalent quantity that can be compared with a uniaxial test strength.

### 1.1 Maximum Shear Stress Theory (MSST / Tresca) — ductile

**Hypothesis:** yielding begins when the maximum shear stress in the part equals the
maximum shear stress at yield in a simple tension test (= S_y/2).

Order the principal stresses sigma_1 >= sigma_2 >= sigma_3. Then:

```
tau_max = (sigma_1 - sigma_3) / 2 >= S_y / 2     => yield

Failure criterion:  sigma_1 - sigma_3 = S_y
Factor of safety:   n = S_y / (sigma_1 - sigma_3)
```

For **plane stress** with computed in-plane principals sigma_A, sigma_B (and the
third = 0), there are cases: if sigma_A, sigma_B have opposite signs,
n = S_y/(sigma_A - sigma_B); if same sign, n = S_y/|larger one|.

MSST is **conservative** (safe) — it predicts failure slightly earlier than DET.
Simple, hand-friendly.

### 1.2 Distortion Energy Theory (DET / von Mises / Maximum Octahedral Shear) — ductile

**Hypothesis:** yielding begins when the *distortion* strain energy per unit volume
equals the distortion energy per unit volume at yield in simple tension. (Hydrostatic
stress causes only volume change, not yielding — so only the distortion part counts.)

Define the **von Mises (equivalent) stress** sigma':

```
General 3-D principal form:
sigma' = sqrt{ [ (sigma_1-sigma_2)^2 + (sigma_2-sigma_3)^2 + (sigma_3-sigma_1)^2 ] / 2 }

Plane stress (principals sigma_A, sigma_B):
sigma' = sqrt( sigma_A^2 - sigma_A*sigma_B + sigma_B^2 )

General components (no need to find principals first):
sigma' = sqrt( sigma_x^2 + sigma_y^2 - sigma_x*sigma_y + 3*tau_xy^2 )
```

```
Failure criterion:  sigma' = S_y
Factor of safety:   n = S_y / sigma'
```

DET is **more accurate** than MSST for ductile metals and is the default in machine
design. It is slightly less conservative (predicts failure at up to 15% higher load
than MSST). The DET shear-yield relation: **S_sy = 0.577·S_y**.

**MSST vs. DET picture:** in sigma_1–sigma_2 space, DET is an ellipse; MSST is a
hexagon *inscribed* in that ellipse. They agree on the pure-tension and pure-
compression axes; they differ most in pure shear, where MSST gives S_sy = 0.5 S_y and
DET gives 0.577 S_y.

### 1.3 Maximum Normal Stress Theory (MNST) — brittle

**Hypothesis:** fracture occurs when the largest principal stress reaches the
ultimate strength.

```
Failure when:  sigma_1 = S_ut   (tension)   or   sigma_3 = -S_uc  (compression)
Factor of safety:  n = S_ut / sigma_1   (tension-controlled)
```

Adequate for brittle materials when the stress state is mostly tensile; inaccurate in
the tension–compression quadrants. Do **not** use for ductile materials.

### 1.4 Coulomb-Mohr and Modified Mohr — brittle, unequal strengths

For brittle materials with S_uc > S_ut, the **Brittle Coulomb-Mohr** theory
interpolates linearly between the tension and compression limits. With ordered
principals sigma_1 >= sigma_3:

```
If sigma_1 >= 0 >= sigma_3:   sigma_1/S_ut - sigma_3/S_uc = 1/n
If both positive:             n = S_ut / sigma_1
If both negative:             n = S_uc / |sigma_3|
```

**Modified Mohr** corrects Coulomb-Mohr in the fourth quadrant (one tension, one
compression) where Coulomb-Mohr is overly conservative; it agrees better with cast-
iron test data and is the recommended brittle theory when data is available.

### 1.5 Static failure theory — decision logic

```
Is the material DUCTILE (elongation >= ~5%)?
├── YES → use DET (von Mises) for accuracy, or MSST for a conservative quick check.
│         Compute sigma', compare to S_y, n = S_y/sigma'.
│         Keep stress concentration only if loading is also fatigue or material is
│         marginally ductile; for purely static ductile loading K_t is usually dropped.
└── NO (brittle) → is compression strength ~ equal to tension strength?
        ├── YES (rare) → MNST acceptable.
        └── NO (S_uc > S_ut, typical cast iron) → use Modified Mohr (preferred) or
              Brittle Coulomb-Mohr (conservative). ALWAYS keep K_t for brittle parts,
              even static.
```

---

## 2. Stress Concentration

### 2.1 Geometric (theoretical) factor K_t

A geometric discontinuity (fillet, hole, groove, keyway, shoulder) raises local
stress above the nominal:

```
sigma_max = K_t * sigma_nom         tau_max = K_ts * tau_nom
```

K_t (normal) and K_ts (shear) come from charts (Peterson's, Roark's) as functions of
geometry ratios (r/d, D/d, etc.). K_t depends only on geometry and load type, not on
the material.

### 2.2 Static use of K_t

- **Ductile + static load:** localized yielding at the notch redistributes stress;
  K_t is commonly **neglected** for static strength (but not for deflection or for
  brittle/low-ductility materials).
- **Brittle + static load:** K_t **must be applied** — no yielding to relieve the peak.
- **Any material + fatigue load:** stress concentration **always** matters — see §3.

### 2.3 Fatigue stress concentration factor K_f and notch sensitivity

Materials are less sensitive to notches in fatigue than the full geometric K_t
predicts. Define the **fatigue stress concentration factor**:

```
K_f = 1 + q * (K_t - 1)
```

where **q = notch sensitivity** (0 <= q <= 1; q = 0 means no notch effect, q = 1
means the full geometric effect applies). q is read from charts as a function of
notch radius r and material (q rises with notch radius and with material strength).
A parallel factor K_fs uses q_shear with K_ts for shear/torsional concentration.

**Where to apply K_f:** multiply it onto the **alternating** stress component (and,
in the conservative approach, onto the mean stress too — modern practice often
applies K_f to both sigma_a and sigma_m).

---

## 3. Fatigue Failure (Design for Variable Loading)

Most machine parts fail by **fatigue** — progressive cracking under repeated loading
at stress levels *well below* the static strength. Roughly: a crack initiates at a
stress concentration, propagates a little each cycle, and final fracture occurs when
the remaining section can no longer carry the load. Fatigue fractures show a
characteristic "beach mark" region (slow growth) plus a final fast-fracture zone.

### 3.1 Stress cycle nomenclature (fluctuating stress)

Given a stress that cycles between sigma_max and sigma_min:

```
Mean stress:        sigma_m = (sigma_max + sigma_min) / 2
Alternating (amplitude) stress: sigma_a = (sigma_max - sigma_min) / 2
Stress range:       sigma_r = sigma_max - sigma_min
Stress ratio:       R = sigma_min / sigma_max
Amplitude ratio:    A = sigma_a / sigma_m
```

Special cases:
- **Fully reversed:** sigma_m = 0, R = -1 (rotating shaft bending — the classic case).
- **Repeated / released:** sigma_min = 0, R = 0, so sigma_m = sigma_a.
- **Static:** sigma_a = 0, R = 1.

### 3.2 The S-N diagram

Plot of fatigue strength (stress amplitude for fully reversed loading) vs. number of
cycles to failure N, on log-log axes (Wohler curve).

- **Low-cycle fatigue:** N < ~10^3 cycles. Often treated as quasi-static.
- **High-cycle fatigue:** N >= ~10^3 cycles.
- **Endurance limit S_e:** for steels and some titaniums, the S-N curve becomes
  horizontal at about 10^6–10^7 cycles — stresses below S_e give (theoretically)
  infinite life. **Nonferrous metals (aluminum, copper) have NO endurance limit** —
  the curve keeps dropping; you specify a fatigue strength S_f at a chosen life
  (e.g., 5×10^8 cycles).

### 3.3 The rotating-beam endurance limit S_e'

From the standard R.R. Moore rotating-beam test (polished specimen, 7.5 mm dia,
fully reversed bending):

```
Steels:   S_e' ≈ 0.5 * S_ut      for S_ut <= ~1400 MPa (200 ksi)
          S_e' ≈ 700 MPa (100 ksi)   for S_ut above that cap
Cast iron: S_e' ≈ 0.4 * S_ut
```

S_e' is the *idealized* lab value. The real part is not a polished lab specimen, so
it must be corrected.

### 3.4 Marin endurance-limit modification factors

The corrected endurance limit of the actual part:

```
S_e = k_a * k_b * k_c * k_d * k_e * k_f * S_e'
```

| Factor | Name | What it accounts for |
|---|---|---|
| k_a | Surface condition | Finish: ground, machined, hot-rolled, as-forged. k_a = a*(S_ut)^b with tabulated a, b per finish. Rougher → lower k_a. |
| k_b | Size | Larger parts have more volume at high stress → lower strength. k_b ≈ 1 for axial loading; for bending/torsion of round sections k_b = 1.24*d^-0.107 (2.79 <= d <= 51 mm), etc. Use an equivalent diameter for non-round sections. |
| k_c | Load type | k_c = 1 (bending), 0.85 (axial), 0.59 (torsion). Reflects that the test was a bending test. |
| k_d | Temperature | k_d ≈ 1 near room temp; reduces at elevated temperature; k_d = S_T/S_RT. |
| k_e | Reliability | Adjusts for scatter in fatigue data. k_e = 1 - 0.08*z_a; e.g. 0.897 for 90%, 0.868 for 95%, 0.814 for 99%, 0.753 for 99.9% reliability. |
| k_f | Miscellaneous | Catch-all: corrosion, plating, residual stress, case hardening, frettage, etc. |

If a factor is unknown or not applicable, set it to 1. Note **k_c is applied as a
Marin factor** when the loading is a single type; when combining loading types
(bending + torsion together) the modern approach drops k_c and instead builds a von
Mises alternating stress and a von Mises mean stress, with k_c = 1.

### 3.5 Fluctuating-stress failure criteria (mean-stress effect)

A nonzero mean stress reduces the allowable alternating stress. On the
sigma_m (x-axis) vs. sigma_a (y-axis) diagram, several lines connect the alternating-
only point (0, S_e) to a mean-only point on the x-axis:

```
Soderberg (most conservative; line to S_y):
    sigma_a/S_e + sigma_m/S_y = 1/n

Modified Goodman (line to S_ut; the workhorse):
    sigma_a/S_e + sigma_m/S_ut = 1/n

Gerber (parabola to S_ut; best fit to ductile-steel data, mean of the scatter):
    (n*sigma_a)/S_e + (n*sigma_m/S_ut)^2 = 1

ASME-elliptic (quarter ellipse to S_y; good fit, accounts for yield):
    (n*sigma_a/S_e)^2 + (n*sigma_m/S_y)^2 = 1

Langer first-cycle yield line (guards against yielding on the first cycle):
    sigma_a + sigma_m = S_y / n
```

**Relationship / when to use which:**
- **Soderberg** — most conservative, automatically guards against yield (uses S_y),
  rarely used for final design because it wastes material.
- **Modified Goodman** — straight line, slightly conservative, easy algebra, the most
  common teaching and design criterion. Does NOT guard against first-cycle yield by
  itself — pair it with the Langer line and take the more restrictive.
- **Gerber** — parabola, best central fit to experimental ductile-steel data; less
  conservative; good for "expected life" estimates.
- **ASME-elliptic** — good experimental fit and inherently considers yielding;
  increasingly the recommended criterion.

The **safe design region** is below/inside whichever line(s) you adopt; the governing
factor of safety is the smallest of the fatigue n and the Langer yield n.

### 3.6 Fatigue analysis procedure (the full recipe)

1. **Loads → stresses.** Find the time-varying loads; compute sigma_max and sigma_min
   (or M_max, M_min, T_max, T_min) at the critical section.
2. **Mean and alternating components:** sigma_m = (sigma_max+sigma_min)/2,
   sigma_a = (sigma_max-sigma_min)/2 — for each loading type.
3. **Apply stress concentration:** multiply by K_f (and K_fs for shear). Conservative
   modern practice applies K_f to both sigma_a and sigma_m.
4. **Combine multiaxial stresses** into a **von Mises alternating stress sigma_a'**
   and a **von Mises mean stress sigma_m'** (using the §1.2 formula on the alternating
   components and again on the mean components separately).
5. **Static endurance limit:** S_e' = 0.5·S_ut (steel, capped).
6. **Correct it:** S_e = k_a·k_b·k_c·k_d·k_e·k_f·S_e' (Marin factors). With the
   von Mises combination in step 4, take k_c = 1.
7. **Choose a criterion** (Modified Goodman / Gerber / ASME-elliptic / Soderberg) and
   compute the **fatigue factor of safety n_f** from its equation using sigma_a',
   sigma_m'.
8. **Check first-cycle yield** with the Langer line: n_y = S_y / (sigma_a' + sigma_m').
9. **Governing n = min(n_f, n_y).** If finite life is wanted instead of infinite, use
   the S-N curve: find the fatigue strength at the target N and substitute it for S_e.
10. **Resize and iterate** if n < n_d.

### 3.7 Cumulative damage — Miner's rule

For variable-amplitude loading (several stress levels, each applied n_i cycles, each
with fatigue life N_i at that level):

```
Miner's rule:  sum( n_i / N_i ) = 1  at failure  (often 0.7–2.2 in practice; 1 is the design value)
```

### 3.8 Fatigue pitfalls

- Forgetting that **aluminum has no endurance limit** — you must design to a finite
  life and a specified S_f.
- Applying S_e' directly without the Marin correction (overestimates strength badly).
- Omitting K_f — stress concentration is *always* relevant in fatigue, even for
  ductile materials.
- Confusing sigma_max with sigma_a — the alternating stress is the *amplitude*, half
  the range.
- Using k_c twice — once as a Marin factor *and* again via a von Mises combination.
  Pick one approach.
- Forgetting the Langer yield check — Goodman alone can allow a stress state that
  yields on cycle one.

---

## 4. Shaft Design

### 4.1 Stresses in a rotating shaft

A rotating shaft carrying transverse loads sees **fully reversed bending** (each
fiber alternates tension/compression every revolution) and usually a **steady
torque**. So typically: sigma_a from bending (M_a), sigma_m from bending ≈ 0; tau_m
from torque (T_m), tau_a from torque ≈ 0 (if torque is steady).

For a solid round shaft of diameter d:

```
Bending stress:  sigma = 32*M / (pi*d^3)
Torsional shear: tau   = 16*T / (pi*d^3)
```

### 4.2 The DE-Goodman shaft-sizing equation

Combining the von Mises stress, the modified Goodman criterion, and the round-shaft
section properties yields a closed-form **diameter** equation. For fully reversed
bending moment M_a and steady torque T_m (the common case), with fatigue factors K_f
(bending) and K_fs (torsion):

```
d = { (16*n)/pi * [ (sqrt(4*(K_f*M_a)^2)) / S_e  +  (sqrt(3*(K_fs*T_m)^2)) / S_ut ] }^(1/3)
```

More general DE-Goodman form (all four components M_a, M_m, T_a, T_m present):

```
1/n = (16/(pi*d^3)) * [ (1/S_e) * sqrt( 4*(K_f*M_a)^2 + 3*(K_fs*T_a)^2 )
                       + (1/S_ut)* sqrt( 4*(K_f*M_m)^2 + 3*(K_fs*T_m)^2 ) ]
```

Analogous closed forms exist for **DE-Gerber**, **DE-ASME-elliptic**, and
**DE-Soderberg** — same structure, different criterion algebra. Soderberg uses S_y
in place of S_ut and inherently guards yield; Gerber and ASME-elliptic are less
conservative.

### 4.3 Shaft design procedure

1. Draw the shaft layout; place gears, pulleys, bearings; find reaction forces in two
   planes.
2. Draw bending-moment diagrams in both planes; combine: M = sqrt(M_xz^2 + M_xy^2).
   Identify the **critical section** (often a shoulder fillet or keyway near max M).
3. Determine M_a, M_m, T_a, T_m at that section.
4. Get K_f, K_fs from the local geometry (fillet radius, keyway).
5. Material: S_ut, S_y → S_e' → Marin factors → S_e.
6. Pick a criterion (DE-Goodman is the standard teaching choice) and solve for d.
7. Round up to a standard size; recheck n (including a first-cycle yield check using
   the maximum instantaneous stress).
8. **Check deflection and slope** — shafts often fail serviceability (bearing
   misalignment, gear-mesh error) before strength. Slope at bearings and gears, and
   lateral deflection at gears, have allowable limits.
9. **Check critical (whirl) speed** — the shaft's first bending natural frequency
   should be well clear of the operating speed (rule of thumb: operate below ~0.75×
   or above ~1.5× the critical speed).

### 4.4 Shaft pitfalls

- Forgetting to combine bending in two planes before finding M.
- Putting the critical section at max M when a stress concentration elsewhere (keyway,
  small fillet) actually governs.
- Designing only for strength and ignoring deflection/critical-speed limits.
- Treating a steady torque as contributing to sigma_a (it contributes to the mean).

---

## 5. Bolted and Screwed Joints

### 5.1 Thread and fastener geometry

- **Tensile stress area A_t** — the effective area for a threaded rod in tension,
  based on the mean of pitch and minor diameters (tabulated per thread size; always
  use A_t, not the nominal-diameter area, for thread tension).
- **Proof strength S_p** — the maximum stress a bolt can take with no permanent set;
  the key bolt-grade strength (SAE grades, metric property classes 4.6, 8.8, 10.9,
  12.9). S_p ≈ 0.85·S_y typically.

### 5.2 Preloaded bolted joints in tension — the joint stiffness model

A properly designed bolted joint is **preloaded** (tightened to an initial tension
F_i). External load is then *shared* between bolt and clamped members in proportion
to their stiffnesses.

```
Joint stiffness constant:  C = k_b / (k_b + k_m)

k_b = bolt stiffness (bolt acts as a spring; combine shank + threaded portions in series)
k_m = clamped-members stiffness (often from a frustum-cone model of the compressed material)
```

When an external tensile load P is applied per bolt:

```
Bolt total load:    F_b = C*P + F_i
Member load:        F_m = (1-C)*P - F_i      (joint stays clamped while F_m < 0, i.e. compressive)
Bolt stress:        sigma_b = F_b / A_t
```

Because the members are much stiffer than the bolt (C is typically 0.2–0.4), most of
the external load goes into *relieving member compression*, not into stretching the
bolt — this is the whole point of preload: it makes the bolt see only a fraction C of
P, dramatically improving fatigue life.

### 5.3 Bolt factors of safety (static, tension joint)

```
Yielding of bolt:     n_p = (S_p*A_t - F_i) / (C*P)        [load factor: load needed to reach proof]
Joint separation:     n_0 = F_i / [ P*(1 - C) ]            [load factor against the joint opening]
```

Recommended preload: F_i = 0.75·F_proof for reused connections, 0.90·F_proof for
permanent ones, where F_proof = S_p·A_t.

### 5.4 Bolted joints in fatigue

With a fluctuating external load (P from P_min to P_max), only the bolt's *share* C·P
fluctuates:

```
Alternating bolt stress: sigma_a = C*(P_max - P_min) / (2*A_t)
Mean bolt stress:        sigma_m = C*(P_max + P_min) / (2*A_t) + F_i/A_t
```

Apply a fatigue criterion (Goodman/Gerber). The fatigue factor of safety with preload
sigma_i = F_i/A_t (Goodman form):

```
n_f = (S_e*(S_ut - sigma_i)) / (S_e*(sigma_m - sigma_i) + S_ut*sigma_a)
```

Preload sigma_i raises the mean but, by reducing C·P share, **improves** fatigue life
overall — high preload is good for fatigue.

### 5.5 Bolted/riveted joints loaded in shear

Failure modes to check for a shear-loaded bolt group (each gives a separate n):

1. **Bolt shear** — tau = V/A_v (single or double shear).
2. **Bearing (crushing)** on the bolt or the plate hole — sigma_b = F/(t·d).
3. **Tension tear-out of the plate** through the net section — sigma = F/A_net.
4. **Shear tear-out / edge rupture** of the plate behind the bolt.

For an **eccentrically loaded bolt group**, superpose: (a) a *direct* shear (total
load ÷ number of bolts, same direction on each) and (b) a *moment* shear (torque =
load × eccentricity, distributed to each bolt proportional to its distance from the
group centroid, perpendicular to that radius). Vector-add the two on the worst bolt.

### 5.6 Bolt-joint pitfalls

- Using nominal diameter area instead of A_t for thread tension.
- Forgetting preload entirely — an un-preloaded bolt sees the *full* external load,
  with terrible fatigue performance.
- Forgetting the separation check — a joint that opens loses its preload benefit and
  the bolt then sees full load impact.
- For shear joints, checking only bolt shear and missing bearing or tear-out.

---

## 6. Welded Joints

### 6.1 Fillet weld geometry and stress

The weld is idealized to fail across its **throat**. For a fillet weld of leg size h,
the throat is t = 0.707·h. The stress is taken on the **throat area** A = 0.707·h·L
(L = total weld length):

```
Direct (transverse or parallel) shear:   tau = F / (0.707 * h * L)
```

The standard code approach treats *all* fillet-weld stress as **shear on the throat**,
regardless of whether the applied load is tension or shear — a deliberate
simplification that matches test data conservatively.

### 6.2 Weld groups loaded by bending or torsion — treat the weld as a line

For a weld group resisting a moment, use the **"weld as a line"** method: compute the
unit second moment of area of the weld pattern (a geometric property of the line
pattern, units length^3), call it I_u (bending) or J_u (torsion). Then:

```
Throat area:             A = 0.707 * h * (total weld length)
Bending: section modulus S = 0.707 * h * S_u  where S_u = I_u/c
Torsion: polar modulus    = 0.707 * h * J_u

tau_from_moment = M*c/(0.707*h*I_u)   etc.
```

Compute the primary (direct) shear and the secondary (moment) shear, vector-add at
the worst point of the weld group, compare to the allowable weld-metal shear stress.

### 6.3 Allowable weld stresses and fatigue

Allowable stresses are set by code (AWS) per electrode classification (e.g., E60xx,
E70xx — the number is the tensile strength in ksi). Welds in fatigue: use **stress
concentration factors** specific to the weld type (reinforced butt weld, toe of
transverse fillet, end of parallel fillet — each has a tabulated K_f), because weld
toes are severe stress raisers.

### 6.4 Weld pitfalls

- Using leg size h instead of throat 0.707h for the stress area.
- Forgetting to vector-add direct and moment-induced shear in a loaded weld group.
- Ignoring the high fatigue stress concentration at weld toes.

---

## 7. Mechanical Springs

### 7.1 Helical compression spring — stresses

For a round-wire helical spring: wire diameter d, mean coil diameter D, axial force
F. **Spring index** C = D/d (good range 4–12; below 4 hard to form, above 12 tangles).

The wire sees torsional shear from the coil torque *plus* direct (transverse) shear.
Combined and corrected:

```
Shear stress:   tau = K_s * (8*F*D) / (pi*d^3)
   K_s = (2C+1)/(2C)        — direct-shear (static) correction factor

For fatigue, use the Bergsträsser/Wahl factor (includes curvature effect):
   K_W = (4C-1)/(4C-4) + 0.615/C        (Wahl factor)
```

### 7.2 Deflection and spring rate

```
Deflection:   delta = (8 * F * D^3 * N_a) / (d^4 * G)
Spring rate:  k = F/delta = (d^4 * G) / (8 * D^3 * N_a)
```

N_a = number of **active** coils. End treatment determines active vs. total coils:
plain ends N_a = N_t; squared & ground ends N_a = N_t - 2; squared ends N_a = N_t - 2;
plain & ground N_a = N_t - 1.

### 7.3 Spring design checks

- **Solid length / clash allowance:** the spring must not go solid in service; keep a
  clash allowance (~10–15% of working deflection).
- **Buckling:** slender compression springs buckle — check the free-length-to-mean-
  diameter ratio against stability charts (depends on end conditions).
- **Fatigue:** for cyclically loaded springs use the torsional endurance limit of
  spring wire (e.g., Zimmerli data: S_se ~ 310 MPa for unpeened, higher if shot-
  peened) and a Goodman/Gerber check in the shear domain.
- **Spring materials:** music wire, oil-tempered wire, chrome-vanadium, etc.; ultimate
  strength is size-dependent: S_ut = A / d^m with tabulated A, m per material.

### 7.4 Spring pitfalls

- Using total coils where active coils are required (or vice versa).
- Forgetting the curvature (Wahl) correction in fatigue — it raises the actual peak
  stress on the inside of the coil substantially.
- Designing to a stress without checking solid-length and buckling.

---

## 8. Rolling-Element Bearings

### 8.1 Bearing life — the L10 / basic dynamic load rating model

Rolling bearings fail by **surface fatigue (spalling)**. Life is statistical. The
**basic dynamic load rating C** is the load that gives an L10 life (life that 90% of
bearings exceed) of 10^6 revolutions.

```
Life equation:   L10 = (C / P)^a   million revolutions

   a = 3   for ball bearings
   a = 10/3 for roller bearings
   P = equivalent radial load
```

To design for a different reliability or a different life:

```
Required rating:  C = P * (L_desired / L10)^(1/a) * (1/K_R)
```

where K_R is a reliability adjustment factor (K_R = 1 at 90% reliability, < 1 for
higher reliability).

### 8.2 Equivalent load for combined radial + thrust

When a bearing sees both radial load F_r and axial (thrust) load F_a:

```
P = X * V * F_r + Y * F_a
```

X, Y are tabulated factors that depend on the bearing type and the ratio F_a/F_r
relative to a threshold e; V is a rotation factor (1.0 inner ring rotating, 1.2 outer
ring rotating).

### 8.3 Bearing selection procedure

1. Determine radial and thrust loads at each bearing from the shaft reactions.
2. Pick a bearing type (deep-groove ball, angular contact, cylindrical roller, tapered
   roller, thrust...) based on load direction, speed, and space.
3. Compute the equivalent load P.
4. Choose the desired life L (hours → revolutions using speed) and reliability.
5. Compute the required C; select a catalog bearing with rating >= C.
6. Check speed limits, mounting, lubrication, and that the bore fits the shaft.

### 8.4 Bearing pitfalls

- Using the wrong life exponent a (3 for ball, 10/3 for roller).
- Forgetting to convert operating hours and rpm into revolutions.
- Ignoring the thrust component when computing P.

---

## 9. Gears (Spur Gear Strength)

### 9.1 Geometry fundamentals

- **Module m** (SI) or **diametral pitch P_d** (US) — tooth-size measure;
  m = d/N (pitch diameter / number of teeth); P_d = N/d. m = 25.4/P_d.
- **Pitch diameter d**, **circular pitch p = pi·m**, **pressure angle phi**
  (commonly 20°), **addendum, dedendum, face width F**.
- **Velocity ratio:** omega_pinion/omega_gear = N_gear/N_pinion = d_gear/d_pinion.

### 9.2 Lewis bending equation — tooth root bending fatigue

The gear tooth is modeled as a cantilever beam; bending stress at the tooth root:

```
Lewis form:   sigma = W_t * P_d / (F * Y)        (US)
              sigma = W_t / (F * m * Y)          (SI)

   W_t = transmitted tangential load = T / (d/2) = 2T/d
   Y   = Lewis form factor (function of number of teeth and tooth system)
   F   = face width
```

The transmitted load comes from the power: W_t = (power)/(pitch-line velocity), with
pitch-line velocity v = pi·d·n.

### 9.3 AGMA refinement

The modern **AGMA bending stress equation** dresses up the Lewis equation with factors:

```
sigma = W_t * K_o * K_v * K_s * (P_d / F) * (K_m * K_B / J)
```

- K_o — overload factor (shock from driver/driven machine).
- K_v — dynamic factor (tooth-mesh dynamics, increases with pitch-line velocity).
- K_s — size factor.
- K_m — load-distribution factor (face-width misalignment).
- K_B — rim-thickness factor.
- J — AGMA geometry factor (a refined Lewis form factor including stress concentration
  at the root fillet and load sharing).

Compare to the **allowable bending stress number S_t** adjusted by life factor Y_N,
temperature factor K_T, reliability factor K_R: sigma <= S_t·Y_N/(K_T·K_R·SF).

### 9.4 Surface durability — AGMA contact (pitting) stress

Gears also fail by **surface pitting** — contact (Hertzian) fatigue on the tooth
flanks:

```
sigma_c = C_p * sqrt( W_t * K_o * K_v * K_s * (K_m / (d_p * F)) * (C_f / I) )
```

C_p = elastic coefficient, I = geometry factor for pitting, C_f = surface-condition
factor. Compare to allowable contact stress number S_c adjusted by life factor Z_N,
hardness-ratio factor C_H, etc. **Both bending and pitting must be checked** — a gear
is safe only if it passes both.

### 9.5 Gear pitfalls

- Checking only bending and forgetting surface durability (or vice versa).
- Mixing module and diametral pitch units.
- Using the wrong geometry factor (Lewis Y vs. AGMA J).
- Forgetting that the pinion (smaller gear) usually governs — fewer teeth, more
  load cycles per unit time, smaller form factor.

---

## 10. Cross-Cutting Design Patterns and Pitfalls

### 10.1 The general machine-element design loop

1. **Function & loads** — what must the part do; what are the worst-case static and
   fluctuating loads?
2. **Material & strengths** — pick a candidate; gather S_y, S_ut, S_e', hardness.
3. **Critical-location stress analysis** — find the worst section; compute nominal
   stresses; apply K_t / K_f.
4. **Static check** — DET (ductile) or Mohr (brittle); n_static >= n_d?
5. **Fatigue check** — Marin-corrected S_e; Goodman/Gerber/ASME; n_fatigue >= n_d?
   Plus a first-cycle yield (Langer) check.
6. **Serviceability check** — deflection, slope, vibration/critical speed, wear,
   thermal.
7. **Iterate** geometry/material until all checks pass with margin; then choose
   standard sizes and recheck.

### 10.2 Recurring student pitfalls across all machine-design topics

- **Ductile/brittle confusion** — picking the wrong failure theory; forgetting that
  brittle parts keep K_t even when static.
- **Endurance limit misuse** — using S_e' (lab) instead of S_e (corrected); assuming
  aluminum has an endurance limit.
- **Mean vs. alternating** — mixing up sigma_m and sigma_a, or forgetting that a
  steady torque is a *mean* shear, not alternating.
- **Stress concentration in fatigue** — dropping K_f because "the material is
  ductile" (valid for static, invalid for fatigue).
- **Preload omission** — analyzing a bolted joint as if the bolt sees the full
  external load.
- **Single failure mode** — checking bolt shear but not bearing/tear-out; checking
  gear bending but not pitting; checking shaft strength but not deflection.
- **Units** — module vs. diametral pitch; A_t vs. nominal area; throat vs. leg of a
  weld; revolutions vs. hours for bearing life.
- **n_d vs. n** — designing *to* a factor of safety, then forgetting to verify the
  finished (rounded-to-standard-size) part still achieves it.
- **Conservatism stacking** — multiplying every conservative assumption together can
  produce an absurdly heavy design; know which choices are "best estimate" (Gerber)
  vs. "safe bound" (Soderberg, MSST).

---

## Open-source sources used

- **Roylance, David.** *Mechanics of Materials.* MIT OpenCourseWare, hosted on
  Engineering LibreTexts (CC BY-NC-SA 4.0).
  https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_of_Materials_(Roylance)
  — yield and fracture criteria, material fatigue, stress concentration, dislocation
  basis of yielding (Chapter 6).
- **Moore, Jacob, et al.** *Mechanics Map* open textbook (CC BY-NC-SA), Engineering
  LibreTexts and Penn State ROAM.
  https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Mechanics_Map_(Moore_et_al.)
  and https://roam.libraries.psu.edu/node/1519 — combined-loading stress analysis,
  section properties, equilibrium framework feeding component design.
- **Lord, J., Davison, S., Richardson, A., Dillard, D.** *Strength of Materials*
  (Virginia Tech), Open Textbook Library (CC BY-NC-SA).
  https://open.umn.edu/opentextbooks/textbooks/1544 — stress/strain, combined loading,
  and failure-theory foundations underpinning machine-element design.
- **Baker, D. and Haynes, W.** *Engineering Statics: Open and Interactive*, Open
  Textbook Library / Engineering LibreTexts (CC BY-NC-SA).
  https://engineeringstatics.org/ — equilibrium, load paths, and reaction analysis
  prerequisite to component loading.
- **LibreTexts Engineering**, Mechanical Engineering bookshelf (CC BY-NC-SA), general
  index for open mechanical-engineering course material.
  https://eng.libretexts.org/Bookshelves/Mechanical_Engineering
- **Open Textbook Library**, Engineering / Mechanical Engineering collection
  (assorted CC-licensed mechanics and design texts).
  https://open.umn.edu/opentextbooks
- Standard machine-design failure, fatigue, and component-sizing relations
  (DET/von Mises, MSST, Coulomb-Mohr, Marin endurance modifiers, Goodman/Soderberg/
  Gerber/ASME-elliptic, DE-Goodman shaft equation, bolted-joint stiffness model,
  fillet-weld throat method, helical-spring Wahl factor, bearing L10 model, Lewis/AGMA
  gear equations) are the standardized, non-proprietary engineering relations
  presented consistently across the open texts above and open courseware handouts
  such as the Missouri S&T *Fundamental Mechanics of Materials Equations* sheet
  (https://web.mst.edu/jthomas/classes/2210/formulas/).
