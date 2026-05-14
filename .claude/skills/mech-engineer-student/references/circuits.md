# Electronic Circuits & Machines Reference

> PhD-level study companion for EE 2305 — Electronic Circuits & Machines.
> Covers DC & AC circuit analysis (KVL/KCL, Thevenin/Norton, superposition, mesh/nodal),
> RC/RL/RLC transients, phasors & impedance, AC power, operational amplifiers, diodes &
> transistors, and electric machines (transformers, DC motors, induction motors).
> Plain-text math: `*` = multiply, `^` = power, `sqrt()` = square root, `j` = imaginary unit,
> `angle` = phase angle, `w` = omega (angular frequency), `||` = in parallel.

---

## 1. Fundamental Quantities & Laws

### 1.1 Definitions

| Quantity | Symbol | Unit | Definition |
|---|---|---|---|
| Charge | Q, q | coulomb (C) | quantity of electricity |
| Current | I, i | ampere (A) | i = dq/dt, rate of charge flow |
| Voltage | V, v | volt (V) | energy per unit charge, v = dw/dq |
| Power | P, p | watt (W) | p = v·i, rate of energy transfer |
| Energy | W | joule (J) | W = integral of p dt |
| Resistance | R | ohm (Ω) | opposition to current |
| Conductance | G | siemens (S) | G = 1/R |

### 1.2 Ohm's Law

  **V = I·R**   (also I = V/R, R = V/I)
Power dissipated in a resistor: **P = V·I = I^2·R = V^2/R**

### 1.3 Sign Conventions (critical)

- **Passive sign convention**: current enters the **+** terminal of an element. With this
  convention, P = v·i; P > 0 means the element **absorbs** power, P < 0 means it **delivers**.
- A source delivering power has P < 0 under the passive convention (current leaves its + terminal).
- Choose a reference (ground) node; all node voltages are measured relative to it.
- Pick current direction arbitrarily — a negative answer just means the real current is opposite.

### 1.4 Kirchhoff's Laws

- **KCL (Current Law)**: the algebraic sum of currents entering any node = 0.
  (Charge conservation — current in = current out.)
- **KVL (Voltage Law)**: the algebraic sum of voltages around any closed loop = 0.
  (Energy conservation — sum of rises = sum of drops.)

### 1.5 Series / Parallel Combinations

**Resistors in series** (same current): R_eq = R_1 + R_2 + ...
**Resistors in parallel** (same voltage): 1/R_eq = 1/R_1 + 1/R_2 + ...
  Two resistors: R_eq = (R_1·R_2)/(R_1 + R_2)
**Voltage divider** (series): V_x = V_total·(R_x / R_total)
**Current divider** (two parallel resistors): I_1 = I_total·(R_2/(R_1 + R_2))

### 1.6 Capacitors & Inductors

| Element | v–i relation | Series combine | Parallel combine | Energy stored |
|---|---|---|---|---|
| Capacitor C | i = C·dv/dt ; v = (1/C)∫i dt | 1/C_eq = Σ1/C_i | C_eq = ΣC_i | W = (1/2)·C·v^2 |
| Inductor L | v = L·di/dt ; i = (1/L)∫v dt | L_eq = ΣL_i | 1/L_eq = Σ1/L_i | W = (1/2)·L·i^2 |

- Capacitor: voltage cannot change instantaneously; in DC steady state acts as **open circuit**.
- Inductor: current cannot change instantaneously; in DC steady state acts as **short circuit**.

### 1.7 Pitfalls

- Capacitors combine **opposite** to resistors (series caps add reciprocals).
- "Voltage across" vs. "voltage at a node" — divider gives the voltage across a chosen element.
- Passive sign convention errors flip the sign of every power calculation.

---

## 2. DC Circuit Analysis Techniques

### 2.1 Nodal Analysis — Procedure

Solves for **node voltages** using KCL.
1. Identify all nodes; pick one as the **reference (ground)**, V = 0.
2. Label the remaining n−1 node voltages.
3. Write a **KCL equation at each non-reference node**: sum of currents leaving = 0. Express each
   resistor current as (V_a − V_b)/R via Ohm's law.
4. **Supernode**: if a voltage source connects two non-reference nodes, enclose both in a
   supernode — write one KCL for the whole supernode plus the constraint equation
   (V_a − V_b = V_source).
5. Solve the linear system for the node voltages.
6. Back-compute branch currents and powers as needed.

### 2.2 Mesh Analysis — Procedure

Solves for **loop (mesh) currents** using KVL. Best for **planar** circuits.
1. Identify the **meshes** (windowpane loops, no element inside).
2. Assign a mesh current to each, conventionally **all clockwise**.
3. Write a **KVL equation around each mesh**: sum of voltage drops = 0. A resistor shared by two
   meshes drops (I_mesh − I_adjacent)·R.
4. **Supermesh**: if a current source is shared between two meshes, combine them into a supermesh
   (KVL around the outer loop, skipping the source) plus the constraint
   (I_a − I_b = I_source).
5. Solve the linear system for the mesh currents.
6. Branch current = algebraic sum of the mesh currents through that branch.

### 2.3 Superposition

For a **linear** circuit with multiple independent sources:
1. **Activate one independent source at a time.** Deactivate the others:
   - Voltage source → replace with a **short circuit**.
   - Current source → replace with an **open circuit**.
   - (Dependent sources stay active — never deactivate them.)
2. Compute the contribution of the active source to the variable of interest.
3. Repeat for each independent source.
4. **Algebraically sum** all contributions.
Note: superposition does NOT apply to **power** (power is nonlinear, ∝ I^2) — only to V and I.

### 2.4 Thevenin's Theorem — Procedure

Any linear two-terminal network reduces to a voltage source V_th in series with resistance R_th.
1. **V_th** = open-circuit voltage across the load terminals (remove the load, find V_oc).
2. **R_th**:
   - No dependent sources: deactivate all independent sources (V-source → short, I-source →
     open), then compute the equivalent resistance looking back into the terminals.
   - With dependent sources: apply a test source (1 V or 1 A) at the terminals with independent
     sources deactivated; R_th = V_test / I_test.
   - Alternative: R_th = V_oc / I_sc (open-circuit voltage / short-circuit current).
3. Reattach the load to the V_th–R_th equivalent and solve.

### 2.5 Norton's Theorem — Procedure

Dual of Thevenin: a current source I_N in parallel with resistance R_N.
1. **I_N** = short-circuit current through the load terminals (replace load with a short, find I_sc).
2. **R_N = R_th** (same procedure as above).
3. **Source transformation relationship**: V_th = I_N·R_N, and I_N = V_th/R_th, R_th = R_N.

### 2.6 Source Transformation

A voltage source V in series with R ↔ a current source I = V/R in parallel with the same R.
Useful for simplifying circuits before nodal/mesh analysis.

### 2.7 Maximum Power Transfer

For a Thevenin source (V_th, R_th) driving a load R_L:
- Maximum power is delivered when **R_L = R_th**.
- That maximum power: **P_max = V_th^2 / (4·R_th)**.
- Efficiency at max power transfer is only **50%** (half the power is lost in R_th).
- (AC version: load impedance Z_L = conjugate of Z_th, i.e., Z_L = R_th − j·X_th.)

### 2.8 Pitfalls

- Nodal solves for voltages; mesh solves for currents — pick based on what's asked / fewer equations.
- Don't deactivate **dependent** sources in superposition or Thevenin.
- Superposition applies to V and I, **never directly to power**.
- Supernode needs the constraint equation; supermesh needs its constraint too — easy to forget.
- R_th = V_oc/I_sc only works when both are finite and nonzero.

---

## 3. Transient Analysis (First-Order Circuits)

### 3.1 RC Circuit

A resistor and capacitor; **time constant tau = R·C** (seconds).
**Charging** (capacitor initially uncharged, switched to source V_s at t = 0):
  v_C(t) = V_s·(1 − e^(−t/tau))
  i(t)   = (V_s/R)·e^(−t/tau)
**Discharging** (capacitor initially at V_0, source removed):
  v_C(t) = V_0·e^(−t/tau)

### 3.2 RL Circuit

A resistor and inductor; **time constant tau = L/R** (seconds).
**Current rise** (inductor energizing from source V_s):
  i_L(t) = (V_s/R)·(1 − e^(−t/tau))
**Current decay** (source removed, initial current I_0):
  i_L(t) = I_0·e^(−t/tau)

Note: for RL, tau is **inversely** proportional to R — opposite of the RC intuition.

### 3.3 General First-Order Solution (the universal formula)

For any first-order circuit variable x(t):
  **x(t) = x(∞) + [x(0+) − x(∞)]·e^(−t/tau)**
- x(0+) = value just after switching (use continuity: v_C and i_L cannot jump).
- x(∞) = final steady-state value (cap = open, inductor = short for DC).
- tau = R_th·C or L/R_th, where R_th is the Thevenin resistance seen by the C or L.

### 3.4 Time-Constant Milestones

| Elapsed time | % of total change completed |
|---|---|
| 1·tau | 63.2% |
| 2·tau | 86.5% |
| 3·tau | 95.0% |
| 4·tau | 98.2% |
| 5·tau | 99.3% (≈ "fully settled") |

### 3.5 Pitfalls

- v_C and i_L are **continuous** — they cannot change instantaneously. v_C(0+) = v_C(0−),
  i_L(0+) = i_L(0−). But i_C and v_L CAN jump.
- For tau, use the resistance the cap/inductor "sees" (Thevenin R at its terminals), not just R.
- RL time constant is L/R, not R/L — and bigger R means **faster** decay.
- At t = ∞ for DC: capacitor → open, inductor → short. At t = 0+ for an initially relaxed
  element: capacitor → short (v=0), inductor → open (i=0).

---

## 4. Second-Order Circuits (RLC)

### 4.1 Series RLC — Governing Equation

KVL around a series RLC loop (with the capacitor voltage as the variable) yields:
  L·C·v_C'' + R·C·v_C' + v_C = v_source
Rewritten in standard form:
  v_C'' + (R/L)·v_C' + (1/(L·C))·v_C = ...

Define:
- **Undamped natural frequency**: w_0 = 1/sqrt(L·C)
- **Damping (neper) frequency, series**: alpha = R/(2·L)
- **Damping ratio**: zeta = alpha/w_0 = (R/2)·sqrt(C/L)
- Characteristic roots: s = −alpha ± sqrt(alpha^2 − w_0^2)

### 4.2 Parallel RLC

Same w_0 = 1/sqrt(L·C), but **alpha = 1/(2·R·C)** for the parallel configuration.

### 4.3 Three Damping Cases

| Condition | Name | Roots | Response |
|---|---|---|---|
| alpha > w_0 (zeta > 1) | Overdamped | two real negative | Slow, no oscillation |
| alpha = w_0 (zeta = 1) | Critically damped | repeated real −alpha | Fastest non-oscillatory |
| alpha < w_0 (zeta < 1) | Underdamped | −alpha ± j·w_d | Decaying oscillation |

**Damped oscillation frequency**: w_d = sqrt(w_0^2 − alpha^2)

Underdamped response form:
  x(t) = x(∞) + e^(−alpha·t)·[B_1·cos(w_d·t) + B_2·sin(w_d·t)]
Constants B_1, B_2 from two initial conditions (x(0+) and x'(0+)).

### 4.4 Solution Procedure

1. Find initial conditions: v_C(0+), i_L(0+) (continuity), then derive x'(0+) from element laws.
2. Find final value x(∞) (DC steady state).
3. Compute alpha and w_0; classify the damping case.
4. Write the appropriate solution form with unknown constants.
5. Apply the two initial conditions to solve for the constants.

### 4.5 Pitfalls

- alpha differs between series (R/2L) and parallel (1/2RC) RLC — don't mix them up.
- Need **two** initial conditions for a second-order circuit; the second usually comes from
  applying element laws at t = 0+ (e.g., i_C = C·dv_C/dt).
- w_d < w_0 always.

---

## 5. AC Steady-State Analysis — Phasors & Impedance

### 5.1 Sinusoids

A sinusoid v(t) = V_m·cos(w·t + phi):
- V_m = amplitude (peak), w = angular frequency (rad/s) = 2·pi·f, phi = phase angle.
- **RMS value**: V_rms = V_m / sqrt(2) (for a sinusoid).

### 5.2 Phasors

A phasor represents a sinusoid as a complex number (magnitude + phase), implicitly at frequency w:
  v(t) = V_m·cos(w·t + phi)  ↔  **V = V_m ∠phi**  (or V_rms ∠phi, state which)
Phasor arithmetic replaces calculus: d/dt → multiply by jw, integral → divide by jw.

### 5.3 Impedance

**Impedance Z** = phasor voltage / phasor current; complex, units of ohms. Z = R + jX.
- R = resistance (real part), X = reactance (imaginary part).

| Element | Impedance Z | Reactance | Phase (V relative to I) |
|---|---|---|---|
| Resistor | Z_R = R | 0 | 0° (in phase) |
| Inductor | Z_L = jwL | X_L = wL (+) | +90° (V leads I) |
| Capacitor | Z_C = 1/(jwC) = −j/(wC) | X_C = −1/(wC) (−) | −90° (V lags I) |

**Admittance** Y = 1/Z = G + jB (G = conductance, B = susceptance).

### 5.4 Impedance Combinations

Impedances combine **exactly like resistances**:
- Series: Z_eq = Z_1 + Z_2 + ...
- Parallel: 1/Z_eq = 1/Z_1 + 1/Z_2 + ... ; two elements: Z_eq = Z_1·Z_2/(Z_1+Z_2)
- Voltage/current dividers, KVL, KCL, nodal, mesh, Thevenin, Norton, superposition — **all
  apply unchanged**, just with complex impedances and phasors.

### 5.5 AC Analysis Procedure

1. Convert all sources to phasors; all R, L, C to impedances at the operating w.
2. Apply any DC technique (nodal, mesh, Thevenin, etc.) using complex algebra.
3. The result is a phasor — convert back to a time-domain sinusoid:
   V = V_m∠phi  →  v(t) = V_m·cos(w·t + phi).
- Mixed frequencies: use **superposition** — solve at each frequency separately, sum time-domain results.

### 5.6 Resonance

**Series RLC resonance**: at w_0 = 1/sqrt(L·C), X_L = X_C, so Z is purely **real and minimum**
(= R). Current is maximum.
**Parallel RLC resonance**: at w_0, impedance is purely real and **maximum**; current is minimum.
- **Quality factor** (series): Q = w_0·L/R = (1/R)·sqrt(L/C)
- **Bandwidth**: BW = w_0/Q (between the half-power frequencies).

### 5.7 Pitfalls

- Always state whether a phasor magnitude is **peak** or **RMS** — power formulas use RMS.
- Inductor: V leads I ("ELI"); Capacitor: I leads V ("ICE") → mnemonic "ELI the ICE man".
- 1/(jwC) = −j/(wC): the capacitor reactance is **negative**.
- You can only use phasors at a **single frequency** — multi-frequency needs superposition.
- Adding sinusoids of different frequency is NOT a phasor operation.

---

## 6. AC Power

### 6.1 Power Quantities

For an AC load with voltage and current phasors (RMS), and theta = angle between V and I:
- **Instantaneous power**: p(t) = v(t)·i(t)
- **Real (average / active) power**: **P = V_rms·I_rms·cos(theta)**  [watts, W] — power actually
  dissipated.
- **Reactive power**: **Q = V_rms·I_rms·sin(theta)**  [volt-amperes reactive, VAR] — power that
  shuttles back and forth, stored/returned by L and C.
- **Apparent power**: **S = V_rms·I_rms**  [volt-amperes, VA]
- **Complex power**: **S = P + jQ = V·I*** (I* = conjugate of current phasor); |S| = S_apparent.
- **Power triangle**: S^2 = P^2 + Q^2.

### 6.2 Power Factor

  **PF = cos(theta) = P / S**
- theta = angle of the load impedance (angle of V minus angle of I).
- **Lagging PF**: inductive load (current lags voltage), Q > 0.
- **Leading PF**: capacitive load (current leads voltage), Q < 0.
- **Power factor correction**: add a parallel capacitor to an inductive load to reduce Q and
  bring PF closer to 1 → less current for the same real power.

### 6.3 Power in Each Element

- Resistor: absorbs only real power P = I_rms^2·R; Q = 0.
- Inductor: absorbs only reactive power Q = I_rms^2·X_L; P = 0.
- Capacitor: supplies reactive power Q = −I_rms^2·|X_C|; P = 0.

### 6.4 Pitfalls

- Use **RMS** values in all power formulas. Using peak values overstates power by 2×.
- Reactive power is real and matters (utility billing, conductor sizing) — it just isn't dissipated.
- cos(theta) alone is ambiguous — always specify leading or lagging.
- Average power of a resistor: P = V_rms^2/R, not V_peak^2/R.

---

## 7. Operational Amplifiers (Op-Amps)

### 7.1 Ideal Op-Amp Assumptions

1. Infinite open-loop gain (A → ∞).
2. Infinite input impedance → **no current into either input terminal** (i+ = i− = 0).
3. Zero output impedance.
4. Infinite bandwidth, zero offset.

### 7.2 The Two Golden Rules (with negative feedback)

- **Rule 1**: no current flows into the input terminals.
- **Rule 2 (virtual short)**: the op-amp output drives the inputs to be equal: **V+ = V−**.
  When V+ is grounded, V− is a **virtual ground** (0 V but not actually connected to ground).

### 7.3 Standard Configurations

| Configuration | Gain / output | Notes |
|---|---|---|
| Inverting amplifier | V_out = −(R_f/R_in)·V_in | input at V−, V+ grounded; input Z = R_in |
| Non-inverting amplifier | V_out = (1 + R_f/R_in)·V_in | input at V+; very high input Z |
| Voltage follower (buffer) | V_out = V_in | gain = 1, isolates stages |
| Summing amplifier | V_out = −R_f·(V_1/R_1 + V_2/R_2 + ...) | inverting summer |
| Difference amplifier | V_out = (R_f/R_1)·(V_2 − V_1) | with matched resistor ratios |
| Integrator | V_out = −(1/(R·C))·∫V_in dt | feedback capacitor |
| Differentiator | V_out = −R·C·(dV_in/dt) | input capacitor; noisy |

### 7.4 Analysis Procedure (ideal op-amp with feedback)

1. Confirm there is **negative feedback** (path from output to V−).
2. Apply Rule 2: set V− = V+.
3. Apply Rule 1: write KCL at the input node(s) — no current enters the op-amp, so all current
   into the node goes through the feedback element.
4. Solve for V_out.

### 7.5 Real Op-Amp Non-Idealities

- Finite open-loop gain and bandwidth → **gain-bandwidth product (GBW)** is roughly constant:
  closed-loop gain × bandwidth ≈ GBW.
- **Slew rate** limits how fast V_out can change (V/μs).
- Input offset voltage, input bias currents, finite input/output impedance.
- Output saturates at the supply rails (cannot exceed ±V_supply).

### 7.6 Pitfalls

- The virtual-short rule applies **only with negative feedback** — for a comparator (no feedback
  or positive feedback) the output just saturates.
- Inverting amp has gain −R_f/R_in; non-inverting has 1 + R_f/R_in — note the "+1" and signs.
- Virtual ground is at 0 V but draws no current to actual ground — don't connect it.
- Real op-amps clip at the rails — check that the computed V_out is within ±V_supply.

---

## 8. Diodes

### 8.1 Diode Behavior

A diode conducts in one direction (anode → cathode) once forward-biased past the threshold.
- **Ideal model**: short when forward-biased, open when reverse-biased.
- **Constant-voltage-drop model**: V_D ≈ 0.7 V (Si) when conducting, open otherwise.
- **Shockley equation**: I_D = I_S·(e^(V_D/(n·V_T)) − 1), V_T ≈ 25.85 mV at room temperature.

### 8.2 Analysis Procedure (constant-drop model)

1. **Assume** a state for each diode (ON or OFF).
2. Analyze the resulting linear circuit.
3. **Check consistency**: an ON diode must carry I_D > 0; an OFF diode must have V_D < 0.7 V.
4. If any check fails, change that diode's assumed state and repeat.

### 8.3 Common Diode Circuits

- **Half-wave rectifier**: passes one half of the AC cycle.
- **Full-wave (bridge) rectifier**: passes both halves; output ≈ |V_in| − 2·V_D.
- **Zener diode**: operated in reverse breakdown at a fixed V_Z — used for voltage regulation.
- **Clippers / clampers**: shape waveforms by limiting or shifting.

### 8.4 Pitfalls

- Always **verify** the assumed diode states; a wrong assumption gives a self-inconsistent answer.
- Bridge rectifier drops **two** diode voltages, not one.
- Zener is used in **reverse** breakdown — forward it behaves like an ordinary diode.

---

## 9. Transistors (Basics)

### 9.1 BJT (Bipolar Junction Transistor)

Three terminals: base (B), collector (C), emitter (E). Current-controlled.
- **Cutoff**: both junctions reverse-biased → transistor OFF, I_C ≈ 0.
- **Active**: BE forward, BC reverse → **I_C = beta·I_B**, I_E = I_C + I_B = (beta+1)·I_B.
  Used for **amplification**.
- **Saturation**: both junctions forward → transistor fully ON, V_CE ≈ 0.2 V. Used as a closed **switch**.
- beta (h_FE) = current gain, typically 50–300.

### 9.2 MOSFET (Metal-Oxide-Semiconductor FET)

Three terminals: gate (G), drain (D), source (S). Voltage-controlled (no gate current).
- **Cutoff**: V_GS < V_th → OFF.
- **Triode (ohmic)**: V_GS > V_th and small V_DS → acts like a voltage-controlled resistor.
- **Saturation**: V_GS > V_th and V_DS large → I_D ≈ (1/2)·k·(V_GS − V_th)^2, used for amplification.

### 9.3 DC Bias Analysis Procedure (BJT, active region)

1. Assume the active region. Use V_BE ≈ 0.7 V.
2. Apply KVL to the base-emitter loop to find I_B (or I_E).
3. Compute I_C = beta·I_B.
4. Apply KVL to the collector-emitter loop to find V_CE.
5. **Verify**: V_CE > V_CE(sat) (≈ 0.2 V) confirms active; if V_CE ≤ 0.2 V, the transistor is
   actually saturated — redo with V_CE = 0.2 V.

### 9.4 Pitfalls

- Always verify the assumed operating region (like diodes).
- BJT is **current**-controlled (I_B), MOSFET is **voltage**-controlled (V_GS).
- "Saturation" means **opposite** things for BJT (fully ON, switch) vs. MOSFET (the amplifying
  region) — a notorious source of confusion.

---

## 10. Electric Machines

### 10.1 Transformers

An iron core links two windings; transfers AC power between voltage levels via mutual induction.
**Ideal transformer relations** (turns ratio a = N_1/N_2):
  V_1/V_2 = N_1/N_2 = a
  I_1/I_2 = N_2/N_1 = 1/a
  Power conserved: V_1·I_1 = V_2·I_2 (ideal, lossless)
**Impedance referral**: an impedance Z_2 on the secondary appears as a^2·Z_2 on the primary.
- Step-up: N_2 > N_1 (raises voltage); step-down: N_2 < N_1.
- Real transformers have copper losses (winding R), core losses (hysteresis + eddy currents),
  and leakage reactance.
- Efficiency = P_out/P_in; tested via open-circuit (core loss) and short-circuit (copper loss) tests.

### 10.2 DC Motors

Convert DC electrical power to mechanical rotation. Key relations:
- **Back-EMF**: E_b = K·phi·w   (proportional to flux and speed)
- **Torque**: T = K·phi·I_a   (proportional to flux and armature current)
- **Armature circuit (KVL)**: V_t = E_b + I_a·R_a
  → I_a = (V_t − E_b)/R_a
- **Speed equation**: w = (V_t − I_a·R_a)/(K·phi)
Types by field connection:
- **Shunt**: field parallel to armature → nearly constant speed.
- **Series**: field in series with armature → very high starting torque, speed varies strongly
  with load (must not be run unloaded — runaway).
- **Compound**: combination of shunt and series characteristics.
- Speed control: vary V_t (armature control) or phi (field control).

### 10.3 Induction (Asynchronous) Motors

The workhorse AC motor; rotor currents are **induced** (no electrical connection to the rotor).
- **Synchronous speed**: n_s = 120·f / P  (rpm), where f = line frequency, P = number of poles.
- **Slip**: s = (n_s − n) / n_s, where n = actual rotor speed.
  - At standstill: s = 1. At synchronous speed: s = 0 (but then no torque).
  - Normal operation: small slip, typically 1–5%.
- Rotor frequency = s·f.
- Torque is produced because the rotor "slips" behind the rotating stator field; torque is zero
  at exactly synchronous speed.
- Squirrel-cage rotor (rugged, common) vs. wound rotor (slip rings, adjustable).

### 10.4 Synchronous Machines (brief)

Rotor is excited with DC and **locks to** the rotating stator field: runs exactly at n_s.
Used as generators (most grid power) and as synchronous motors / condensers (PF correction).

### 10.5 Pitfalls

- Transformer impedance referral uses **a^2**, not a.
- An induction motor can **never** reach synchronous speed under load (it needs slip to make torque).
- A **series** DC motor must not be started unloaded — it can over-speed destructively.
- Back-EMF rises with speed and limits armature current; at startup E_b = 0 so inrush current is
  large (V_t/R_a) — starting resistors or soft-starters are used.
- Slip is dimensionless (a fraction or %); rotor frequency = slip × line frequency.

---

## 11. Quick-Reference Tables

### 11.1 Circuit Element Relations

| Element | DC steady state | v–i relation | Impedance Z(jw) | Energy |
|---|---|---|---|---|
| Resistor R | R | v = R·i | R | dissipates I^2·R |
| Capacitor C | open circuit | i = C·dv/dt | 1/(jwC) | (1/2)C·v^2 |
| Inductor L | short circuit | v = L·di/dt | jwL | (1/2)L·i^2 |

### 11.2 First-Order Transient Summary

| Circuit | Time constant tau | Universal formula |
|---|---|---|
| RC | R·C | x(t) = x(∞) + [x(0+) − x(∞)]·e^(−t/tau) |
| RL | L/R | x(t) = x(∞) + [x(0+) − x(∞)]·e^(−t/tau) |

### 11.3 Series RLC Parameters

| Quantity | Series RLC | Parallel RLC |
|---|---|---|
| Natural frequency w_0 | 1/sqrt(LC) | 1/sqrt(LC) |
| Damping alpha | R/(2L) | 1/(2RC) |
| Damped frequency w_d | sqrt(w_0^2 − alpha^2) | sqrt(w_0^2 − alpha^2) |
| Quality factor Q | w_0·L/R | R/(w_0·L) |

### 11.4 AC Power Triangle

| Quantity | Symbol | Formula | Unit |
|---|---|---|---|
| Real power | P | V_rms·I_rms·cos(theta) | W |
| Reactive power | Q | V_rms·I_rms·sin(theta) | VAR |
| Apparent power | S | V_rms·I_rms | VA |
| Complex power | S | P + jQ = V·I* | VA |
| Power factor | PF | cos(theta) = P/S | — |

### 11.5 Op-Amp Configuration Gains

| Configuration | Gain |
|---|---|
| Inverting | −R_f/R_in |
| Non-inverting | 1 + R_f/R_in |
| Voltage follower | 1 |
| Integrator | −1/(R·C·s) |
| Differentiator | −R·C·s |

### 11.6 Machine Key Equations

| Machine | Key relation |
|---|---|
| Ideal transformer | V_1/V_2 = N_1/N_2 = a ; I_1/I_2 = 1/a ; Z_referred = a^2·Z |
| DC motor | E_b = K·phi·w ; T = K·phi·I_a ; V_t = E_b + I_a·R_a |
| Induction motor | n_s = 120f/P ; s = (n_s − n)/n_s |

---

## Open-source sources used

- James M. Fiore, *DC Electrical Circuit Analysis: A Practical Approach*, Engineering LibreTexts — KCL/KVL, series/parallel, nodal & mesh analysis, superposition, Thevenin/Norton, RC & RL transients — `https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/DC_Electrical_Circuit_Analysis_-_A_Practical_Approach_(Fiore)`
- James M. Fiore, *AC Electrical Circuit Analysis: A Practical Approach*, Engineering LibreTexts — phasors & impedance, AC nodal/mesh, AC Thevenin/Norton, RLC second-order response, AC power, resonance — `https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/AC_Electrical_Circuit_Analysis:_A_Practical_Approach_(Fiore)`
- James M. Fiore, *Operational Amplifiers and Linear Integrated Circuits: Theory and Application*, Engineering LibreTexts — ideal op-amp, inverting/non-inverting amplifiers, integrators, differentiators, non-idealities — `https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/Operational_Amplifiers_and_Linear_Integrated_Circuits_-_Theory_and_Application_(Fiore)`
- *Circuits and Devices*, Engineering LibreTexts (Cañada College) — AC circuit analysis theorems and techniques, diodes, transistors, electric machines — `https://eng.libretexts.org/Courses/Canada_College/Circuits_and_Devices`
- Ultimate Electronics Book (CircuitLab, open online edition) — Thevenin/Norton equivalents, op-amp circuits, transient analysis — `https://ultimateelectronicsbook.com/`
- *College Physics* (OpenStax), Physics LibreTexts — RLC series AC circuits, resonance, electromagnetic induction & AC machines — `https://phys.libretexts.org/Bookshelves/College_Physics/College_Physics_1e_(OpenStax)`
- MIT OpenCourseWare 6.071J — *Introduction to Electronics, Signals, and Measurement* — RLC transient response notes — `https://ocw.mit.edu/courses/6-071j-introduction-to-electronics-signals-and-measurement-spring-2006/`
