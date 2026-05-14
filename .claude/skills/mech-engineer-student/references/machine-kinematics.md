# Machine Kinematics Reference — Gears, Gear Trains, Cams, Power Screws & Mechanical Advantage

> PhD-level study companion for ENGR 3125 — Machine Dynamics & Vibrations (textbook: Martin,
> *Kinematics and Dynamics of Machines*). This file **complements `vibrations.md`**, which covers
> SDOF/MDOF vibration and linkage kinematics; this file covers the topics `vibrations.md` omits:
> gear geometry, gear trains (simple, compound, reverted, epicyclic, worm, belt/chain), cam
> profile design, power screws, and mechanical advantage.
>
> Plain-text math notation: `^` = power, `*` = multiply, `/` = divide, `sqrt()` = square root,
> subscripts inline (N_A, omega_arm, d_p). Greek spelled out or as symbols: phi = pressure angle,
> omega = angular velocity, alpha = angular acceleration, lambda = lead angle, eta = efficiency,
> theta = cam/shaft angle, beta = cam segment angle, mu = friction coefficient.

---

## PART 1 — SPUR GEAR TOOTH GEOMETRY & FUNDAMENTALS

### 1.1 Why Gears? The Problem of Conjugate Action

A gear pair must transmit rotary motion from one shaft to another with a **constant angular
velocity ratio** — no fluctuation. Friction wheels (two cylinders pressed together) slip; gears
add teeth to prevent slip but the teeth must be shaped so motion stays smooth. The requirement
that the velocity ratio be constant is the **Fundamental Law of Gearing**:

> **Fundamental Law of Gearing:** For a gear pair to produce a constant angular velocity ratio,
> the common normal to the tooth profiles at the point of contact must always pass through a
> fixed point on the line of centers, called the **pitch point** P.

Tooth profiles that satisfy this are called **conjugate profiles**, and the resulting smooth
transmission is **conjugate action**. The pitch point divides the line of centers into segments
inversely proportional to the angular velocities:

    omega_1 / omega_2 = r_2 / r_1   (r = pitch radius)

Two curves satisfy conjugate action well in practice: the **cycloid** (historical, used in
clocks) and the **involute** (universal in power transmission). The involute dominates because
of the properties below.

### 1.2 The Involute Profile

**Definition.** An involute of a circle is the curve traced by the end of a taut string as it
is unwrapped from a circle. The circle is the **base circle**; the string is always tangent to
the base circle, and the string is the **radius of curvature** of the involute at that point.

**Why the involute is used (its key advantages):**

1. **Conjugate action is automatic.** When two involutes mesh, the line of action (common normal
   at the contact point) is the common internal tangent to the two base circles. It is a
   **straight, fixed line** — it never moves. Therefore the common normal always crosses the
   line of centers at the same pitch point => constant velocity ratio, always.
2. **Insensitive to center distance.** Because the line of action depends only on the base
   circles, small errors in center distance (bearing wear, manufacturing tolerance) do **not**
   change the velocity ratio. They only change the pressure angle and backlash slightly.
3. **Interchangeability.** Any two involute gears of the same module/diametral pitch and the
   same pressure angle will mesh correctly regardless of tooth count. This is why gears are
   stocked by module and pressure angle, not as matched sets.
4. **Straight-sided rack.** The involute of an infinitely large base circle is a straight line,
   so a gear meshes with a straight-toothed **rack**. This allows generating-type manufacture
   (hobbing, rack-cutter shaping).

### 1.3 Gear Nomenclature

| Term | Symbol | Definition |
|---|---|---|
| Pitch circle | — | Imaginary circle that rolls without slip on the mating gear's pitch circle. The "working" circle. |
| Pitch radius / diameter | r, d | d = pitch diameter; r = d/2 |
| Pitch point | P | Point where the two pitch circles are tangent; lies on line of centers |
| Base circle | r_b, d_b | Circle from which the involute is generated. d_b = d * cos(phi) |
| Pressure angle | phi | Angle between the line of action and the common tangent to the pitch circles. Standard: 20° (most common), 14.5° (older), 25° |
| Line of action (pressure line) | — | The straight line along which contact force acts; tangent to both base circles; inclined at phi to the common tangent |
| Addendum | a | Radial distance from pitch circle to tooth tip. Standard full-depth: a = m = 1/P |
| Dedendum | b | Radial distance from pitch circle to tooth root. Standard: b = 1.25*m (= 1.25/P) |
| Clearance | c | c = b - a = 0.25*m. Gap between tip of one tooth and root of mate |
| Whole depth | h_t | h_t = a + b = 2.25*m |
| Working depth | h_k | h_k = 2*a = 2*m. Sum of addenda; depth of mesh engagement |
| Addendum circle | r_a | Outside circle. r_a = r + a |
| Dedendum (root) circle | r_d | r_d = r - b |
| Circular pitch | p | Arc distance on the pitch circle from one tooth to the corresponding point on the next. p = pi*d/N |
| Tooth thickness | t | Arc thickness of a tooth on the pitch circle. Nominally t = p/2 |
| Tooth space | — | Arc width of the space; nominally p/2; (space - thickness) = backlash |
| Face width | F | Length of tooth measured axially |
| Backlash | B | Amount by which tooth space exceeds tooth thickness on the pitch circle, measured along the pitch circle |
| Number of teeth | N | Integer count of teeth |

### 1.4 Module, Diametral Pitch, Circular Pitch — the Size Parameters

Three equivalent ways to specify tooth size; pick one consistently.

- **Module** m (SI, units = mm): m = d / N. "Millimeters of pitch diameter per tooth."
  Standard modules: 1, 1.25, 1.5, 2, 2.5, 3, 4, 5, ... mm.
- **Diametral pitch** P (US customary, units = teeth/inch): P = N / d. "Teeth per inch of pitch
  diameter." Standard: 4, 6, 8, 10, 12, 16, 20, 24, 32, 48.
- **Circular pitch** p (units of length): p = pi*d/N = pi*m  (SI) = pi/P (US).

**Conversions and identities:**

    m = d/N        P = N/d        p = pi*d/N
    m = 1/P        (when m in inches; or m[mm] = 25.4/P)
    p = pi*m = pi/P
    m * P = 1      (consistent units)

**Meshing condition:** two gears mesh only if they have the **same module** (or same diametral
pitch) **and the same pressure angle**.

### 1.5 Center Distance and Velocity Ratio

For an **external** gear pair, the pitch circles are tangent externally:

    C = r_1 + r_2 = (d_1 + d_2)/2 = m*(N_1 + N_2)/2 = (N_1 + N_2)/(2*P)

For an **internal** gear pair (pinion inside an internal/ring gear):

    C = r_ring - r_pinion = m*(N_ring - N_pinion)/2

**Velocity ratio (speed ratio)** — the central result. Because pitch circles roll without slip,
v = omega_1 * r_1 = omega_2 * r_2 at the pitch point, and since d is proportional to N:

    VR = omega_driven / omega_driving = N_driving / N_driven = d_driving / d_driven = r_driving / r_driven

The **gear ratio** (often quoted as the reduction) is the reciprocal of the driven/driving
speed ratio:

    m_G = N_driven / N_driving = omega_driving / omega_driven   (>1 for a speed reducer)

**Torque ratio (ideal, no losses):** since power P = T*omega is conserved,

    T_driven / T_driving = omega_driving / omega_driven = N_driven / N_driving

A speed reducer multiplies torque by the same factor it divides speed.

**Direction:** an external mesh **reverses** rotation sense; an internal mesh **preserves** it.

### 1.6 Line of Action, Contact Ratio, and Length of Contact

**Length of action** Z is the distance along the line of action over which a tooth pair is in
contact. It runs from where the addendum circle of the driven gear crosses the line of action
to where the addendum circle of the driver crosses it:

    Z = sqrt(r_a1^2 - r_b1^2) + sqrt(r_a2^2 - r_b2^2) - C*sin(phi)

where r_a = addendum (outside) radius, r_b = base radius = r*cos(phi).

**Contact ratio** m_c (also m_p) = average number of tooth pairs in contact:

    m_c = Z / p_b      where  p_b = base pitch = p*cos(phi) = pi*m*cos(phi)

**Requirement:** m_c > 1 (otherwise one tooth pair disengages before the next engages — motion
stalls/impacts). In practice m_c >= 1.2 for smooth running; 1.4–1.7 is typical for spur gears.
A contact ratio of, say, 1.6 means "1 pair always in contact, 2 pairs 60% of the time."

### 1.7 Interference and Undercutting

**Interference** occurs when the involute portion of one tooth tries to contact the
**non-involute** (fillet/flank) portion of the mating tooth, below its base circle. Contact at
those points is not conjugate — it gouges. Interference happens when the addendum circle of a
gear extends past the **interference point** (the tangent point of the line of action on the
mating base circle).

- It is worst for a **small pinion meshing with a large gear** (or with a rack).
- **Undercutting** is the manufacturing consequence: a generating cutter (hob) removes the
  interfering material at the tooth root, leaving an undercut that weakens the tooth and
  shortens the contact region.

**Minimum number of teeth to avoid interference.** For a pinion meshing with a rack (worst
case), standard full-depth teeth:

    N_min = 2 / sin^2(phi)

  - phi = 14.5°  =>  N_min = 32
  - phi = 20°    =>  N_min = 18  (commonly rounded; 17 often quoted/used)
  - phi = 25°    =>  N_min = 12

For a pinion (N_p) meshing with a gear of N_g teeth, the more general limit is:

    N_p >= 2*k*(1 + sqrt(1 + (N_g/N_p)*(N_g/N_p + 2)*sin^2(phi))) / ((N_g/N_p)*sin^2(phi))
        ... with k = 1 for full-depth teeth.

**Remedies for interference:** use a larger pressure angle; use fewer teeth on the gear; use
**stub teeth** (shorter addendum, k = 0.8); use **profile-shifted (corrected) gears** where the
cutter is moved out for the pinion and in for the gear.

### 1.8 Backlash

**Backlash** B = (tooth space) - (tooth thickness), measured along the pitch circle. It is the
play that lets gears turn freely, allows for lubrication film, thermal expansion, and
manufacturing tolerance. Zero backlash => binding.

- Backlash is created by cutting teeth slightly thin or by running gears at a slightly larger
  center distance than nominal.
- Increasing center distance by delta_C increases backlash by approximately
  B = 2*delta_C*tan(phi).
- Backlash causes **lost motion** on reversal — a problem in positioning systems (CNC,
  robotics), addressed by anti-backlash split gears or preloaded duplex worm sets.

### 1.9 Helical, Bevel, and Worm Gears (brief)

**Helical gears.** Teeth are cut on a helix at the **helix angle** psi. Advantages: gradual
tooth engagement => quieter, smoother, higher load capacity than spur. Disadvantage: produces
an **axial thrust** load (resolved by thrust bearings or canceled with double-helical /
herringbone gears). Key relations:

    p_n = p_t * cos(psi)            (normal vs transverse circular pitch)
    m_n = m_t * cos(psi)            (normal vs transverse module)
    phi_n related to phi_t by:  tan(phi_n) = tan(phi_t) * cos(psi)
    Transverse plane behaves like a spur gear with module m_t.
    Equivalent (virtual) spur tooth count for strength:  N_e = N / cos^3(psi)

**Bevel gears.** Transmit motion between **intersecting shafts** (commonly 90°). Teeth lie on a
cone (the pitch cone). Pitch cone angles gamma_1, gamma_2 satisfy tan(gamma_1) = N_1/N_2 for a
90° shaft angle. Velocity ratio still = N_driving / N_driven. **Spiral bevel** gears are the
helical analog — curved teeth, smoother. **Hypoid** gears are offset (non-intersecting) bevels.

**Worm gears.** A **worm** (a screw) drives a **worm gear (worm wheel)**. The worm is treated as
a gear whose number of teeth equals its **number of thread starts** — a single-start worm acts
like a **1-tooth gear**, a double-start like a 2-tooth gear, etc.

  - Number of worm "teeth": z_w = number of thread starts (1, 2, 3, 4, ...)
  - Velocity ratio: VR = omega_gear / omega_worm = z_w / N_gear  => very large reductions
    (e.g. single-start worm with a 40-tooth wheel gives 40:1 in one mesh).
  - **Lead** L = z_w * p_axial; **lead angle** lambda satisfies tan(lambda) = L / (pi * d_worm).
  - **Self-locking** worm drive: the gear cannot back-drive the worm when the lead angle is
    small enough — approximately when lambda < arctan(mu), i.e. tan(lambda) < mu (friction
    coefficient). Used in hoists and where holding load without a brake is required.
  - Worm drives are compact and quiet but have **low efficiency** (high sliding friction),
    typically 50–90%, dropping further as they approach self-locking.

---

## PART 2 — GEAR TRAINS

A **gear train** is a set of meshing gears arranged to transmit motion between an input and an
output shaft, producing a desired speed ratio, torque ratio, or direction. The single most
important quantity is the **train value** (or **train ratio**) e:

    e = (speed of last/output gear) / (speed of first/input gear)
      = omega_L / omega_F

For a train of fixed-axis meshes, the train value is built from the individual mesh ratios.
**Magnitude** = (product of driving tooth counts) / (product of driven tooth counts) for each
mesh — see the careful statement below. **Sign** = (-1)^(number of external meshes).

### 2.1 Simple Gear Train (one gear per shaft)

Every shaft carries exactly one gear. Gears 1 — 2 — 3 — ... — n in series, each meshing with
the next.

Apply the velocity ratio mesh by mesh:

    omega_2/omega_1 = -N_1/N_2
    omega_3/omega_2 = -N_2/N_3
    omega_4/omega_3 = -N_3/N_4   ... etc.

Multiply them — **all intermediate tooth counts cancel**:

    e = omega_n / omega_1 = (-1)^(n-1) * (N_1 / N_n)

**Key insight: intermediate gears do not affect the magnitude of the speed ratio.** A gear in
the middle of a simple train is called an **idler**.

**Idler gears — what they do:**

- An idler **does not change the speed-ratio magnitude** (it appears in both a numerator and a
  denominator and cancels).
- An idler **does change direction** — each idler adds one external mesh, flipping the output
  sense. One idler makes input and output rotate the **same** way.
- Idlers are also used to **bridge a large center distance** without one giant gear, and to
  provide a take-off point for a third shaft.

### 2.2 Compound Gear Train

At least one shaft carries **two (or more) gears keyed together** (a "compound gear") that
rotate as a unit. Now the intermediate tooth counts do **not** all cancel — this is how a
compound train achieves a large ratio in a small package.

**General formula:**

    e = omega_L / omega_F = (-1)^q * (product of teeth on all DRIVING gears)
                                     ---------------------------------------
                                     (product of teeth on all DRIVEN gears)

where q = number of external meshes. Equivalently:

    Train value = (product of driver tooth counts) / (product of driven tooth counts)

**Worked pattern — two-stage compound reducer.** Input gear A (N_A) meshes with gear B (N_B);
B is compounded with gear C (N_C) on the same shaft; C meshes with output gear D (N_D).

    Stage 1:  omega_B/omega_A = -N_A/N_B       (B and C share a shaft: omega_C = omega_B)
    Stage 2:  omega_D/omega_C = -N_C/N_D
    Overall:  e = omega_D/omega_A = (-N_A/N_B)*(-N_C/N_D) = (N_A * N_C)/(N_B * N_D)

Two external meshes => sign = (-1)^2 = + => input and output turn the same direction.

Drivers here are A and C; driven are B and D — matches the general formula.

### 2.3 Reverted Gear Train

A **reverted** train is a compound train whose **input and output shafts are coaxial** (on the
same axis line). Common in clocks, lathes, automotive transmissions (the "direct-drive" feel),
and where packaging demands the output come back out along the input axis.

Because input and output are coaxial, the **center distance of stage 1 must equal the center
distance of stage 2**. With gears A–B in stage 1 and C–D in stage 2:

    C_AB = C_CD
    (d_A + d_B)/2 = (d_C + d_D)/2
    => m_AB*(N_A + N_B) = m_CD*(N_C + N_D)

If the same module is used throughout (m_AB = m_CD), the constraint reduces to:

    N_A + N_B = N_C + N_D

This **couples the two stages**: you cannot pick all four tooth counts freely. The design
procedure is: (1) pick the overall ratio e = (N_A*N_C)/(N_B*N_D); (2) split it into two stage
ratios; (3) choose tooth counts that hit those ratios **and** satisfy the center-distance
constraint, while keeping each pinion above N_min for interference and each count an integer.

### 2.4 Sign / Direction Convention

- Each **external** mesh reverses sense: contributes a factor of (-1).
- Each **internal** mesh (pinion inside a ring gear) preserves sense: factor of (+1).
- Overall sign of e = (-1)^(number of external meshes).
- Positive e: output rotates the **same** way as input. Negative e: **opposite**.
- For 3-D trains (bevel, worm, crossed-helical), the "sign" is ambiguous — track direction with
  a sketch and the right-hand rule instead of blindly applying (-1)^q.

### 2.5 Worm Gear Drives in Trains

Treat the worm as a gear with z_w teeth (= number of thread starts). A worm–wheel mesh in a
train contributes a ratio of z_w / N_wheel — typically a very large single-stage reduction.

    e_wormstage = omega_wheel / omega_worm = z_w / N_wheel

Worm stages are normally **non-reversible in direction sense by the usual (-1)^q rule** — use a
sketch. They are frequently chosen specifically for the **self-locking** property (Section 1.9):
the load on the wheel cannot back-drive the worm, so the train holds position without a brake.

### 2.6 Belt, Chain, and Sprocket Drives in Trains

Belt and chain drives behave like gear meshes for ratio purposes, with two differences:

- Ratio is set by **pulley/sprocket pitch diameters** (belts) or **tooth counts** (chains,
  toothed/timing belts):

      omega_driven / omega_driver = D_driver / D_driven = N_driver / N_driven

- **Direction:** an open belt/chain keeps both shafts turning the **same** way (like an internal
  mesh, factor +1); a **crossed belt** reverses the driven shaft.
- Flat/V-belts can **slip** (ratio not perfectly constant; acts as an overload "fuse"); chains
  and timing belts do **not** slip (positive drive, exact ratio). Belts/chains also span large
  center distances cheaply where a gear train would be bulky.

When a belt or chain stage appears inside a larger gear train, fold its ratio into the train
value just like any other stage.

### 2.7 Epicyclic (Planetary) Gear Trains

In an **epicyclic** or **planetary** gear train, the **axis of at least one gear moves** — that
gear (the **planet**) rotates about its own axis *and* revolves around a central axis. This is
the source of all the difficulty: you cannot just multiply mesh ratios, because the planet's
center is itself moving.

**Terminology:**

| Part | Role |
|---|---|
| **Sun gear** | Central gear, fixed axis, on the central axis |
| **Planet gear(s)** | Mesh with the sun (and usually the ring); axis revolves around the central axis. Often 2–4 planets for load sharing — kinematically they all behave the same, so analyze one |
| **Ring gear (annulus)** | Internal gear surrounding the planets; meshes with the planets internally |
| **Arm / carrier / spider** | Rigid member that carries the planet axes; rotates about the central axis. **The arm is a kinematic member, not a gear** — forgetting it is the #1 student error |

An epicyclic train has **2 degrees of freedom**: you must specify **two** of the four motions
(sun, ring, arm, and one input/output) to determine the rest. Fix one member and drive another
=> the third is the output.

#### 2.7.1 Method 1 — Tabular (Superposition) Method

Idea: any motion of the train = (rigid-body rotation of the whole assembly) + (motion with the
arm held fixed). Build it in three rows.

**Step-by-step procedure:**

1. **Row 1 — Arm fixed, give the first gear +1 revolution.** With the arm locked, the train is
   an ordinary fixed-axis train. Compute each other gear's revolutions from the tooth-count
   ratios (with correct signs: external mesh flips sign, internal mesh keeps it). Record a
   number in every column (sun, planet, ring, arm). The arm column is 0 in this row.
2. **Row 2 — Arm fixed, give the first gear +x revolutions.** Multiply Row 1 by x. (x stays
   symbolic for now.)
3. **Row 3 — Lock the whole train and give everything +y revolutions.** Add y to every column,
   **including the arm**. This is the rigid-body term.
4. **Total row = Row 2 + Row 3.** Every column is now (something)*x + y.
5. **Apply the two known conditions** (e.g., "ring is fixed" => its total = 0; "arm runs at
   100 rpm" => arm total = 100). Two equations, two unknowns (x, y). Solve.
6. **Back-substitute** x and y into the column you want (usually the output gear or the sun).

**Tabular template** (sun S, planet P, ring R, arm; S meshes with P externally, P meshes with R
internally):

| Operation | Sun (S) | Planet (P) | Ring (R) | Arm |
|---|---|---|---|---|
| 1. Arm fixed, +1 to Sun | +1 | -N_S/N_P | -N_S/N_P * (-N_P/N_R) = +N_S/N_R | 0 |
| 2. Arm fixed, +x to Sun | +x | -x*N_S/N_P | +x*N_S/N_R | 0 |
| 3. Whole train +y | +y | +y | +y | +y |
| **Total** | **x + y** | **y - x*N_S/N_P** | **y + x*N_S/N_R** | **y** |

Note the ring-column sign: Sun→Planet is external (-), Planet→Ring is internal (+), so the net
Sun→Ring sign through the planet is (-)*(+) = (-)... but because the planet is an idler between
sun and ring, the magnitude is N_S/N_R and you must carry the sign carefully. (A clean check:
for a fixed carrier, sun and ring of a simple sun-planet-ring set rotate in **opposite**
directions, so omega_R/omega_S = -N_S/N_R. The table above writes the ring entry as +N_S/N_R
following one common sign bookkeeping; **always verify direction against a physical sketch** —
this is exactly where students lose points.)

#### 2.7.2 Method 2 — Formula Method (Train Value Equation)

Idea: subtract the arm's motion from everything — i.e., work in the **reference frame of the
arm**. In that frame the planet axes are stationary, so the train is an ordinary fixed-axis
train and the ordinary train-value rule applies.

**The train value equation:**

    (omega_last - omega_arm) / (omega_first - omega_arm) = e

where e is the **fixed-carrier train value** — the train value you would compute if the arm
were held still, with its proper sign:

    e = +/- (product of teeth on driving gears) / (product of teeth on driven gears)

evaluated from the "first" gear to the "last" gear through the gear path **excluding the arm**.

**Step-by-step procedure:**

1. **Choose "first" and "last" gears.** Pick the two gears whose motions you know or want
   (often: first = sun, last = ring; or first = sun, last = planet). Be consistent for the
   rest of the problem.
2. **Compute e (fixed-carrier train value).** Hold the arm fixed in your mind, trace the mesh
   path from first to last, multiply driving/driven tooth ratios, and attach the sign:
   (-1)^(number of external meshes) along that path. Internal (ring) meshes do not flip sign.
3. **Write the train value equation:** (omega_L - omega_arm)/(omega_F - omega_arm) = e.
4. **Insert the two known conditions** (a fixed member has omega = 0; a driven input has its
   given omega). The arm speed omega_arm may itself be one unknown.
5. **Solve algebraically** for the requested speed.

**Worked pattern — sun input, ring fixed, arm output (classic reduction):**
Let first = sun S, last = ring R. Fixed-carrier value e = -N_S/N_R (sun and ring counter-rotate
when carrier is held).

    (omega_R - omega_arm) / (omega_S - omega_arm) = -N_S/N_R
    Ring fixed => omega_R = 0:
    (0 - omega_arm) / (omega_S - omega_arm) = -N_S/N_R
    -omega_arm * N_R = -N_S * (omega_S - omega_arm)
    -omega_arm * N_R = -N_S*omega_S + N_S*omega_arm
    omega_arm * (N_S + N_R) = N_S * omega_S
    => omega_arm / omega_S = N_S / (N_S + N_R)

So a sun-driven, ring-fixed planetary gives a reduction of (N_S + N_R)/N_S — a compact, coaxial,
high-ratio reducer. (Also note N_R = N_S + 2*N_P from the geometry, useful as a check.)

**Geometry constraint (always true for a sun–planet–ring set):**

    N_R = N_S + 2*N_P        (concentricity: sun radius + 2*planet radius = ring radius)

Also, for equally spaced planets to assemble, (N_S + N_R) must be divisible by the number of
planets.

#### 2.7.3 Tabular vs. Formula — When to Use Which

| Aspect | Tabular method | Formula method |
|---|---|---|
| Best for | Beginners; trains with several compound planets; when you want every member's speed | Quick answers; standard sun/ring/arm sets; symbolic design work |
| Bookkeeping | Visual, hard to lose a member | Compact, but easy to get the sign of e wrong |
| Risk | Sign errors propagating across rows | Picking inconsistent "first"/"last"; mis-signing e |
| Reliability check | Both should agree — solve once each way to verify a hard problem |

### 2.8 Step-by-Step Solution Procedures by Train Type

**Simple train:** (1) Identify input and output. (2) Count external meshes q. (3)
e = (-1)^(q) * N_input/N_output. (4) Idlers cancel — ignore them in magnitude. (5)
omega_out = e * omega_in.

**Compound train:** (1) Identify every shaft; mark which gears are keyed together (compound
sets rotate together — same omega). (2) List drivers and driven for each mesh. (3) Magnitude =
(product of driver N) / (product of driven N). (4) Sign = (-1)^(external meshes). (5)
omega_out = e * omega_in.

**Reverted train:** (1) Do the compound-train analysis for the ratio. (2) Additionally enforce
the center-distance constraint m_AB(N_A+N_B) = m_CD(N_C+N_D). (3) Iterate tooth counts until
ratio, integer-tooth, interference-minimum, and center-distance constraints are all satisfied.

**Worm in a train:** (1) Worm teeth = thread starts z_w. (2) Worm-stage ratio = z_w/N_wheel.
(3) Fold into the overall train value. (4) Determine direction from a sketch. (5) Check
self-locking if the load can back-drive.

**Belt/chain in a train:** (1) Stage ratio = D_driver/D_driven (or N_driver/N_driven for
toothed). (2) Open drive = same direction; crossed = reversed. (3) Fold into train value.

**Epicyclic train:** (1) Identify sun, planet(s), ring, arm — explicitly find the arm. (2)
Confirm it has 2 DOF; identify the two given conditions. (3) Pick tabular or formula method.
(4) For formula: compute fixed-carrier e with correct sign, write
(omega_L - omega_arm)/(omega_F - omega_arm) = e, substitute, solve. (5) For tabular: build the
three rows, total, apply conditions, solve for x and y, back-substitute. (6) Sanity-check with
the geometry constraint N_R = N_S + 2*N_P and against a physical-direction sketch.

### 2.9 Common Student Pitfalls (Gear Trains)

- **Idler confusion:** thinking an idler changes the speed ratio. It does not — it only changes
  direction. Conversely, forgetting that each idler flips the output direction.
- **Sign errors:** miscounting external vs. internal meshes; forgetting that a ring (internal)
  mesh does **not** flip the sign.
- **Forgetting the arm in a planetary train:** treating an epicyclic train as a fixed-axis
  train and just multiplying mesh ratios. The planet's moving axis makes that wrong.
- **Mixing up driving vs. driven:** the formula is driver-product over driven-product; swapping
  them inverts the ratio.
- **Compound-set errors:** forgetting that two gears keyed to the same shaft have the **same**
  angular speed (not the same tooth count, not a 1:1 mesh).
- **Reverted trains:** solving for the ratio but ignoring the center-distance constraint, then
  getting tooth counts that physically won't fit coaxially.
- **Inconsistent "first/last" in the formula method:** changing which gear is "first" partway
  through, or using a sign of e inconsistent with that choice.
- **Units / rpm vs. rad/s:** the kinematic equations are ratios so units cancel — but be
  consistent, and convert at the end if the answer is wanted in rpm or rad/s.
- **Assuming the answer's direction:** always confirm rotation sense with a quick sketch,
  especially for worm, bevel, and internal-gear stages where (-1)^q is unreliable.

---

## PART 3 — CAM DESIGN / PROFILE GEOMETRY

A **cam** is a shaped member (usually rotating) that imparts a prescribed motion to a
**follower** through direct contact. Cams convert rotary input into an *arbitrary* follower
motion — far more flexible than a linkage, which is why they run valve trains, indexing
mechanisms, automated machinery, and printers.

### 3.1 Cam-and-Follower Terminology

| Term | Definition |
|---|---|
| **Base circle** | Smallest circle tangent to the cam profile, centered on the cam axis. Sets the minimum cam size; everything is measured from it |
| **Trace point** | A reference point on the follower used to generate the cam profile. For a **knife-edge** follower it is the knife edge; for a **roller** follower it is the **center of the roller** |
| **Pitch curve** | Path of the trace point relative to the cam (the locus of the trace point as the cam rotates). For a knife-edge follower the pitch curve = cam profile; for a roller follower the cam profile is the pitch curve **offset inward by the roller radius** |
| **Prime circle** | Smallest circle tangent to the **pitch curve**, centered on the cam axis. prime circle radius = base circle radius + roller radius |
| **Pressure angle** | Angle between the **normal to the pitch curve** at the contact point and the **direction of follower motion**. Large pressure angle => large side thrust on the follower => jamming. Keep it small (rule of thumb: <= 30° for translating followers) by enlarging the base circle |
| **Pitch point** | Point on the pitch curve where the pressure angle is maximum |
| **Lift / stroke / rise** | Maximum follower displacement, h (also denoted L or S_max) |
| **Cam angle** | theta, the angular position of the cam (the independent variable) |
| **Segment angle** | beta, the cam rotation over which a particular event (rise, dwell, return) occurs |
| **Dwell** | Period during which the follower is stationary while the cam rotates |
| **Transition point** | Point on the profile where motion changes character (rise→dwell, etc.) — where discontinuities in v, a, j can appear |

### 3.2 Follower Classifications

**By the shape of the contacting surface:**
- **Knife-edge** — simple, exact trace point; high contact stress and wear; rarely used in practice.
- **Roller** — a rotating roller reduces friction and wear; most common. Trace point = roller
  center; cam profile is offset from the pitch curve by the roller radius.
- **Flat-face (mushroom)** — flat follower face; cannot follow a concave cam profile; produces
  a side load but no pressure-angle jamming problem; common in automotive valve trains.
- **Spherical-face** — compromise between roller and flat-face.

**By the motion of the follower:**
- **Translating (reciprocating)** — slides in a straight line.
- **Oscillating (pivoted)** — swings about a pivot.

**By the line of follower motion:**
- **Radial (in-line)** — follower motion line passes through the cam axis.
- **Offset** — follower motion line is offset from the cam axis (used to manage the pressure
  angle / force direction).

**By how contact is maintained:**
- **Force-closed** — a spring (or gravity) holds the follower on the cam. Can lose contact
  ("follower jump") at high speed if inertia exceeds the spring force.
- **Form-closed (positive-drive)** — a groove or conjugate pair captures the follower; contact
  is guaranteed but the mechanism is heavier and needs clearance.

### 3.3 The Displacement Diagram

The **displacement diagram** plots follower displacement s on the vertical axis against cam
angle theta (or time t, since theta = omega*t at constant cam speed) on the horizontal axis,
over one full revolution. It is the master design document: the cam profile is generated *from*
it.

From s(theta), the kinematic quantities follow by differentiation. With cam angular speed omega
(rad/s), and using primes for d/d(theta):

    velocity:      v = ds/dt = omega * (ds/d theta)             = omega * s'
    acceleration:  a = dv/dt = omega^2 * (d^2 s/d theta^2)      = omega^2 * s''
    jerk:          j = da/dt = omega^3 * (d^3 s/d theta^3)      = omega^3 * s'''

A typical cycle is **RDFD**: Rise — Dwell — Fall (return) — Dwell. The follower must have
**matched displacement, velocity, and (ideally) acceleration at every transition point**, or
inertia forces spike.

### 3.4 The Fundamental Law of Cam Design

> **Fundamental Law of Cam Design:** The cam function must be **continuous in displacement and
> velocity, and continuous in acceleration, across the entire cycle (including transitions to
> and from dwells).**

Reason: a discontinuity in **acceleration** produces an **infinite jerk** — a step in force —
which causes vibration, noise, and impact wear. A discontinuity in **velocity** would imply
infinite acceleration (infinite force) — never acceptable. Hence good motion programs match
s and v (mandatory) and a (strongly preferred) at every boundary.

### 3.5 Standard Follower Motion Programs

For a **rise of total lift h over cam-segment angle beta**, let the segment-local angle be
theta (0 <= theta <= beta). Equations below give s, v, a, j. (For the return, mirror: replace
s by (h - s), etc., or substitute theta -> (beta - theta).)

| Program | s(theta) | v = omega*s' | a = omega^2*s'' | Acceleration / jerk character |
|---|---|---|---|---|
| **Uniform velocity** (constant velocity) | s = h*(theta/beta) | v = omega*h/beta (constant) | a = 0 in the interior | a is **infinite** at both ends (step in v). Unusable as-is at speed; needs blended ends |
| **Uniform / constant acceleration (parabolic)** | 1st half: s = 2h*(theta/beta)^2 ; 2nd half: s = h - 2h*(1 - theta/beta)^2 | piecewise-linear, peaks at mid-stroke v_max = 2h*omega/beta | a = +4h*omega^2/beta^2 (1st half), -4h*omega^2/beta^2 (2nd half) — **lowest possible peak acceleration** | a is a step function => **finite but discontinuous** => infinite jerk at the ends and the midpoint |
| **Simple harmonic motion (SHM)** | s = (h/2)*(1 - cos(pi*theta/beta)) | v = (pi*h*omega)/(2*beta) * sin(pi*theta/beta) | a = (pi^2*h*omega^2)/(2*beta^2) * cos(pi*theta/beta) | a is smooth (cosine) **but nonzero at the ends** => still a step in a when joining a dwell => infinite jerk at rise/dwell boundaries |
| **Cycloidal motion** | s = h*[ theta/beta - (1/(2*pi))*sin(2*pi*theta/beta) ] | v = (h*omega/beta)*[1 - cos(2*pi*theta/beta)] | a = (2*pi*h*omega^2/beta^2)*sin(2*pi*theta/beta) | a is sinusoidal **and zero at both ends** => smoothly matches a dwell => **finite jerk everywhere**. The preferred high-speed program |

**Peak-value comparison (rise h over beta), useful for design selection:**

| Program | v_max | a_max |
|---|---|---|
| Parabolic (const accel) | 2.000 * h*omega/beta | 4.000 * h*omega^2/beta^2 |
| Simple harmonic | 1.571 * h*omega/beta (= pi/2) | 4.935 * h*omega^2/beta^2 (= pi^2/2) |
| Cycloidal | 2.000 * h*omega/beta | 6.283 * h*omega^2/beta^2 (= 2*pi) |

### 3.6 Rationale — Why SHM and Cycloidal Are Preferred Over the Simpler Programs

- **Uniform velocity** has infinite acceleration at the ends (the velocity jumps from 0 to a
  finite value instantly). Unacceptable except for slow, lightly loaded cams or with blended
  transitions.
- **Parabolic (constant acceleration)** gives the *theoretically lowest peak acceleration*, but
  its acceleration is a **step function** — discontinuous at the start, midpoint, and end =>
  **infinite jerk** at those points => impact, noise, vibration. Acceptable at low/moderate
  speed only.
- **SHM** has a smooth (cosine) acceleration curve, so it is far better than parabolic — but
  the cosine is **nonzero at the ends of the segment**. When an SHM rise meets a dwell (where
  a = 0), there is still a sudden **step in acceleration** => infinite jerk at that junction.
  Fine when SHM segments meet other moving segments, problematic against dwells.
- **Cycloidal** has an acceleration that is a full sine wave over the segment — it is **zero at
  both ends**. So a cycloidal rise blends into a dwell (a = 0) with **no step in acceleration**:
  jerk stays **finite everywhere**. This continuity of acceleration is exactly the Fundamental
  Law of Cam Design, which is why cycloidal motion is the standard choice for **high-speed,
  high-inertia cams** despite having the highest peak acceleration of the three smooth programs.

Higher-order polynomial programs (e.g., the **3-4-5 polynomial** and **4-5-6-7 polynomial**)
generalize this idea: choose polynomial coefficients so that s, v, **and a** (and sometimes j)
are all zero at both ends — giving even smoother behavior than cycloidal when needed.

### 3.7 Cam Profile Layout

**Graphical layout (kinematic inversion).** "Invert" the mechanism: hold the cam stationary and
walk the follower around it backward.
1. Draw the base circle (and prime circle if a roller follower).
2. Divide the cam rotation into intervals (e.g., every 15° or 30°), matching the displacement
   diagram divisions.
3. For each interval, measure the follower displacement s from the displacement diagram and
   step the **trace point** out from the prime circle by that amount, *in the direction
   opposite cam rotation*.
4. Mark all trace-point positions — this locus is the **pitch curve**.
5. For a knife-edge follower, the pitch curve **is** the cam profile. For a roller follower,
   draw the cam profile as the **inner envelope** of roller circles centered on the pitch
   curve (offset the pitch curve inward by the roller radius). For an offset or oscillating
   follower, account for the offset / pivot geometry in step 3.

**Analytical layout.** Express the cam profile in polar coordinates (r, theta) directly from
the chosen motion program: for a radial knife-edge follower, r(theta) = R_base + s(theta). For
roller followers, compute the pitch curve r_pitch(theta) = R_prime + s(theta), then offset
normal-inward by the roller radius to get the manufacturable profile. CNC machining and
simulation use the analytical form.

### 3.8 Common Student Pitfalls (Cams)

- **Confusing base circle, prime circle, and pitch curve.** Base circle => smallest circle on
  the *cam profile*; prime circle => smallest circle on the *pitch curve*; prime = base +
  roller radius. The displacement is added to the **prime** circle, not the base circle, for a
  roller follower.
- **Cutting the profile on the pitch curve for a roller follower.** The pitch curve is the
  **roller-center** path; the actual cam surface is offset inward by the roller radius.
- **Ignoring the jerk / acceleration discontinuity.** Picking parabolic or even SHM against a
  dwell because the equations are simpler, then getting a noisy, short-lived cam.
- **Wrong direction of profile generation.** In graphical inversion you step the follower in
  the direction **opposite** to cam rotation.
- **Letting the pressure angle get too large.** Forgetting that a small base circle => large
  pressure angle => the follower jams. Fix: enlarge the base circle or offset the follower.
- **Not matching boundary conditions** of s and v (and ideally a) at every transition between
  segments — produces velocity/acceleration spikes.
- **Mixing per-time and per-angle derivatives.** s' = ds/d theta is not v; multiply by omega
  (and omega^2 for a, omega^3 for j). Only valid as written when omega is constant.

---

## PART 4 — POWER SCREWS / TRANSLATION SCREWS

A **power screw** (translation screw, lead screw) converts rotary motion into linear motion to
move a load — screw jacks, vises, presses, lathe lead screws, linear actuators, C-clamps. It is
essentially an inclined plane wrapped around a cylinder.

### 4.1 Screw Geometry and Terminology

| Term | Symbol | Definition |
|---|---|---|
| **Pitch** | p | Axial distance between corresponding points on adjacent threads |
| **Lead** | L | Axial advance of the nut (or screw) per **one full revolution** |
| **Number of starts (threads)** | n | Number of independent helical threads. **Single-start: L = p. Multiple-start: L = n*p** |
| **Mean (pitch) diameter** | d_m | Average of major and minor diameters; the diameter at which thread forces are taken to act |
| **Lead angle** | lambda | Helix angle of the thread at the mean diameter, measured from a plane perpendicular to the axis: tan(lambda) = L / (pi*d_m) |
| **Thread (flank) half-angle** | alpha_n | Half the included thread angle, in the normal plane. Square thread: alpha_n = 0; ACME: alpha_n = 14.5° |
| **Coefficient of friction** | mu | Between screw and nut threads. mu_c = collar friction coefficient |
| **Collar / thrust** | — | The bearing surface that takes the axial load reaction; contributes additional friction torque |

**Single vs. multiple threads.** A multiple-start screw advances faster (larger L for the same
p), giving more linear travel per turn and **higher efficiency** (larger lead angle), at the
cost of being **less likely to self-lock** and providing **less mechanical advantage**.

### 4.2 Torque to Raise the Load (lifting / tightening)

Model: a force pushes a block up an inclined plane of inclination lambda, against the load W
and friction. Wrapping the plane around the cylinder, the torque applied at radius d_m/2 to
**raise** load W is:

**Square thread (alpha_n = 0):**

    T_raise = (W*d_m/2) * (L + pi*mu*d_m) / (pi*d_m - mu*L)

Equivalently, with tan(lambda) = L/(pi*d_m):

    T_raise = (W*d_m/2) * (tan(lambda) + mu) / (1 - mu*tan(lambda))
            = (W*d_m/2) * tan(lambda + phi_f)        where tan(phi_f) = mu (friction angle)

**ACME / V thread (half-angle alpha_n != 0):** the thread-angle increases the effective normal
force, so replace mu by mu/cos(alpha_n):

    T_raise = (W*d_m/2) * (L + pi*mu*d_m*sec(alpha_n)) / (pi*d_m - mu*L*sec(alpha_n))

**Collar friction** adds a separate term (collar carries the thrust on a mean collar radius
r_c, or mean diameter d_c):

    T_collar = mu_c * W * d_c / 2

    T_total_raise = T_raise + T_collar

### 4.3 Torque to Lower the Load (lowering / loosening)

Friction now acts **up** the plane (opposing the descent), so signs flip:

**Square thread:**

    T_lower = (W*d_m/2) * (pi*mu*d_m - L) / (pi*d_m + mu*L)
            = (W*d_m/2) * (mu - tan(lambda)) / (1 + mu*tan(lambda))
            = (W*d_m/2) * tan(phi_f - lambda)

**ACME / V thread:**

    T_lower = (W*d_m/2) * (pi*mu*d_m*sec(alpha_n) - L) / (pi*d_m + mu*L*sec(alpha_n))

Add T_collar again for total lowering torque.

**Sign interpretation of T_lower:**
- **T_lower > 0** => positive torque must be applied to lower the load => the screw is
  **self-locking** (it will not back-drive on its own).
- **T_lower <= 0** => the load would drive the screw down by itself (an actual *restraining*
  torque is needed to hold it) => the screw is **not self-locking** (overhauling).

### 4.4 Self-Locking Condition

A power screw is **self-locking** when it cannot be back-driven by the axial load — i.e., the
load alone cannot make it turn. From T_lower >= 0:

**Square thread:**   self-locking when   mu >= tan(lambda)    (equivalently lambda <= phi_f)

**ACME / V thread:** self-locking when   mu >= tan(lambda)*cos(alpha_n)
                     (equivalently mu*sec(alpha_n) >= tan(lambda))

In words: **self-locking requires the friction coefficient to be at least the tangent of the
lead angle.** Small lead angle (fine pitch, single start) => self-locking; large lead angle
(coarse / multiple start) => overhauling. Self-locking is essential for screw jacks and
C-clamps (the load must stay put with no holding torque) but wastes energy — efficiency of a
self-locking screw is always below 50%.

### 4.5 Screw Efficiency

Efficiency = (work output) / (work input) per revolution. Work output raising W through one
lead L is W*L; work input is 2*pi*T_raise (excluding collar, or include collar in T):

    eta = (W*L) / (2*pi*T_raise)

**Square thread, no collar friction**, this reduces to a clean form:

    eta = tan(lambda) / tan(lambda + phi_f)        where tan(phi_f) = mu

Key facts:
- eta increases with lead angle up to an optimum, then falls; max efficiency occurs near
  lambda = 45° - phi_f/2.
- **A self-locking screw always has eta < 50%.** (At the self-locking limit lambda = phi_f,
  eta = tan(lambda)/tan(2*lambda) < 0.5.)
- **Square threads are the most efficient** (alpha_n = 0). **ACME threads** are slightly less
  efficient (the 14.5° half-angle raises the effective friction by sec(alpha_n)) but are easier
  to manufacture, stronger at the root, and allow a split nut for wear take-up — the usual
  practical choice. **Buttress threads** are used when load is one-directional.

### 4.6 Common Student Pitfalls (Power Screws)

- **Confusing pitch and lead.** They are equal **only for single-start** threads. For an
  n-start screw, L = n*p — use **lead** in every torque/efficiency formula, never pitch.
- **Forgetting collar friction.** T_collar is often comparable to thread torque; omit it and
  the required input torque is badly underestimated.
- **Using the raise formula to lower** (or vice versa) — friction reverses direction; the sign
  inside the bracket changes.
- **Dropping sec(alpha_n) for ACME threads** — treating an ACME screw as a square thread
  underestimates friction and torque.
- **Misreading the sign of T_lower** — a negative T_lower does not mean "no torque," it means a
  *restraining* torque is needed (not self-locking).
- **Assuming high efficiency for a self-locking screw** — impossible; eta < 50% always when
  self-locking.

---

## PART 5 — MECHANICAL ADVANTAGE

### 5.1 Definition

**Mechanical advantage (MA)** is the factor by which a machine multiplies the input force:

    MA = (output force) / (input force) = F_out / F_in

The companion quantity is the **velocity ratio (VR)** — sometimes called movement ratio:

    VR = (distance moved by input) / (distance moved by output)
       = (input velocity) / (output velocity)

For a perfect (lossless) machine, energy in = energy out, so F_in * d_in = F_out * d_out, which
gives the **Ideal Mechanical Advantage**:

    IMA = VR     (ideal: MA equals the velocity ratio)

### 5.2 The Master Relationship: MA = VR * efficiency

Real machines lose energy to friction. Efficiency eta = (work out)/(work in) = (F_out*d_out) /
(F_in*d_in). Rearranging:

    AMA (actual MA) = F_out/F_in = eta * (d_in/d_out) = eta * VR

> **MA = VR * eta.** The actual mechanical advantage is the ideal mechanical advantage
> (= velocity ratio) reduced by the efficiency.

Also: eta = AMA / IMA = (actual MA) / (velocity ratio). For an ideal machine eta = 1 and
MA = VR; for any real machine MA < VR.

### 5.3 Mechanical Advantage of Common Machines

**Lever.** For a lever with effort arm a and load arm b about the fulcrum:

    IMA = a / b      (effort-arm length / load-arm length)

Levers are very efficient (eta ~ 1), so AMA ~ IMA. Classes: 1st-class (fulcrum between effort
and load — can give MA >1 or <1), 2nd-class (load between — MA always >1, e.g. wheelbarrow),
3rd-class (effort between — MA always <1, trades force for speed/range, e.g. forearm, tweezers).

**Gear train.** The velocity ratio is the train value's reciprocal magnitude; the ideal MA
equals it:

    IMA = N_driven / N_driving  (for a single reduction)
        = (product of driven teeth) / (product of driving teeth)  (for a compound train)
    AMA = eta_train * IMA

A speed reducer (output slower than input) has MA > 1: it multiplies torque/force. Typical
spur-gear-stage efficiency ~ 97–99%; worm-gear stage 50–90%.

**Wheel and axle.** IMA = R_wheel / r_axle.

**Pulley system (block and tackle).** IMA = number of rope sections supporting the load
(= number of supporting strands). AMA = eta * (that count); friction in the sheaves makes
eta noticeably below 1 for many-sheave systems.

**Inclined plane.** IMA = (length of incline) / (height) = 1/sin(angle). AMA = eta * IMA.

**Wedge.** IMA = (length of slope) / (thickness of the wide end) — a moving double inclined
plane.

**Screw / screw jack.** For a screw jack with an operating lever (or wheel) of radius r turning
a screw of lead L, in one revolution the effort moves 2*pi*r while the load rises L, so:

    VR = IMA_ideal = (2*pi*r) / L

    AMA = eta * VR = eta * (2*pi*r) / L

The screw jack illustrates the trade-off vividly: huge MA (small L, large r) but low efficiency
(self-locking screws are < 50% efficient), so AMA is much smaller than IMA — yet still large
enough to lift a car by hand.

### 5.4 Ideal vs. Actual MA — Summary

| Quantity | Symbol | Meaning |
|---|---|---|
| Velocity ratio | VR | Geometric: input travel / output travel. Fixed by the machine's geometry; independent of friction |
| Ideal mechanical advantage | IMA | = VR. The MA a frictionless version of the machine would have |
| Actual mechanical advantage | AMA | = F_out/F_in measured on the real machine. Always < IMA for real machines |
| Efficiency | eta | = AMA / IMA = (work out)/(work in). 0 < eta < 1; the gap between ideal and actual |

**Conceptual takeaways:**
- VR is pure geometry — it does **not** change with friction, wear, or lubrication.
- IMA = VR always; this is just energy conservation in the lossless limit.
- AMA = eta * VR — friction always makes the real machine *underperform* its geometry.
- A machine that "amplifies force" (MA > 1) always "reduces speed/distance" (VR > 1) by the
  same geometric factor — you never get force multiplication for free; you trade distance.
- For a gear train this is identical to the speed/torque relationship in Part 1.5: a reducer
  multiplies torque (MA-like) exactly as it divides speed (VR), minus efficiency losses.

### 5.5 Common Student Pitfalls (Mechanical Advantage)

- **Equating AMA with VR.** Only the *ideal* MA equals the velocity ratio; the actual MA is
  smaller by the efficiency factor.
- **Thinking friction changes the velocity ratio.** It does not — VR is geometric. Friction
  changes only the *force* relationship (AMA), via eta.
- **Forgetting MA can be less than 1.** Third-class levers and overdrive gears trade force for
  speed; MA < 1 is legitimate.
- **Mixing up which arm is which on a lever.** IMA = effort arm / load arm — the *effort* arm
  on top.
- **For screw jacks, using pitch instead of lead**, or forgetting the 2*pi from one full
  revolution of the operating radius.

---

## Open-source sources used

The following open-access / open-educational resources were consulted via web search and web
fetch while writing this reference. Where a specific page would not fetch in full, the content
was cross-checked against and supplemented with standard, well-established mechanical-engineering
canon (Martin, *Kinematics and Dynamics of Machines*; Shigley/Budynas, *Mechanical Engineering
Design*; Norton, *Design of Machinery*; Wilson & Sadler, *Kinematics and Dynamics of Machinery*)
— this is stable, long-settled textbook material, and any place relying on canon rather than a
fetched open source is noted as such here.

- **Engineering LibreTexts — Mechanics Map (Moore et al.), 6.4 "Power Screws"**
  (eng.libretexts.org) — power-screw torque-to-raise/lower, efficiency, and self-locking
  treatment; ACME vs. square thread (beta factor, sec(alpha) effect).
- **CodeCogs — "Gear Trains: Theory of Machines, Engineering Reference with Worked Examples"**
  (codecogs.com) — fetched in full; simple/compound/reverted train formulas, the relative-
  velocity (formula) method and the tabular method for epicyclic trains, and the
  three-torque relations for epicyclic gearing.
- **Wikipedia — "Involute gear"** (en.wikipedia.org) — involute profile, conjugate action,
  pressure angle, interchangeability of involute gears, interference.
- **KHK Gears technical references — "Involute Gear Profile," "Calculation of Gear Dimensions,"
  and "Gear Systems / Planetary Gear System"** (khkgears.net) — gear nomenclature, module/
  diametral-pitch relations, addendum/dedendum standards, planetary-train component terminology.
- **King Saud University, Mechanical Engineering Dept. — "ME 363 Cam Handout"**
  (faculty.ksu.edu.sa, open courseware PDF) — cam nomenclature, displacement diagrams, and the
  uniform-velocity / parabolic / SHM / cycloidal motion programs with their s-v-a equations.
- **Sathyabama Institute and University of Mustansiriyah open lecture notes on Cam Mechanisms**
  (sathyabama.ac.in, uomustansiriyah.edu.iq — open course PDFs) — displacement-diagram
  construction, base/prime circle and pitch-curve definitions, pressure-angle discussion,
  graphical cam layout by kinematic inversion.
- **EngineerExcel — "Planetary Gear Calculations Explained"** and **eFunda — "Gears: Epicyclic
  Train Example"** (engineerexcel.com, efunda.com) — worked-pattern cross-checks for the
  epicyclic train-value equation (omega_last − omega_arm)/(omega_first − omega_arm) = e and the
  N_R = N_S + 2*N_P geometry constraint.
- **Engineers Edge — "Power Screws Design Equation and Calculator"** and **RoyMech — "Power
  Screw Torque & Efficiency Equations"** (engineersedge.com, roymech.co.uk) — cross-check of
  the raise/lower torque forms, collar-friction term, and efficiency expression.
- **SDP-SI — "Elements of Metric Gear Technology"** (sdp-si.com) — helical/bevel/worm gear
  geometry notes (normal vs. transverse pitch, lead angle, worm-as-n-thread-gear concept).

Topics relying primarily on established textbook canon (noted per the research instruction):
the precise N_min = 2/sin^2(phi) interference limit and its phi-specific values, the
length-of-action and base-pitch contact-ratio derivation, the helical virtual-tooth-count
relation N_e = N/cos^3(psi), the higher-order (3-4-5, 4-5-6-7) polynomial cam programs, and the
lever-class / pulley / inclined-plane mechanical-advantage formulas — all standard and stable
across the canonical texts listed above.
