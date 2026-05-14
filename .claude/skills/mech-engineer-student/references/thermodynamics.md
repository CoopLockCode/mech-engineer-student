# Thermodynamics Reference

> Graduate-level study companion for Thermodynamics. Covers properties of pure substances, ideal and real gases, the first law (closed and open systems), the second law, entropy, exergy, and power/refrigeration cycles. Plain-text math notation throughout: `*` multiply, `/` divide, `^` power, Greek spelled out (eta, rho, etc.). Subscripts written inline (h_f, T_H).

---

## 0. Foundational Concepts, Definitions, Sign Conventions

### 0.1 System, surroundings, boundary
- **System** — the matter or region under study.
- **Closed system (control mass)** — fixed mass, no mass crosses the boundary; energy (Q, W) can.
- **Open system (control volume, CV)** — mass *and* energy cross the boundary (turbines, pumps, nozzles).
- **Isolated system** — neither mass nor energy crosses.
- **Boundary** — real or imaginary surface separating system from surroundings; can be fixed or moving.

### 0.2 Properties
- **Intensive** — independent of mass (T, P, rho, v specific volume, all specific quantities).
- **Extensive** — scale with mass (V, U, H, S, m).
- A specific extensive property (per unit mass) is intensive: v = V/m, u = U/m, h = H/m, s = S/m.

### 0.3 State, process, cycle
- **State** — condition described by a set of properties.
- **State postulate** — the state of a *simple compressible system* is fixed by **two independent intensive properties**. (Two properties are independent unless the system is in a two-phase region, where T and P are dependent.)
- **Process** — change of state. **Quasi-equilibrium (quasi-static)** process: deviates from equilibrium infinitesimally, so the path is well-defined and can be drawn on property diagrams.
- **Cycle** — sequence of processes returning the system to its initial state. For a cycle, all property changes are zero: dU_cycle = 0, dS_cycle = 0, etc.

### 0.4 Process types (prefix "iso-")
- Isothermal: T constant. Isobaric: P constant. Isochoric/isometric: v constant. Isentropic: s constant. Adiabatic: Q = 0 (not necessarily isentropic — only reversible + adiabatic is isentropic). Polytropic: P*v^n = constant.

### 0.5 SIGN CONVENTIONS (the #1 source of student errors)
Two common conventions exist. **This reference uses the classical (Cengel/Moran) convention:**
- **Q > 0** when heat is added *to* the system; **Q < 0** when heat leaves.
- **W > 0** when work is done *by* the system on the surroundings; **W < 0** when work is done *on* the system.
- First law (closed): `Q - W = dU` (heat in minus work out equals energy rise).

**Pitfall:** Physics texts and some chem-E texts use `dU = Q + W` (work done *on* the system positive). Pick one convention and never mix. When in doubt, reason physically: adding heat raises energy; the system doing work lowers it.

### 0.6 The zeroth law
If two bodies are each in thermal equilibrium with a third body, they are in thermal equilibrium with each other. This is what makes temperature a meaningful, measurable property.

### 0.7 Pressure
- Absolute pressure: P_abs = P_atm + P_gauge (gauge), or P_abs = P_atm - P_vac (vacuum).
- **Always use absolute pressure and absolute temperature (Kelvin/Rankine) in thermodynamic relations.** Gauge pressure in equations is a classic error.
- Manometry: P_2 - P_1 = rho*g*h (hydrostatic; height difference of a column).

---

## 1. Properties of Pure Substances

### 1.1 Phases and phase-change terminology
A **pure substance** has a fixed chemical composition throughout (water, N2, refrigerant-134a; air is treated as pure even though it's a mixture, as long as no phase change separates components).

Phase-change states for a liquid being heated at constant pressure:
- **Compressed (subcooled) liquid** — below saturation temperature for its pressure.
- **Saturated liquid** — on the verge of vaporizing (subscript f).
- **Saturated liquid–vapor mixture** — two phases coexist; T and P are dependent (saturation line).
- **Saturated vapor** — just fully vaporized (subscript g).
- **Superheated vapor** — above saturation temperature for its pressure.

### 1.2 Key temperatures and points
- **Saturation temperature T_sat** — boiling temperature at a given pressure. **Saturation pressure P_sat** — pressure at which boiling occurs at a given temperature. They are a one-to-one function: P_sat = f(T_sat).
- **Critical point** — above it, no distinct liquid/vapor phase transition occurs (water: 22.06 MPa, 373.95 °C).
- **Triple point** — all three phases coexist (water: 0.6117 kPa, 0.01 °C).

### 1.3 Property diagrams
- **T–v, P–v, P–T** diagrams: learn the dome shape. Inside the dome = two-phase. Left of dome = compressed liquid; right = superheated vapor; apex = critical point.
- **T–s and h–s (Mollier)** diagrams: essential for cycle analysis. On T–s, area under a reversible process path = heat transfer.

### 1.4 Quality and the mixture rule
**Quality** x = m_vapor / m_total, defined only inside the two-phase dome, 0 <= x <= 1.

For ANY specific property y (y = v, u, h, or s) in the two-phase region:
```
y = y_f + x * y_fg          where y_fg = y_g - y_f
equivalently  y = (1 - x) * y_f + x * y_g
solve for quality:  x = (y - y_f) / y_fg
```
**Pitfall:** Quality is NOT a percentage of volume — it is a *mass* fraction. A tank can be 99% full of liquid by volume and still have x near 0.

### 1.5 Property-table usage methods

**Step 1 — Identify the region.** Compare given properties to saturation data:
- If T < T_sat(P)  ->  compressed liquid.
- If T > T_sat(P)  ->  superheated vapor.
- If T = T_sat(P)  ->  in the dome; need a second property (x, or v/u/h/s) to locate it.
- A quick check: if you're given v and find v_f < v < v_g at that T or P, you're in the dome.

**Step 2 — Read or interpolate.**
- **Saturation tables** (indexed by T, or by P): give v_f, v_g, u_f, u_fg, u_g, h_f, h_fg, h_g, s_f, s_fg, s_g.
- **Superheated tables**: indexed by P, then T; give v, u, h, s directly.
- **Compressed-liquid tables**: exist for water at high pressures. When unavailable, use the **compressed-liquid approximation:**
  ```
  y ≈ y_f(T)   for v, u, s   (function of temperature, weakly of pressure)
  h ≈ h_f(T) + v_f(T) * (P - P_sat(T))    (pressure correction matters for h)
  ```

**Step 3 — Linear interpolation.** For a target value t between table entries (t1, y1) and (t2, y2):
```
y = y1 + (t - t1) * (y2 - y1) / (t2 - t1)
```
Double interpolation (between two pressures AND two temperatures in superheat tables): interpolate in T at each pressure first, then interpolate between the two results in P.

**Pitfalls:** (1) Mixing T-table and P-table entries inconsistently. (2) Forgetting u_fg vs reading u_f and u_g separately — both work, be consistent. (3) Reference state: u and h tables have an arbitrary zero (water: u_f = 0 at triple point; R-134a: h_f = 0 at -40 °C). Only *differences* are physical, so never mix substances' tables.

---

## 2. Ideal Gases and Real Gases

### 2.1 The ideal-gas equation of state
```
P * V = m * R * T          P * v = R * T          P * V = N * R_u * T
```
- R = gas constant for the specific gas = R_u / M, where R_u = 8.314 kJ/(kmol*K) (universal), M = molar mass.
- **T must be absolute (K or R). P must be absolute.**
- **Validity:** good when the gas is at low density — high T and/or low P relative to its critical point. Quantified by the compressibility factor.

### 2.2 Compressibility factor and the principle of corresponding states
```
Z = P*v / (R*T)            Z = 1 for an ideal gas
```
Real-gas correction: P*v = Z*R*T. Z is read from the **generalized compressibility chart** as a function of:
```
Reduced pressure   P_R = P / P_cr
Reduced temperature T_R = T / T_cr
```
**Principle of corresponding states:** all gases behave similarly when compared at the same P_R and T_R. Rule of thumb for ideal-gas validity: P_R << 1 OR T_R > 2 (except near the critical point).

### 2.3 Other real-gas equations of state
- **van der Waals:** (P + a/v^2)(v - b) = R*T. Constants a (intermolecular attraction), b (molecular volume) from critical-point data: a = 27*R^2*T_cr^2/(64*P_cr), b = R*T_cr/(8*P_cr).
- **Redlich–Kwong, Benedict–Webb–Rubin, Beattie–Bridgeman** — successively more accurate, more constants.

### 2.4 Internal energy, enthalpy, specific heats of ideal gases
For an ideal gas, u = u(T) and h = h(T) **only** (Joule's law — no pressure or volume dependence).
```
du = c_v(T) dT          dh = c_p(T) dT
h = u + P*v = u + R*T   ->   c_p = c_v + R   ->   c_p - c_v = R
Specific heat ratio:  k = c_p / c_v   (gamma; ~1.4 for air, ~1.67 monatomic, ~1.3 polyatomic)
```
Three ways to evaluate ideal-gas Du and Dh, in increasing accuracy:
1. **Constant specific heats:** Du = c_v,avg * (T2 - T1), Dh = c_p,avg * (T2 - T1). Use room-temp values for small DT or values at the average temperature.
2. **Tabulated u(T) and h(T)** (ideal-gas tables, e.g., air table): Du = u2 - u1, Dh = h2 - h1. Accounts for temperature variation of specific heats.
3. **Polynomial c_p(T)** integrated analytically.

### 2.5 Entropy change of an ideal gas
General (variable c):
```
s2 - s1 = s°(T2) - s°(T1) - R * ln(P2 / P1)
```
where s°(T) is the temperature-dependent part tabulated in ideal-gas tables.

Constant specific heats:
```
s2 - s1 = c_v * ln(T2/T1) + R * ln(v2/v1)
s2 - s1 = c_p * ln(T2/T1) - R * ln(P2/P1)
```

**Isentropic ideal-gas relations** (s2 = s1):
- Variable c: use relative pressure P_r and relative volume v_r from tables: P2/P1 = P_r2/P_r1, v2/v1 = v_r2/v_r1.
- Constant c (the "isentropic relations"):
  ```
  T2/T1 = (P2/P1)^((k-1)/k) = (v1/v2)^(k-1)
  P*v^k = constant
  ```

---

## 3. The First Law — Closed Systems

### 3.1 Forms of energy
Total energy E = U (internal) + KE + PE. Specific: e = u + V^2/2 + g*z.
Internal energy U = sensible + latent + chemical + nuclear (thermodynamics usually tracks sensible + latent).

### 3.2 Work modes (closed system)
- **Moving boundary (P–dV) work:** `W_b = integral( P dV )` from state 1 to 2. This is the **area under the process path on a P–V diagram.** Process-dependent (a path function).
  - Isobaric: W_b = P*(V2 - V1).
  - Isothermal ideal gas: W_b = m*R*T*ln(V2/V1) = P1*V1*ln(V2/V1).
  - Polytropic (P*V^n = C), n != 1: W_b = (P2*V2 - P1*V1)/(1 - n).
- **Spring work:** W_spring = (1/2)*k*(x2^2 - x1^2).
- **Electrical work:** W_e = integral(V*I dt). **Shaft work:** W_sh = 2*pi*n*Torque.

### 3.3 First law for a closed system
```
Q_net,in - W_net,out = dE_system
Q - W = dU + dKE + dPE       (general)
Q - W = dU = m*(u2 - u1)     (stationary closed system — most common)
```
Per-unit-mass and rate forms:
```
q - w = du            Q_dot - W_dot = dE/dt
```
**Special cases:**
- Isochoric (rigid tank, W_b = 0): Q = dU.
- Isobaric: Q - W_b = dU  ->  Q = dU + P*dV = dH, so **Q = m*(h2 - h1)** at constant P. (This is *why* enthalpy is defined.)
- Adiabatic: -W = dU.
- Cycle: Q_net = W_net (since dU_cycle = 0).

### 3.4 Specific heats — defining relations
```
c_v = (du/dT) at constant v        c_p = (dh/dT) at constant P
```
For incompressible substances (liquids, solids): c_p = c_v = c, and
```
du = c*dT       dh = c*dT + v*dP       ds = c*dT/T
```

### 3.5 Worked-example pattern — closed system
1. Sketch the system; draw the process on a P–v or T–v diagram.
2. Identify the substance and both end states; build a state table (P, T, v, u, h, s, x).
3. Look up / compute properties at states 1 and 2.
4. Write the first law; cross out zero terms (state assumptions explicitly).
5. Compute work from the process path; solve for the unknown.
6. Sanity-check signs and magnitudes.

---

## 4. The First Law — Open Systems (Control Volumes)

### 4.1 Conservation of mass
```
dm_CV/dt = sum(m_dot_in) - sum(m_dot_out)
Mass flow rate:  m_dot = rho * A * V_avg = A * V_avg / v
Volume flow rate: V_dot = A * V_avg = m_dot * v
```
Steady state: dm_CV/dt = 0  ->  sum(m_dot_in) = sum(m_dot_out). Single stream: m_dot_1 = m_dot_2  ->  rho1*A1*V1 = rho2*A2*V2.

### 4.2 Flow work and enthalpy
Pushing mass into/out of a CV requires **flow work** w_flow = P*v per unit mass. Combining flow work with internal energy gives enthalpy naturally: the energy carried by flowing mass per unit mass is `h + V^2/2 + g*z` — this is *why* h, not u, appears in CV energy balances.

### 4.3 General energy balance for a control volume
```
dE_CV/dt = Q_dot_net,in - W_dot_net,out
           + sum_in  m_dot*(h + V^2/2 + g*z)
           - sum_out m_dot*(h + V^2/2 + g*z)
```
Here W_dot is **shaft/electrical work only** — flow work is already absorbed into h.

### 4.4 Steady-flow energy equation (SFEE)
Steady state: dE_CV/dt = 0, dm_CV/dt = 0. For a single inlet (1), single outlet (2):
```
Q_dot - W_dot = m_dot * [ (h2 - h1) + (V2^2 - V1^2)/2 + g*(z2 - z1) ]
```
Per unit mass:  q - w = (h2 - h1) + (V2^2 - V1^2)/2 + g*(z2 - z1).

### 4.5 Steady-flow devices — assumptions and reduced energy balances

| Device | Purpose | Key assumptions | Reduced SFEE |
|---|---|---|---|
| **Nozzle** | accelerate flow | adiabatic, w=0, dPE~0 | h1 + V1^2/2 = h2 + V2^2/2 |
| **Diffuser** | decelerate flow | adiabatic, w=0, dPE~0 | h1 + V1^2/2 = h2 + V2^2/2 |
| **Turbine** | extract shaft work | adiabatic, dKE & dPE ~0 | w_out = h1 - h2 |
| **Compressor/Pump/Fan** | add work to fluid | adiabatic, dKE & dPE ~0 | w_in = h2 - h1 |
| **Throttle valve** | drop pressure | adiabatic, w=0, dKE & dPE ~0 | **h1 = h2** (isenthalpic) |
| **Heat exchanger** | transfer heat between streams | w=0, dKE & dPE ~0 | sum(m_dot*h)_in = sum(m_dot*h)_out (whole HX adiabatic) |
| **Mixing chamber** | combine streams | w=0, adiabatic, dKE&dPE~0 | sum(m_dot*h)_in = sum(m_dot*h)_out |
| **Pipe/duct flow** | transport | w=0 | q = (h2-h1) + dKE [+ dPE] |

**Throttling note:** for an ideal gas h = h(T) only, so throttling gives T2 = T1. For a real gas/two-phase fluid, temperature changes — the **Joule–Thomson coefficient** mu_JT = (dT/dP) at constant h characterizes this; it is the basis of refrigeration via expansion valves.

**Pump work shortcut (incompressible, reversible):** w_pump = v*(P2 - P1) since v ~ constant for a liquid.

### 4.6 Unsteady (transient) flow — uniform-flow process
For filling/emptying a tank:
```
Mass:   m2 - m1 = sum(m_in) - sum(m_out)
Energy: Q - W = m2*u2 - m1*u1 + sum(m_out*h_out) - sum(m_in*h_in)
```
Inlet/outlet states assumed uniform and constant during the process.

---

## 5. The Second Law of Thermodynamics

### 5.1 Why we need it
The first law says energy is conserved; it does NOT forbid impossible processes (heat flowing cold-to-hot, a ball spontaneously bouncing higher). The second law gives **direction** and a ceiling on conversion of heat to work.

### 5.2 Thermal reservoirs, heat engines, refrigerators
- **Thermal reservoir** — a body large enough that heat transfer doesn't change its temperature.
- **Heat engine** — operates in a cycle; receives Q_H from a hot reservoir, rejects Q_L to a cold reservoir, produces net work W_net = Q_H - Q_L.
  ```
  Thermal efficiency:  eta_th = W_net/Q_H = 1 - Q_L/Q_H
  ```
- **Refrigerator/heat pump** — cycle that moves heat from cold to hot using work input W_net = Q_H - Q_L.
  ```
  COP_refrigerator = Q_L / W_net = Q_L / (Q_H - Q_L)
  COP_heat pump    = Q_H / W_net = Q_H / (Q_H - Q_L) = COP_R + 1
  ```

### 5.3 The two classical statements (equivalent)
- **Kelvin–Planck:** No heat engine can produce net work while exchanging heat with a *single* reservoir. (eta_th < 100% always; you must reject some heat.)
- **Clausius:** No device can transfer heat from a cold body to a hot body with *no* work input.
Violating one violates the other.

### 5.4 Reversible vs irreversible processes
- **Reversible process** — can be reversed leaving no trace on system OR surroundings. Idealization; never achieved.
- **Irreversibilities** (causes of irreversibility): friction, unrestrained expansion, mixing, heat transfer across a finite DT, electrical resistance, inelastic deformation, chemical reactions.
- **Internally reversible** — no irreversibilities within the system. **Totally reversible** — none within OR outside.

### 5.5 The Carnot cycle
Four reversible processes (executed by a heat engine between T_H and T_L):
1. Reversible isothermal heat addition at T_H.
2. Reversible adiabatic (isentropic) expansion T_H -> T_L.
3. Reversible isothermal heat rejection at T_L.
4. Reversible adiabatic (isentropic) compression T_L -> T_H.
On a T–s diagram the Carnot cycle is a **rectangle**.

**Carnot principles:**
1. No engine between two reservoirs can be more efficient than a reversible one.
2. All reversible engines between the same two reservoirs have the same efficiency.

**Carnot efficiency and COPs** (depend ONLY on reservoir temperatures, absolute):
```
eta_Carnot      = 1 - T_L / T_H
COP_R,Carnot    = T_L / (T_H - T_L)
COP_HP,Carnot   = T_H / (T_H - T_L)
```
These set the **upper bound**: eta_real <= eta_Carnot, COP_real <= COP_Carnot.

**Pitfall:** Carnot efficiency requires *absolute* temperature. Using °C gives nonsense.

---

## 6. Entropy

### 6.1 The Clausius inequality and the definition of entropy
```
cyclic integral of (dQ/T) <= 0     (= 0 reversible, < 0 irreversible)
```
Entropy is defined from the reversible part:
```
dS = (dQ/T)_internally reversible       [kJ/K]
S2 - S1 = integral_1^2 (dQ/T)_int rev
```
Entropy is a **property** (path-independent) even though dQ/T is evaluated along a reversible path.

### 6.2 The increase-of-entropy principle (entropy balance)
For ANY process of a closed system:
```
S2 - S1 = integral(dQ/T) + S_gen        with S_gen >= 0
```
- S_gen = 0  -> internally reversible process.
- S_gen > 0  -> irreversible process.
- S_gen < 0  -> **impossible** (this is the second law's teeth).

For an **isolated system** (or system + surroundings = universe): S_gen = dS_total >= 0. The entropy of the universe never decreases.

### 6.3 The T dS (Gibbs) relations
Derived by combining the first law for an internally reversible process with dS = dQ/T:
```
T dS = dU + P dV          (per unit mass:  T ds = du + P dv)
T dS = dH - V dP          (per unit mass:  T ds = dh - v dP)
```
These hold for **any** process between equilibrium states (they relate properties), reversible or not.

### 6.4 Entropy change of substances
- **Pure substances:** read s from tables; in the dome s = s_f + x*s_fg.
- **Incompressible** (liquids, solids): ds = c dT/T  ->  s2 - s1 = c_avg * ln(T2/T1).
- **Ideal gas:** see Section 2.5.

### 6.5 Isentropic processes and isentropic efficiency
An **isentropic** process is reversible + adiabatic. It is the *ideal benchmark* for adiabatic steady-flow devices.

**Isentropic efficiencies** (compare actual to ideal isentropic device between the same inlet state and same exit pressure):
```
Turbine:      eta_T = w_actual / w_isentropic = (h1 - h2a) / (h1 - h2s)
Compressor:   eta_C = w_isentropic / w_actual = (h2s - h1) / (h2a - h1)
Pump:         eta_P = w_isentropic / w_actual = v*(P2 - P1) / (h2a - h1)
Nozzle:       eta_N = KE_actual / KE_isentropic = (h1 - h2a) / (h1 - h2s)
```
Subscript s = isentropic exit state (same P2, s2 = s1); a = actual exit state.
**Pitfall:** the definition *inverts* between work-producing (turbine) and work-consuming (compressor/pump) devices — actual over ideal vs ideal over actual. Always check that eta <= 1.

### 6.6 Reversible steady-flow work
For an internally reversible steady-flow process:
```
w_rev = - integral_1^2 v dP - dKE - dPE
```
Neglecting KE & PE: w_rev = - integral(v dP). Consequences:
- For a **liquid (v ~ const)**: w_rev = -v*(P2 - P1). Pumping a liquid costs little work.
- For a **gas**: v is large, so compressors cost much more work than pumps for the same pressure ratio. This is why **multistage compression with intercooling** is used — it reduces integral(v dP).

### 6.7 Entropy balance for a control volume
```
dS_CV/dt = sum(Q_dot_k / T_k) + sum(m_dot_in * s_in) - sum(m_dot_out * s_out) + S_gen_dot
```
Steady state, single stream, adiabatic:  S_gen_dot = m_dot*(s2 - s1) >= 0.

### 6.8 Worked-example pattern — second law / entropy
1. Define the system or CV; identify reservoirs and their temperatures.
2. Find s at every state (tables or ideal-gas relations).
3. Write the entropy balance; isolate S_gen.
4. If S_gen < 0, you made an error or the process is impossible.
5. For "is this possible/what's the max" questions, set S_gen = 0 to get the reversible limit.

---

## 7. Exergy (Availability) — The Second-Law Accounting of Work Potential

### 7.1 Concept
**Exergy** = the maximum useful work obtainable as a system is brought to equilibrium with a specified **dead state** (environment, subscript 0: T_0, P_0). Exergy is destroyed by irreversibilities; it is NOT conserved.

### 7.2 Dead state
The dead state is thermodynamic equilibrium with the environment: same T_0, P_0, zero velocity, reference elevation. At the dead state a system has zero exergy.

### 7.3 Exergy of a closed system (per unit mass)
```
phi = (u - u_0) + P_0*(v - v_0) - T_0*(s - s_0) + V^2/2 + g*z
```

### 7.4 Flow exergy (per unit mass, for a stream)
```
psi = (h - h_0) - T_0*(s - s_0) + V^2/2 + g*z
```

### 7.5 Reversible work, irreversibility, exergy destruction
```
Exergy destroyed:  X_destroyed = T_0 * S_gen >= 0       (Gouy–Stodola theorem)
Irreversibility:   I = X_destroyed = W_rev - W_useful  (work-producing)
                       or = W_useful - W_rev           (work-consuming)
```

### 7.6 Exergy (second-law) efficiency
```
eta_II = exergy recovered / exergy supplied = 1 - X_destroyed / X_supplied
```
Examples: turbine eta_II = w_actual / w_rev; heater eta_II = exergy gained by stream / exergy of fuel.
**Why it matters:** two devices with the same first-law efficiency can have very different exergy efficiencies — eta_II tells you where the *real* losses are.

### 7.7 Exergy balance (control volume, steady state)
```
sum(X_dot_in) - sum(X_dot_out) - X_dot_destroyed = 0
X_dot_heat = (1 - T_0/T_k) * Q_dot_k       (exergy carried by heat at temperature T_k)
```

---

## 8. Power Cycles — Vapor (Rankine)

### 8.1 Ideal Rankine cycle — four processes
Working fluid: water. Components and processes:
1. **1->2 Pump** (isentropic): compress saturated liquid. w_pump,in = h2 - h1 ≈ v1*(P2 - P1).
2. **2->3 Boiler** (isobaric): add heat. q_in = h3 - h2.
3. **3->4 Turbine** (isentropic): expand to condenser pressure. w_turb,out = h3 - h4.
4. **4->1 Condenser** (isobaric): reject heat. q_out = h4 - h1.

```
w_net = w_turb,out - w_pump,in = q_in - q_out
eta_th = w_net / q_in = 1 - q_out / q_in
Back-work ratio bwr = w_pump,in / w_turb,out   (small for Rankine — a key advantage)
```

### 8.2 Analysis procedure
1. State 1: saturated liquid at condenser pressure -> h1 = h_f(P1), v1 = v_f(P1).
2. State 2: P2 = boiler pressure, s2 = s1 -> h2 = h1 + v1*(P2 - P1).
3. State 3: P3 = P2, T3 given (superheated) -> h3, s3 from superheat table.
4. State 4: P4 = P1, s4 = s3 -> find x4 = (s4 - s_f)/s_fg, then h4 = h_f + x4*h_fg.
5. Compute q_in, q_out, w_net, eta_th.
6. Check turbine exit quality x4 — should be >= ~0.88 to avoid blade erosion.

### 8.3 Improving Rankine efficiency
- **Lower condenser pressure** — raises eta but lowers x4 (more moisture).
- **Superheat the steam** — raises eta and raises x4 (good both ways); limited by metallurgy.
- **Raise boiler pressure** — raises eta but lowers x4.
- **Reheat cycle** — expand partway, return steam to boiler for reheat, expand again. Keeps x4 high while allowing high boiler pressure.
- **Regeneration** — extract (bleed) steam from the turbine to preheat feedwater in **feedwater heaters** (open or closed). Raises average heat-addition temperature -> higher eta.

### 8.4 Actual Rankine cycle
Include pump and turbine isentropic efficiencies; include pressure drops in boiler/condenser and heat loss.

---

## 9. Power Cycles — Gas

### 9.1 Air-standard assumptions (used for all gas cycles below)
1. Working fluid is air, behaving as an ideal gas.
2. All processes internally reversible.
3. Combustion replaced by heat addition from an external source.
4. Exhaust replaced by heat rejection restoring the initial state.
**Cold-air-standard:** additionally assume constant specific heats at room temperature.

### 9.2 Otto cycle (spark-ignition engines) — four processes
1. 1->2 Isentropic compression. 2->3 Constant-volume heat addition.
3. 3->4 Isentropic expansion. 4->1 Constant-volume heat rejection.
```
Compression ratio  r = V_max/V_min = V1/V2
eta_Otto = 1 - 1/r^(k-1)         (cold-air-standard)
```
Efficiency rises with r and with k. Limited by **autoignition/knock**.

### 9.3 Diesel cycle (compression-ignition engines)
1. 1->2 Isentropic compression. 2->3 **Constant-pressure** heat addition.
3. 3->4 Isentropic expansion. 4->1 Constant-volume heat rejection.
```
Cutoff ratio  r_c = V3/V2
eta_Diesel = 1 - (1/r^(k-1)) * [ (r_c^k - 1) / (k*(r_c - 1)) ]
```
For the same r, eta_Otto > eta_Diesel; but Diesels run at much higher r (no knock limit), so real Diesels are more efficient.

### 9.4 Brayton cycle (gas turbines) — four processes
1. 1->2 Isentropic compression (compressor). 2->3 Constant-pressure heat addition (combustor).
3. 3->4 Isentropic expansion (turbine). 4->1 Constant-pressure heat rejection.
```
Pressure ratio  r_p = P2/P1
eta_Brayton = 1 - 1/r_p^((k-1)/k)        (cold-air-standard)
```
**Back-work ratio is large** (bwr ~ 0.4–0.8) — the compressor consumes a big fraction of turbine output, so component efficiencies matter enormously.

**Brayton improvements:**
- **Regeneration** — use hot turbine exhaust to preheat compressor discharge (works only when T4 > T2). Effectiveness eps = (h5 - h2)/(h4 - h2).
- **Intercooling** — multistage compression with cooling between stages (reduces compressor work).
- **Reheat** — multistage expansion with reheating between turbine stages (increases turbine work).
- Intercooling + reheat + regeneration approaches the **Ericsson cycle** limit.

### 9.5 Combined gas–vapor (combined-cycle) plants
Brayton topping cycle's exhaust feeds the boiler of a Rankine bottoming cycle. Combined eta can exceed 60%.

---

## 10. Refrigeration Cycles

### 10.1 Ideal vapor-compression refrigeration cycle — four processes
Working fluid: a refrigerant (R-134a, etc.).
1. **1->2 Compressor** (isentropic): saturated vapor compressed to condenser pressure. w_in = h2 - h1.
2. **2->3 Condenser** (isobaric): reject heat to warm surroundings. q_H = h2 - h3.
3. **3->4 Expansion valve** (throttle, isenthalpic): h4 = h3.
4. **4->1 Evaporator** (isobaric): absorb heat from the refrigerated space. q_L = h1 - h4.
```
COP_R  = q_L / w_in = (h1 - h4) / (h2 - h1)
COP_HP = q_H / w_in = (h2 - h3) / (h2 - h1) = COP_R + 1
```

### 10.2 Analysis procedure
1. State 1: saturated vapor at evaporator pressure -> h1, s1.
2. State 2: P2 = condenser pressure, s2 = s1 -> h2 (superheated).
3. State 3: saturated liquid at condenser pressure -> h3 = h_f(P_cond).
4. State 4: h4 = h3, P4 = P_evap -> x4 = (h4 - h_f)/h_fg.
5. Compute q_L, q_H, w_in, COP.

### 10.3 Why the throttle instead of a turbine?
A turbine would recover a little work, but the work is tiny (liquid-dominated expansion) and a turbine handling a two-phase mixture is impractical and expensive. The throttle is cheap, reliable, and provides flow control.

### 10.4 Actual vapor-compression cycle
Differences from ideal: superheating at evaporator exit (ensures no liquid enters compressor), subcooling at condenser exit (ensures no vapor enters the valve), pressure drops, non-isentropic compressor, heat exchange with surroundings in lines.

### 10.5 Other refrigeration systems
- **Gas refrigeration cycle** — reversed Brayton; used in aircraft and cryogenics.
- **Absorption refrigeration** — uses a heat source (not a compressor) to drive the cycle; ammonia-water or LiBr-water.
- **Cascade systems** — multiple cycles for very low temperatures.

---

## 11. Cycle Summary Tables

### 11.1 Power cycles

| Cycle | Application | Heat-addition process | Heat-rejection process | Ideal efficiency (cold-air-std) |
|---|---|---|---|---|
| Carnot | benchmark | isothermal @ T_H | isothermal @ T_L | 1 - T_L/T_H |
| Rankine | steam power plants | isobaric (boiler) | isobaric (condenser) | 1 - q_out/q_in |
| Otto | gasoline engines | isochoric | isochoric | 1 - 1/r^(k-1) |
| Diesel | diesel engines | isobaric | isochoric | 1 - (1/r^(k-1))*(r_c^k-1)/(k(r_c-1)) |
| Brayton | gas turbines / jets | isobaric | isobaric | 1 - 1/r_p^((k-1)/k) |
| Stirling/Ericsson | (ideal regenerative) | isothermal | isothermal | 1 - T_L/T_H |

### 11.2 Refrigeration cycles

| Cycle | Driven by | Expansion device | Performance metric |
|---|---|---|---|
| Reversed Carnot | benchmark | turbine | COP_R = T_L/(T_H - T_L) |
| Vapor-compression | compressor (work) | throttle valve | COP_R = (h1-h4)/(h2-h1) |
| Gas (reversed Brayton) | compressor (work) | turbine | COP_R = q_L/w_net |
| Absorption | heat source | throttle valve | COP = q_L/q_generator |

---

## 12. Master List of Common Student Pitfalls

1. **Temperature units** — always Kelvin/Rankine in any ratio, efficiency, or gas law. °C only works for *differences*.
2. **Pressure** — always absolute in equations.
3. **Sign convention** — pick Q-in positive, W-out positive, and never switch.
4. **Region identification** — always check whether you're in the compressed-liquid, two-phase, or superheated region *before* reaching for a table.
5. **Quality is a mass fraction**, not a volume fraction; defined only inside the dome.
6. **u vs h** — use u for closed rigid systems, h for flow / constant-pressure. Q = dH only at constant P.
7. **Isentropic efficiency inverts** between turbines (actual/ideal) and compressors/pumps (ideal/actual). eta must end up <= 1.
8. **Adiabatic != isentropic.** Only *reversible* adiabatic is isentropic.
9. **Throttling: h1 = h2**, not T1 = T2 (except ideal gas).
10. **Pump work** uses w = v*DP because liquids are ~incompressible; don't use it for gases.
11. **Carnot is a ceiling**, not a prediction; real eta is always lower.
12. **S_gen >= 0 always** — a negative result means an error or an impossible process.
13. **Exergy is destroyed, not conserved.** Energy balances and exergy balances are different accounting systems.
14. **Reference states differ between substances** — never mix property tables for two different fluids.
15. **Back-work ratio** — for Brayton it is large; component inefficiencies can kill net output entirely.
16. **Interpolation** — always interpolate; using the nearest table row introduces avoidable error.

---

## Open-source sources used

- **Yan, Claire.** *Introduction to Engineering Thermodynamics.* Engineering LibreTexts / University of British Columbia (CC-licensed). https://eng.libretexts.org/Bookshelves/Mechanical_Engineering/Introduction_to_Engineering_Thermodynamics_(Yan) — used for first law (closed/open systems), entropy and second law (Kelvin–Planck/Clausius statements, entropy generation, Carnot cycle), and steady-flow device treatment.
- **Cleynen, Olivier.** *Engineering Thermodynamics* (free open textbook). https://thermodynamicsbook.com/ — used for property-of-pure-substance treatment, cycle analysis, and gas-cycle structure.
- **Urieli, Israel.** *Engineering Thermodynamics — A Graphical Approach* (Creative Commons), Ohio University; and its OER successor "Thermodynamics for Engineers." OER Commons: https://oercommons.org/courseware/lesson/101623 — used for graphical cycle-analysis methods (Rankine, Brayton, vapor-compression).
- **Introduction to Engineering Thermodynamics**, Open Textbook Library. https://open.umn.edu/opentextbooks/textbooks/1252 — cross-reference for property-table methods and ideal-gas relations.
- **MIT OpenCourseWare**, Thermodynamics course materials (2.005 / 16.unified thermodynamics modules) — cross-reference for second-law statements, availability/exergy, and cycle efficiency derivations.
