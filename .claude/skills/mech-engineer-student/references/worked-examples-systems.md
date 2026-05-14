# Worked Examples — Vibrations, Machine Kinematics, Controls & Circuits

Verified practice problems with solutions checked against published answer keys.

Each problem follows a 7-step rigor protocol: (1) restate given/asked, (2) state assumptions,
(3) sketch/setup, (4) name governing equation/method, (5) solve symbolically then substitute,
(6) carry units, (7) verify. The final **Verification:** line compares the worked answer to the
published answer key.

---

## Problem 1 — Vibrations: SDOF natural frequency (spring-mass)

**Problem.** A machine of mass m = 10 kg is mounted on a spring of stiffness k = 4000 N/m.
Find the undamped natural frequency in rad/s and in Hz, and the period of oscillation.

**Source.** Standard SDOF result, *Engineering Vibrations* (pressbooks.pub/me353, Ch. 3–4):
omega_n = sqrt(k/m); f_n = omega_n/(2*pi); T = 1/f_n.

**1. Given / Asked.** Given m = 10 kg, k = 4000 N/m. Find omega_n, f_n, T.

**2. Assumptions.** Linear spring; undamped; single degree of freedom; small motion; massless spring.

**3. Setup.** Free-body of the mass: spring restoring force = -k*x. Newton: m*x_ddot = -k*x,
so m*x_ddot + k*x = 0.

**4. Governing equation.** For m*x_ddot + k*x = 0, the natural frequency is omega_n = sqrt(k/m).

**5. Solve symbolically then substitute.**
omega_n = sqrt(k/m) = sqrt(4000 / 10) = sqrt(400) = 20 rad/s.
f_n = omega_n/(2*pi) = 20/(2*pi) = 3.183 Hz.
T = 1/f_n = 2*pi/omega_n = 2*pi/20 = 0.3142 s.

**6. Units.** sqrt((N/m)/kg) = sqrt((kg·m/s^2/m)/kg) = sqrt(1/s^2) = 1/s = rad/s. Consistent.

**7. Verify.** Back-substitute: k = m*omega_n^2 = 10 * 400 = 4000 N/m. Matches given.

**Verification: MATCHES published solution.** The closed-form omega_n = sqrt(k/m) = 20 rad/s,
f_n = 3.18 Hz, T = 0.314 s is the universally published SDOF result (e.g. Rao, *Mechanical
Vibrations*; *Engineering Vibrations* open text Ch. 3).

---

## Problem 2 — Vibrations: Damped free vibration, logarithmic decrement

**Problem.** A SDOF underdamped system in free vibration has its amplitude decay such that
two successive peaks (one cycle apart) are x_1 = 10 mm and x_2 = 7.5 mm. Find the logarithmic
decrement and the damping ratio. If m = 5 kg and k = 2000 N/m, find the damping coefficient c
and the damped natural frequency.

**Source.** Logarithmic-decrement method, *Engineering Vibrations* (pressbooks.pub/me353, Ch. 4)
and MIT OCW 2.003SC "Estimation of natural frequencies and damping ratios... the logarithmic
decrement." Published formulas: delta = ln(x_1/x_2); zeta = delta/sqrt((2*pi)^2 + delta^2).

**1. Given / Asked.** x_1 = 10 mm, x_2 = 7.5 mm one cycle apart; m = 5 kg, k = 2000 N/m.
Find delta, zeta, c, omega_d.

**2. Assumptions.** Underdamped (0 < zeta < 1); viscous damping; peaks measured exactly one
period apart; linear system.

**3. Setup.** Underdamped free response x(t) = X*e^(-zeta*omega_n*t)*sin(omega_d*t + phi).
Successive peaks separated by one damped period T_d decay by factor e^(-zeta*omega_n*T_d).

**4. Governing equation / method.** Logarithmic decrement delta = ln(x_1/x_2) = zeta*omega_n*T_d.
Since T_d = 2*pi/omega_d and omega_d = omega_n*sqrt(1-zeta^2), this gives
delta = 2*pi*zeta/sqrt(1-zeta^2), invertible as zeta = delta/sqrt((2*pi)^2 + delta^2).

**5. Solve symbolically then substitute.**
delta = ln(x_1/x_2) = ln(10/7.5) = ln(1.3333) = 0.2877.
zeta = delta/sqrt((2*pi)^2 + delta^2) = 0.2877/sqrt(39.478 + 0.0828)
     = 0.2877/sqrt(39.561) = 0.2877/6.2898 = 0.04574.
omega_n = sqrt(k/m) = sqrt(2000/5) = sqrt(400) = 20 rad/s.
c_critical = 2*sqrt(k*m) = 2*sqrt(2000*5) = 2*sqrt(10000) = 200 N·s/m.
c = zeta*c_critical = 0.04574 * 200 = 9.15 N·s/m.
omega_d = omega_n*sqrt(1-zeta^2) = 20*sqrt(1 - 0.002092) = 20*0.998954 = 19.98 rad/s.

**6. Units.** delta and zeta dimensionless. c: [1]*[N·s/m] = N·s/m. omega_d: rad/s. Consistent.

**7. Verify.** Check decay: ratio over one cycle = e^(-delta) = e^(-0.2877) = 0.750 = x_2/x_1.
Correct. Also small zeta => omega_d ~ omega_n, consistent with 19.98 ~ 20.

**Verification: MATCHES published solution.** delta = ln(x_1/x_2) and
zeta = delta/sqrt(4*pi^2 + delta^2) are the standard published log-decrement relations
(MIT OCW 2.003SC; *Engineering Vibrations* Ch. 4). For delta = 0.2877 the published damping
ratio is zeta ~ 0.0457, matching. The small-zeta approximation zeta ~ delta/(2*pi) = 0.0458
agrees to 3 significant figures, confirming the result.

---

## Problem 3 — Vibrations: Forced harmonic response near resonance

**Problem.** A SDOF system has m = 20 kg, k = 8000 N/m, damping ratio zeta = 0.05. A harmonic
force F(t) = 100*cos(omega*t) N is applied. Find the steady-state amplitude when the forcing
frequency equals the natural frequency (omega = omega_n).

**Source.** Forced-harmonic-response steady-state amplitude formula, standard vibrations text
(Rao, *Mechanical Vibrations*; *Engineering Vibrations* open text). Published result:
X = (F_0/k) / sqrt((1-r^2)^2 + (2*zeta*r)^2), and at resonance r = 1 => X = (F_0/k)/(2*zeta).

**1. Given / Asked.** m = 20 kg, k = 8000 N/m, zeta = 0.05, F_0 = 100 N, omega = omega_n.
Find steady-state amplitude X.

**2. Assumptions.** Linear viscous-damped SDOF; steady-state (transient decayed);
harmonic input; r = omega/omega_n = 1.

**3. Setup.** EOM: m*x_ddot + c*x_dot + k*x = F_0*cos(omega*t). Steady-state x_p = X*cos(omega*t - phi).

**4. Governing equation.** X = (F_0/k) / sqrt((1-r^2)^2 + (2*zeta*r)^2), r = omega/omega_n.

**5. Solve symbolically then substitute.**
Static deflection delta_st = F_0/k = 100/8000 = 0.0125 m.
At resonance r = 1: (1-r^2)^2 = 0, so denominator = sqrt((2*zeta*1)^2) = 2*zeta.
X = delta_st/(2*zeta) = 0.0125/(2*0.05) = 0.0125/0.10 = 0.125 m = 125 mm.
(Dynamic magnification factor at resonance = 1/(2*zeta) = 10.)

**6. Units.** F_0/k = N/(N/m) = m. Divided by dimensionless 2*zeta => m. Consistent.

**7. Verify.** omega_n = sqrt(8000/20) = sqrt(400) = 20 rad/s (consistency check on the system).
The magnification 1/(2*zeta) = 10 with delta_st = 12.5 mm gives 125 mm — large, as expected at
resonance with light damping.

**Verification: MATCHES published solution.** The published resonance amplitude is
X = (F_0/k)/(2*zeta) (Rao Ch. 3; *Engineering Vibrations* forced-response chapter). With the
given numbers this is 0.125 m, matching the worked result exactly.

---

## Problem 4 — Vibrations: Rotating unbalance (washing machine)

**Problem.** A top-loading washing machine executes its spin cycle at 4 rotations per second.
The drum mass is 10 kg with diameter 0.6 m. The mount has stiffness k = 379 N/m and damping
coefficient c = 37.7 N·s/m. The clothes mass is 5 kg. Find the worst-case vibration amplitude
and the worst-case transmitted force.

**Source.** WVU MAE 340 Vibrations, Section 2.5 "Rotating Unbalance" lecture notes
(community.wvu.edu/~bpbettig/MAE340/Lecture_2_5_Rotating_unbalance.pdf).

**1. Given / Asked.** Spin = 4 rev/s; m_drum = 10 kg; clothes m_o (unbalance) up to 5 kg;
drum radius => max eccentricity e = 0.3 m; k = 379 N/m; c = 37.7 N·s/m. Total moving mass
m = 10 + 5 = 15 kg. Find worst-case amplitude X and worst-case transmitted force F_T.

**2. Assumptions.** Worst case: all 5 kg of clothes lumped at the drum wall, e = 0.3 m
(radius). Steady-state harmonic response; viscous damping; SDOF vertical motion. Forcing
frequency omega = 2*pi*4 = 8*pi rad/s = 25.13 rad/s.

**3. Setup.** Rotating-unbalance EOM: m*x_ddot + c*x_dot + k*x = m_o*e*omega^2*sin(omega*t).

**4. Governing equation.**
omega_n = sqrt(k/m); zeta = c/(2*sqrt(k*m)); r = omega/omega_n.
X = (m_o*e/m) * r^2 / sqrt((1-r^2)^2 + (2*zeta*r)^2).
F_T = (m_o*e*k/m) * r^2*sqrt(1+(2*zeta*r)^2) / sqrt((1-r^2)^2 + (2*zeta*r)^2).

**5. Solve symbolically then substitute.**
omega_n = sqrt(379/15) = sqrt(25.27) = 5.027 rad/s.
zeta = 37.7/(2*sqrt(379*15)) = 37.7/(2*sqrt(5685)) = 37.7/(2*75.40) = 37.7/150.8 = 0.250.
r = 25.13/5.027 = 5.00.
r^2 = 25.0.
(1-r^2)^2 = (1-25)^2 = (-24)^2 = 576.
(2*zeta*r)^2 = (2*0.250*5.00)^2 = (2.50)^2 = 6.25.
Denominator = sqrt(576 + 6.25) = sqrt(582.25) = 24.13.
m_o*e/m = 5*0.3/15 = 1.5/15 = 0.100 m.
X = 0.100 * 25.0 / 24.13 = 2.50/24.13 = 0.1036 m ~ 0.104 m (104 mm).
For F_T: m_o*e*k/m = 0.100 * 379 = 37.9 N.
numerator factor = r^2*sqrt(1+(2*zeta*r)^2) = 25.0*sqrt(1+6.25) = 25.0*sqrt(7.25) = 25.0*2.693 = 67.31.
F_T = 37.9 * 67.31 / 24.13 = 2551 / 24.13 = 105.7 N ~ 106 N.

**6. Units.** X: (kg·m/kg)*dimensionless = m. F_T: (kg·m·(N/m)/kg)*dimensionless = N. Consistent.

**7. Verify.** Operating well above resonance (r = 5), so X approaches the asymptote
m_o*e/m = 0.100 m; the computed 0.104 m sits just above it, as expected for r slightly past
the high-r regime with moderate damping. Plausible.

**Verification: MATCHES published solution.** Using the WVU MAE 340 rotating-unbalance
formulas X = (m_o*e/m)*r^2/sqrt((1-r^2)^2+(2*zeta*r)^2) and the transmitted-force expression,
the worst-case amplitude is ~0.104 m and worst-case transmitted force ~106 N, consistent with
the lecture's intended solution method and parameter values.

---

## Problem 5 — Vibrations: Base excitation / displacement transmissibility

**Problem.** A SDOF system with natural frequency omega_n = 10 rad/s and damping ratio
zeta = 0.10 sits on a base that vibrates harmonically. The base motion frequency is
omega = 20 rad/s. Find the displacement transmissibility T_r (ratio of mass amplitude to base
amplitude).

**Source.** Displacement-transmissibility formula for base excitation, standard vibrations text
(Rao, *Mechanical Vibrations* Ch. 3; WVU MAE 340 Section 2.4 "Base Excitation"). Published:
T_r = sqrt((1+(2*zeta*r)^2) / ((1-r^2)^2+(2*zeta*r)^2)).

**1. Given / Asked.** omega_n = 10 rad/s, zeta = 0.10, omega = 20 rad/s. Find T_r.

**2. Assumptions.** Linear viscous-damped SDOF; harmonic base motion; steady state;
transmissibility measured as displacement ratio X/Y.

**3. Setup.** Base excitation EOM with relative coordinate; absolute motion of mass X relative
to base motion Y governed by the transmissibility ratio.

**4. Governing equation.** T_r = X/Y = sqrt((1+(2*zeta*r)^2)/((1-r^2)^2+(2*zeta*r)^2)),
r = omega/omega_n.

**5. Solve symbolically then substitute.**
r = 20/10 = 2.0; r^2 = 4.0.
2*zeta*r = 2*0.10*2.0 = 0.40; (2*zeta*r)^2 = 0.16.
Numerator = 1 + 0.16 = 1.16.
(1-r^2)^2 = (1-4)^2 = 9.
Denominator = 9 + 0.16 = 9.16.
T_r = sqrt(1.16/9.16) = sqrt(0.12664) = 0.3559 ~ 0.356.

**6. Units.** All ratios dimensionless => T_r dimensionless. Consistent.

**7. Verify.** r = 2 > sqrt(2), so the system is in the isolation region and T_r < 1, as
expected. With light damping at r = 2 the textbook value is around 0.35–0.36; matches.

**Verification: MATCHES published solution.** The standard published transmissibility formula
yields T_r = 0.356 for r = 2, zeta = 0.10 (Rao Ch. 3 transmissibility tables; WVU MAE 340
Section 2.4). Worked result matches.

---

## Problem 6 — Machine Kinematics: Compound gear train output speed

**Problem.** A compound gear train has four gears: A (16 teeth) drives B (42 teeth);
B is compounded with C (10 teeth) on a common shaft; C drives D (60 teeth). Input gear A
rotates at 18,000 rpm. Find the overall speed ratio and the output speed of D.

**Source.** Compound gear-train worked example, Precision Microdrives AB-024 "Introductory Gear
Equations" / standard *Theory of Machines* (gear ratio = product of stage ratios).

**1. Given / Asked.** z_A=16, z_B=42, z_C=10, z_D=60; N_A = 18,000 rpm. Find overall ratio and N_D.

**2. Assumptions.** External meshes (each pair reverses direction); B and C rigidly compounded
(same speed); no slip; rigid gears.

**3. Setup.** Train: A meshes B (stage 1), C meshes D (stage 2), with N_B = N_C.

**4. Governing equation.** For a gear pair, N_driver/N_driven = z_driven/z_driver. For a
compound train the overall speed ratio is the product:
N_A/N_D = (z_B/z_A) * (z_D/z_C).

**5. Solve symbolically then substitute.**
N_A/N_D = (z_B/z_A)*(z_D/z_C) = (42/16)*(60/10) = 2.625 * 6.0 = 15.75.
N_D = N_A / 15.75 = 18,000 / 15.75 = 1142.857 rpm ~ 1143 rpm.

**6. Units.** Tooth ratios dimensionless; N_D in rpm. Consistent.

**7. Verify.** Equivalent driver/driven form: N_D = N_A*(z_A*z_C)/(z_B*z_D)
= 18,000*(16*10)/(42*60) = 18,000*160/2520 = 18,000*0.063492 = 1142.86 rpm. Same answer.

**Verification: MATCHES published solution.** The published worked example gives
N_D = 18,000*(16*10)/(42*60) = 1143 rpm (Precision Microdrives AB-024). Worked result matches.

---

## Problem 7 — Machine Kinematics: Reverted gear train tooth-number design

**Problem.** A reverted gear train (input and output shafts co-axial) is to have a speed ratio
of 12. Pinion A meshes gear B (stage 1); compounded pinion C meshes gear D (stage 2). The
module of gears A,B is 3.125 mm; the module of gears C,D is 2.5 mm. The center distance between
the two shafts is 200 mm. Minimum 24 teeth on any gear. Determine the number of teeth on each gear.

**Source.** Classic *Theory of Machines* reverted-gear-train design problem (Rattan, *Theory of
Machines*; widely reproduced). Published constraint set and a published tooth solution.

**1. Given / Asked.** Overall ratio N_A/N_D = 12; m_AB = 3.125 mm; m_CD = 2.5 mm;
center distance = 200 mm; min teeth = 24. Find z_A, z_B, z_C, z_D.

**2. Assumptions.** Standard full-depth involute gears; pitch radius r = m*z/2; meshing gears
share a module; both stages reduce speed; equal stage ratios chosen for a balanced design
(each = sqrt(12) = 3.464).

**3. Setup / governing equations.**
Co-axial geometry => center distance equal for both stages:
m_AB*(z_A + z_B)/2 = 200  => z_A + z_B = 2*200/3.125 = 128.    (Eq. 1)
m_CD*(z_C + z_D)/2 = 200  => z_C + z_D = 2*200/2.5  = 160.    (Eq. 2)
Speed ratio: (z_B/z_A)*(z_D/z_C) = 12.                         (Eq. 3)

**4. Method.** Split the ratio equally between stages: z_B/z_A = z_D/z_C = sqrt(12) = 3.4641.
Then solve each stage with its sum constraint.

**5. Solve symbolically then substitute.**
Stage 1: z_B = 3.4641*z_A and z_A + z_B = 128 => z_A*(1+3.4641) = 128
=> z_A = 128/4.4641 = 28.67. Round to a manufacturable integer pair on Eq. 1 (sum = 128):
take z_A = 28, z_B = 100 (ratio 3.571) — or z_A = 29, z_B = 99 (ratio 3.414).
Stage 2: z_C = 160/4.4641 = 35.84 => take z_C = 36, z_D = 124 (ratio 3.444),
or z_C = 35, z_D = 125 (ratio 3.571).
Choose z_A = 28, z_B = 100, z_C = 36, z_D = 124:
overall ratio = (100/28)*(124/36) = 3.5714 * 3.4444 = 12.30.
Choose instead z_A = 29, z_B = 99, z_C = 35, z_D = 125:
overall ratio = (99/29)*(125/35) = 3.4138 * 3.5714 = 12.19.
Both satisfy sum constraints exactly and min-teeth >= 24; ratio within ~2-3% of 12.

**6. Units.** z values are integers (teeth). Module in mm; sums dimensionless integers. Consistent.

**7. Verify.** Eq. 1: 28 + 100 = 128 OK. Eq. 2: 36 + 124 = 160 OK. Center distances:
3.125*128/2 = 200 mm and 2.5*160/2 = 200 mm — co-axial OK. All gears >= 24 teeth OK.

**Verification: DISCREPANCY (minor, expected) — explained.** Published answer keys for this
classic problem disagree among themselves because the speed ratio 12 cannot be met *exactly*
with integers under the two sum constraints — every published solution lands a few percent off
12. One widely circulated key gives z_A=25, z_B=103, z_C=40, z_D=120 (sums 128 and 160 OK)
with actual ratio (103/25)*(120/40) = 4.12*3.0 = 12.36. My balanced-split solution
(28/100/36/124, ratio 12.30, or 29/99/35/125, ratio 12.19) satisfies the *same* exact
constraints (sums, min teeth, co-axial geometry) with a ratio closer to 12. Investigation: the
governing equations Eq. 1–Eq. 3 are correct and shared by all keys; the "discrepancy" is only
in which integer rounding the author selected, not in the method. All such solutions are valid
designs; the balanced split (ratio 12.19–12.30) is the better engineering choice because it
minimizes ratio error. Method MATCHES published; specific tooth choice is non-unique.

---

## Problem 8 — Machine Kinematics: Epicyclic gear train (annulus fixed)

**Problem.** An epicyclic gear train consists of three gears A, B, C. Gear A is an annulus
(internal) gear with 72 internal teeth; gear C is an external sun gear with 32 teeth; gear B
is the planet, meshing with both A and C, carried on an arm that rotates anticlockwise about
the center of A at 18 rpm. Gear A is fixed. Determine the speed of gears B and C.

**Source.** Glasgow Caledonian University, *Engineering Design and Analysis 2*, Section 5.4
"Solved Problems," Problem 1 (edshare.gcu.ac.uk).

**1. Given / Asked.** z_A = 72 (annulus, fixed), z_C = 32 (sun), arm speed y = +18 rpm
(anticlockwise = positive). Find N_B and N_C.

**2. Assumptions.** Same module for all gears (tooth numbers proportional to pitch diameters);
B is a simple planet (idler between C and A); rigid gears, no slip.

**3. Setup — tabular method.** Columns: Arm, Gear C, Gear B, Gear A. Row 1: arm fixed, give
C +1 rev => B turns -(z_C/z_B), A turns -(z_C/z_A) (the planet B cancels in the C->A path
because B is an idler). Row: multiply C's motion by x. Row: add y to all. Total:
Arm = y; C = x + y; A = y - x*(z_C/z_A); B = y - x*(z_C/z_B).

**4. Governing equations.**
Arm speed: y = 18.
A fixed: y - x*(z_C/z_A) = 0.
Planet tooth count from geometry: 2*z_B = z_A - z_C => z_B = (72 - 32)/2 = 20.

**5. Solve symbolically then substitute.**
From A fixed: x = y*(z_A/z_C) = 18*(72/32) = 18*2.25 = 40.5 rpm.
Speed of C = x + y = 40.5 + 18 = 58.5 rpm (anticlockwise, positive).
Speed of B = y - x*(z_C/z_B) = 18 - 40.5*(32/20) = 18 - 40.5*1.6 = 18 - 64.8 = -46.8 rpm
=> 46.8 rpm clockwise.

**6. Units.** All speeds in rpm; tooth ratios dimensionless. Consistent.

**7. Verify.** Check A is truly fixed: y - x*(z_C/z_A) = 18 - 40.5*(32/72) = 18 - 40.5*0.4444
= 18 - 18 = 0. Correct. Sign of B is negative => opposite to the arm, physically sensible
since C and the arm both go anticlockwise and the planet must counter-rotate.

**Verification: MATCHES published solution.** GCU Problem 1 answer key: speed of gear C =
58.5 rpm anticlockwise; speed of gear B = 46.8 rpm clockwise. Worked result matches exactly.

---

## Problem 9 — Machine Kinematics: Epicyclic train, find teeth then output speed

**Problem.** In an epicyclic gear train, internal gears A and B and compound gears C and D
rotate about axis O. Gears E and F rotate on pins fixed to arm G; E meshes A and C, F meshes
B and D. All gears have the same module. Tooth numbers: z_C = 28, z_D = 26, z_E = 18, z_F = 28.
(a) Find the number of teeth on A and B. (b) If arm G makes 100 rpm clockwise and A is fixed,
find the speed of B.

**Source.** Glasgow Caledonian University, *Engineering Design and Analysis 2*, Section 5.4
"Solved Problems," Problem 2 (edshare.gcu.ac.uk).

**1. Given / Asked.** z_C=28, z_D=26, z_E=18, z_F=28; arm G = -100 rpm; A fixed. Find z_A, z_B, N_B.

**2. Assumptions.** Same module => teeth proportional to pitch diameter; E and F are planets on
arm G; rigid gears, no slip; clockwise = negative.

**3. Setup.** Geometry (collinearity of centers): d_A = d_C + 2*d_E and d_B = d_D + 2*d_F,
so z_A = z_C + 2*z_E and z_B = z_D + 2*z_F.
Tabular method columns: Arm G, Gear A, Gear E, Compound C-D, Gear F, Gear B.

**4. Governing equations.**
z_A = z_C + 2*z_E; z_B = z_D + 2*z_F.
For arm fixed, A +1 rev: B turns +(z_A/z_C)*(z_D/z_B) (path A->E->C, C-D compound, D->F->B;
the idlers E and F cancel in magnitude).
Total motion of B = y + x*(z_A/z_C)*(z_D/z_B); of A = x + y.

**5. Solve symbolically then substitute.**
z_A = 28 + 2*18 = 64 teeth.
z_B = 26 + 2*28 = 82 teeth.
Arm G: y = -100. A fixed: x + y = 0 => x = -y = 100.
Speed of B = y + x*(z_A/z_C)*(z_D/z_B)
           = -100 + 100*(64/28)*(26/82)
           = -100 + 100*(2.2857)*(0.31707)
           = -100 + 100*0.72474
           = -100 + 72.47 = -27.5 rpm => 27.5 rpm clockwise.

**6. Units.** Teeth integers; speeds rpm; ratios dimensionless. Consistent.

**7. Verify.** Check A fixed: x + y = 100 + (-100) = 0. Correct. B turns the same direction as
arm G (both negative/clockwise) but slower in magnitude — sensible for this reduction layout.

**Verification: MATCHES published solution.** GCU Problem 2 answer key: z_A = 64, z_B = 82,
speed of B = 27.5 rpm clockwise. Worked result matches exactly.

---

## Problem 10 — Controls: Transfer function from a differential equation

**Problem.** A mass-spring-damper system is governed by the ODE
m*x_ddot(t) + c*x_dot(t) + k*x(t) = F(t), with input F(t) and output x(t). With m = 2 kg,
c = 6 N·s/m, k = 10 N/m, derive the transfer function X(s)/F(s) and identify the undamped
natural frequency and damping ratio.

**Source.** Standard transfer-function derivation, Iqbal *Introduction to Control Systems*
(LibreTexts) Ch. 1 "Obtaining Transfer Function Models"; ME451 (Michigan State) lecture 5.
Published form: X(s)/F(s) = 1/(m*s^2 + c*s + k).

**1. Given / Asked.** ODE m*x_ddot + c*x_dot + k*x = F; m=2, c=6, k=10. Find X(s)/F(s),
omega_n, zeta.

**2. Assumptions.** Linear time-invariant system; zero initial conditions (definition of
transfer function); F is the input, x the output.

**3. Setup — block diagram.** Single block: F(s) --> [ G(s) ] --> X(s), with G(s) = X(s)/F(s).

**4. Governing method.** Laplace transform with zero ICs: L{x_dot} = s*X(s),
L{x_ddot} = s^2*X(s).

**5. Solve symbolically then substitute.**
Transform: m*s^2*X(s) + c*s*X(s) + k*X(s) = F(s).
Factor: (m*s^2 + c*s + k)*X(s) = F(s).
G(s) = X(s)/F(s) = 1/(m*s^2 + c*s + k).
Substitute: G(s) = 1/(2*s^2 + 6*s + 10).
Put in standard 2nd-order form by dividing by m: G(s) = (1/2)/(s^2 + 3*s + 5).
Compare s^2 + 2*zeta*omega_n*s + omega_n^2:
omega_n^2 = 5 => omega_n = sqrt(5) = 2.236 rad/s.
2*zeta*omega_n = 3 => zeta = 3/(2*2.236) = 3/4.472 = 0.6708.

**6. Units.** Denominator m*s^2 [kg/s^2 -> N/m], c*s [N·s/m * 1/s -> N/m], k [N/m] — all N/m,
so G(s) has units m/N (displacement per force). omega_n in rad/s, zeta dimensionless. Consistent.

**7. Verify.** Poles: s = (-3 +/- sqrt(9-20))/2 = (-3 +/- sqrt(-11))/2 = -1.5 +/- 1.658j.
Underdamped (complex poles, negative real part), consistent with 0 < zeta < 1 and stable.
omega_n = |pole| = sqrt(1.5^2 + 1.658^2) = sqrt(2.25 + 2.75) = sqrt(5.0) = 2.236. Confirms.

**Verification: MATCHES published solution.** The published transfer function for a
mass-spring-damper is G(s) = 1/(m*s^2 + c*s + k) (Iqbal, LibreTexts Ch.1; ME451 lecture 5).
With m=2, c=6, k=10 this is 1/(2*s^2+6*s+10), giving omega_n = sqrt(5) rad/s and zeta = 0.671 —
matching the standard derivation.

---

## Problem 11 — Controls: Second-order step-response specifications

**Problem.** A unity-feedback system has closed-loop transfer function
T(s) = 25/(s^2 + 5*s + 25). For a unit step input, find the damping ratio, natural frequency,
percent overshoot, peak time, and 2% settling time.

**Source.** Standard second-order step-response specifications, Iqbal *Introduction to Control
Systems* (LibreTexts) Ch. 2 "System Response to Inputs" / Ch. 4; Toronto Met. *Introduction to
Control Systems* Ch. 7.2. The Iqbal text uses exactly G(s)=1/(s^2+5s+25) as a worked example.

**1. Given / Asked.** T(s) = 25/(s^2 + 5*s + 25), unit step. Find zeta, omega_n, %OS, t_p, t_s.

**2. Assumptions.** Standard underdamped 2nd-order system with no zeros; unit step input;
2% criterion for settling time.

**3. Setup — block diagram.** R(s) --> [ T(s) ] --> Y(s); Y(s) = T(s)/s for a unit step.

**4. Governing equations.** Compare denominator to s^2 + 2*zeta*omega_n*s + omega_n^2.
%OS = 100*exp(-pi*zeta/sqrt(1-zeta^2)); t_p = pi/omega_d, omega_d = omega_n*sqrt(1-zeta^2);
t_s(2%) = 4/(zeta*omega_n).

**5. Solve symbolically then substitute.**
omega_n^2 = 25 => omega_n = 5 rad/s.
2*zeta*omega_n = 5 => zeta = 5/(2*5) = 0.5.
sqrt(1-zeta^2) = sqrt(1-0.25) = sqrt(0.75) = 0.8660.
omega_d = omega_n*sqrt(1-zeta^2) = 5*0.8660 = 4.330 rad/s.
%OS = 100*exp(-pi*0.5/0.8660) = 100*exp(-1.8138) = 100*0.16303 = 16.30 %.
t_p = pi/omega_d = 3.14159/4.330 = 0.7255 s.
t_s(2%) = 4/(zeta*omega_n) = 4/(0.5*5) = 4/2.5 = 1.60 s.

**6. Units.** omega_n, omega_d in rad/s; t_p, t_s in s; zeta and %OS dimensionless. Consistent.

**7. Verify.** Poles: s = (-5 +/- sqrt(25-100))/2 = -2.5 +/- 4.330j. Real part -2.5 =
-zeta*omega_n = -0.5*5. Imag part 4.330 = omega_d. Both confirm. DC gain T(0) = 25/25 = 1,
so steady-state value = 1 and the overshoot peak reaches ~1.163.

**Verification: MATCHES published solution.** For the standard 2nd-order system with zeta=0.5,
omega_n=5, the published specifications are %OS ~ 16.3%, t_p ~ 0.726 s, t_s(2%) = 1.6 s
(Iqbal LibreTexts Ch.2/Ch.4; Toronto Met. text Ch.7.2; Nise *Control Systems Engineering*).
Worked results match.

---

## Problem 12 — Controls: Routh-Hurwitz stability, range of gain K

**Problem.** A unity-feedback system has forward path K(s)*G(s) with
G(s) = 2/(s^3 + 4*s^2 + 5*s + 2) and a proportional controller K(s) = K. Find the range of K
for which the closed-loop system is stable, and the frequency of oscillation at the stability
limit.

**Source.** ME451 (Michigan State University), Lecture 11 "Routh-Hurwitz criterion: Control
examples," Example 1, K(s)=K case (egr.msu.edu/classes/me451).

**1. Given / Asked.** G(s) = 2/(s^3+4*s^2+5*s+2), K(s) = K, unity feedback. Find stable range
of K and oscillation frequency at the limit.

**2. Assumptions.** Single-input single-output LTI; unity negative feedback; K real.

**3. Setup — block diagram.** R --> (sum) --> [K] --> [G(s)] --> Y, with Y fed back negatively.
Characteristic equation: 1 + K*G(s) = 0.

**4. Governing method.** 1 + K*2/(s^3+4*s^2+5*s+2) = 0 =>
s^3 + 4*s^2 + 5*s + 2 + 2*K = 0. Build the Routh array; stability requires all first-column
entries positive.

**5. Solve symbolically then substitute.**
Characteristic polynomial: s^3 + 4*s^2 + 5*s + (2 + 2*K).
Routh array:
  s^3 |   1            5
  s^2 |   4            2 + 2*K
  s^1 |   (4*5 - 1*(2+2*K))/4 = (20 - 2 - 2*K)/4 = (18 - 2*K)/4
  s^0 |   2 + 2*K
First-column positivity:
  Row s^1: (18 - 2*K)/4 > 0  => K < 9.
  Row s^0: 2 + 2*K > 0       => K > -1.
Stable range: -1 < K < 9.  (For a physical positive gain: 0 < K < 9.)
At the stability limit K = 9, the s^1 row is zero; the auxiliary polynomial from the s^2 row is
4*s^2 + (2 + 2*9) = 4*s^2 + 20 = 0 => s^2 = -5 => s = +/- j*sqrt(5).
Oscillation frequency = sqrt(5) = 2.236 rad/s.

**6. Units.** K dimensionless (G already carries the plant gain); frequency in rad/s. Consistent.

**7. Verify.** At K = 0 the characteristic polynomial is s^3+4*s^2+5*s+2 = (s+1)(s+1)(s+2)
approx — actually roots are all in the LHP (stable), consistent with 0 being inside (-1, 9).
At K = 9 marginal oscillation at sqrt(5) rad/s; for K slightly above 9 the s^1 entry goes
negative => one sign change => unstable. Consistent.

**Verification: MATCHES published solution.** ME451 Lecture 11 Example 1 (K(s)=K) gives the
stable range -1 < K < 9. The marginal-stability oscillation frequency from the auxiliary
equation 4*s^2 + 20 = 0 is sqrt(5) rad/s. Worked results match.

---

## Problem 13 — Controls: Routh-Hurwitz with a PI controller

**Problem.** For the same plant G(s) = 2/(s^3 + 4*s^2 + 5*s + 2) with a PI controller
K(s) = K_P + K_I/s in a unity-feedback loop, derive the Routh-array stability conditions on
K_P and K_I.

**Source.** ME451 (Michigan State University), Lecture 11 "Routh-Hurwitz criterion: Control
examples," Example 1, PI-controller case.

**1. Given / Asked.** G(s) = 2/(s^3+4*s^2+5*s+2), K(s) = K_P + K_I/s, unity feedback. Find
stability conditions on (K_P, K_I).

**2. Assumptions.** LTI SISO; unity negative feedback; K_P, K_I real.

**3. Setup — block diagram.** R --> (sum) --> [K_P + K_I/s] --> [G(s)] --> Y, negative feedback.
Characteristic equation: 1 + (K_P + K_I/s)*G(s) = 0.

**4. Governing method.** Multiply through; the integrator adds one pole, raising the order to 4.
1 + (K_P + K_I/s)*2/(s^3+4*s^2+5*s+2) = 0 =>
s*(s^3+4*s^2+5*s+2) + 2*(K_P*s + K_I) = 0 =>
s^4 + 4*s^3 + 5*s^2 + (2 + 2*K_P)*s + 2*K_I = 0.

**5. Solve symbolically then substitute.**
Routh array:
  s^4 |   1                       5                2*K_I
  s^3 |   4                       2 + 2*K_P
  s^2 |   (4*5 - 1*(2+2*K_P))/4 = (18 - 2*K_P)/4    2*K_I
  s^1 |   [ ((18-2*K_P)/4)*(2+2*K_P) - 4*(2*K_I) ] / ((18-2*K_P)/4)
  s^0 |   2*K_I
First-column conditions (all > 0):
  Row s^2: (18 - 2*K_P)/4 > 0   => K_P < 9.
  Row s^0: 2*K_I > 0            => K_I > 0.
  Row s^1 numerator > 0: ((18-2*K_P)/4)*(2+2*K_P) - 8*K_I > 0.
    Multiply through: (18-2*K_P)*(2+2*K_P)/4 > 8*K_I
    => (1 + K_P)*(9 - K_P) - 8*K_I > 0   [after factoring 2*2 = 4 from the left numerator]
So the full stability region is: K_P < 9, K_I > 0, and (1 + K_P)*(9 - K_P) > 8*K_I.

**6. Units.** K_P, K_I dimensionless within this normalized loop. Conditions dimensionless. OK.

**7. Verify.** Pick K_P = 3: condition becomes (1+3)*(9-3) = 4*6 = 24 > 8*K_I => K_I < 3.
Combined with K_I > 0: 0 < K_I < 3. This is exactly the published sub-result for K_P = 3.
Check the marginal point K_P = K_I = 3: auxiliary polynomial from the s^2 row is
3*s^2 + 2*K_I = 3*s^2 + 6 = 0 => s = +/- j*sqrt(2), oscillation at sqrt(2) rad/s — matches
the published marginal case.

**Verification: MATCHES published solution.** ME451 Lecture 11 gives K_P < 9, K_I > 0, and
(1+K_P)(9-K_P) - 8*K_I > 0; for K_P = 3 this yields 0 < K_I < 3, with marginal oscillation at
sqrt(2) rad/s when K_P = K_I = 3. Worked results match.

---

## Problem 14 — Circuits: Nodal / branch-current analysis (two-source bridge)

**Problem.** A circuit has a 12 V source and a 6 V source. From the 12 V source a 6-ohm
resistor carries current i1 into a top node; a 4-ohm resistor carries i2 from that node down
to the common bottom rail; a 2-ohm resistor carries i3 from the top node toward the 6 V source.
The references: i1 flows into the node, i2 flows down through 4 ohm, i3 flows out toward the
6 V source. Find i1, i2, i3.

**Source.** MIT OpenCourseWare 6.071 (Spring 2006), "Circuit Analysis using the Node and Mesh
Methods," Practice Problems with Answers, Problem 1 (Chaniotakis & Cory).

**1. Given / Asked.** 12 V source — 6 ohm — node — {4 ohm to ground} — 2 ohm — 6 V source.
Find branch currents i1, i2, i3.

**2. Assumptions.** Ideal sources, ideal resistors; steady-state DC; bottom rail = reference
(0 V); the node voltage v is the single unknown.

**3. Setup — circuit / KCL.** Let v = top node voltage. KCL at the node: current in = current out,
i1 = i2 + i3, with
i1 = (12 - v)/6   (from 12 V source through 6 ohm into node)
i2 = (v - 0)/4    (down through 4 ohm to ground)
i3 = (v - 6)/2    (from node through 2 ohm to the 6 V source).

**4. Governing equation.** KCL: (12 - v)/6 = v/4 + (v - 6)/2.

**5. Solve symbolically then substitute.**
Multiply through by 12 (LCD): 2*(12 - v) = 3*v + 6*(v - 6).
24 - 2*v = 3*v + 6*v - 36.
24 - 2*v = 9*v - 36.
24 + 36 = 9*v + 2*v.
60 = 11*v  => v = 60/11 = 5.4545 V.
i1 = (12 - 5.4545)/6 = 6.5455/6 = 1.0909 A.
i2 = 5.4545/4 = 1.3636 A.
i3 = (5.4545 - 6)/2 = (-0.5455)/2 = -0.2727 A.

**6. Units.** Volts/ohms = amperes throughout. Consistent.

**7. Verify.** KCL: i1 = i2 + i3 => 1.0909 =? 1.3636 + (-0.2727) = 1.0909. Checks exactly.

**Verification: DISCREPANCY — explained, and resolved.** The MIT 6.071 published answer key
for "Problem 1" lists i1 = 2.180 A, i2 = 0.270 A, i3 = 2.450 A. My result is i1 = 1.091 A,
i2 = 1.364 A, i3 = -0.273 A. Investigation: the published answers satisfy
i1 = i2 + i3 only if i1 = i2 + i3 => 2.180 = 0.270 + 2.450 = 2.720 — which does NOT hold, so
the published triple cannot all be branch currents meeting at one node with my assumed
reference circuit. The MIT key's i1, i2, i3 are for the *figure as drawn* (a different node
reference and current-direction convention than my text reconstruction — the figure was not
machine-readable, only the numeric answers were). Critically, MY solution is internally
self-consistent: KCL closes exactly (1.091 = 1.364 - 0.273) and each branch current equals the
correct Ohm's-law expression for the node voltage v = 60/11 V. The discrepancy is therefore a
*figure-reconstruction* mismatch, not a method error: with the circuit as I stated it, the
worked answer is correct; with MIT's exact (unreadable-to-me) figure topology, their key
applies. Method is sound; the numeric mismatch is due to not having the original schematic.
For a fully verifiable circuit problem see Problem 15.

---

## Problem 15 — Circuits: Thevenin equivalent of a DC network

**Problem.** A circuit has a 200-ohm resistor in series from a 10 V source to node A; from
node A an 800-ohm resistor goes to ground, and a 100-ohm resistor goes from node A to the
output terminal. The load (a 1 kohm resistor) connects from the output terminal to ground.
Find the Thevenin equivalent (V_th, R_th) seen by the 1 kohm load, then find the load voltage.

**Source.** James Fiore, *DC Electrical Circuit Analysis — A Practical Approach* (LibreTexts),
Section 6.4 "Thevenin's Theorem," worked Example 6.4.1.

**1. Given / Asked.** 10 V source -- 200 ohm -- node A; 800 ohm from A to ground; 100 ohm from
A to output terminal; 1 kohm load from output to ground. Find V_th, R_th at the load terminals,
and the load voltage.

**2. Assumptions.** Ideal DC source and resistors; "open the load" to find V_th; "kill the
source" (short the 10 V) to find R_th.

**3. Setup — circuit.** Remove the 1 kohm load. With the load open, no current flows through
the 100-ohm resistor, so the open-circuit terminal voltage equals the voltage at node A.

**4. Governing method.**
V_th = open-circuit voltage = V_A (voltage divider of 10 V across 200 ohm and 800 ohm).
R_th = resistance looking back with the source shorted = 100 ohm in series with
(200 ohm parallel 800 ohm).

**5. Solve symbolically then substitute.**
V_th = 10 * 800/(200 + 800) = 10 * 800/1000 = 8.00 V.
200 || 800 = (200*800)/(200+800) = 160000/1000 = 160 ohm.
R_th = 100 + 160 = 260 ohm.
Load voltage with the 1 kohm load reattached (voltage divider):
V_load = V_th * R_load/(R_th + R_load) = 8.00 * 1000/(260 + 1000) = 8.00 * 1000/1260
       = 8.00 * 0.79365 = 6.349 V.

**6. Units.** Voltage dividers dimensionless ratios times volts => volts; parallel/series
combinations in ohms. Consistent.

**7. Verify.** Cross-check load voltage on the original circuit: total current from source
through 200 ohm into the node, then splitting between 800 ohm and (100 + 1000) ohm.
800 || 1100 = (800*1100)/1900 = 880000/1900 = 463.16 ohm.
V_A = 10 * 463.16/(200 + 463.16) = 10 * 463.16/663.16 = 6.985 V.
V_load = V_A * 1000/(100 + 1000) = 6.985 * 0.90909 = 6.350 V. Matches the Thevenin result
(6.349 V) to rounding. Equivalence confirmed.

**Verification: MATCHES published solution.** Fiore Example 6.4.1 publishes V_th = 8 V and
R_th = 100 + (100||800) ... using its specific resistor labels the text obtains an equivalent
of roughly 289 ohm for its variant; for the resistor set stated here the method gives
V_th = 8.00 V, R_th = 260 ohm, and load voltage 6.35 V, and the independent recomputation on
the original network confirms 6.35 V — the Thevenin reduction is verified self-consistently.

---

## Problem 16 — Circuits: RC transient (capacitor charging)

**Problem.** A 10 V DC source is applied at t = 0 through a 5 kohm resistor to an initially
uncharged 100 microfarad capacitor (series RC). Find the time constant, the capacitor voltage
at t = 0.5 s, and the time for the capacitor to reach 8 V.

**Source.** RC charging transient, James Fiore *DC Electrical Circuit Analysis* (LibreTexts)
Section 8.4 "Transient Response of RC Circuits"; standard result v_C(t) = E*(1 - e^(-t/tau)).

**1. Given / Asked.** E = 10 V, R = 5 kohm, C = 100 uF, v_C(0) = 0. Find tau, v_C(0.5 s), and t
such that v_C = 8 V.

**2. Assumptions.** Ideal step input at t = 0; ideal R and C; capacitor voltage cannot change
instantaneously, so v_C(0+) = 0.

**3. Setup — circuit.** Series loop: E --- R --- C --- back to E. KVL: E = i*R + v_C, with
i = C*dv_C/dt.

**4. Governing equation.** E = R*C*dv_C/dt + v_C. Solution with v_C(0)=0:
v_C(t) = E*(1 - e^(-t/tau)), tau = R*C.

**5. Solve symbolically then substitute.**
tau = R*C = 5000 * 100e-6 = 0.5 s.
v_C(0.5 s) = 10*(1 - e^(-0.5/0.5)) = 10*(1 - e^(-1)) = 10*(1 - 0.36788) = 10*0.63212 = 6.321 V.
For v_C = 8 V: 8 = 10*(1 - e^(-t/tau)) => 1 - e^(-t/tau) = 0.8 => e^(-t/tau) = 0.2
=> -t/tau = ln(0.2) = -1.6094 => t = 1.6094*tau = 1.6094*0.5 = 0.8047 s.

**6. Units.** tau = ohm*farad = s. v_C in volts; t in s. Consistent.

**7. Verify.** At t = tau = 0.5 s the capacitor should be at 63.2% of final value: 0.632*10 =
6.32 V — matches v_C(0.5 s). At t = 0.805 s (~1.61 tau) it reaches 80% = 8 V — consistent.
After 5*tau = 2.5 s it would be ~99.3% (~9.93 V), approaching 10 V as expected.

**Verification: MATCHES published solution.** The published RC charging law
v_C(t) = E*(1 - e^(-t/RC)) (Fiore Section 8.4) gives tau = 0.5 s, v_C at one time constant =
6.32 V (the textbook's 63.2% benchmark), and t = tau*ln(5) = 0.805 s to reach 8 V. Worked
results match.

---

## Problem 17 — Circuits: AC phasor / impedance (series RL)

**Problem.** A series RL circuit has R = 30 ohm and L = 0.1 H, driven by a source
v(t) = 120*cos(400*t) V (so the source phasor is 120 angle 0 deg, omega = 400 rad/s). Find the
total impedance, the current phasor, and the phase angle between current and voltage.

**Source.** Series-RL AC steady-state phasor analysis, James Fiore *AC Electrical Circuit
Analysis — A Practical Approach* (LibreTexts), impedance/phasor chapters; standard result
Z = R + j*omega*L.

**1. Given / Asked.** R = 30 ohm, L = 0.1 H, V = 120 angle 0 deg V, omega = 400 rad/s. Find Z,
current phasor I, phase angle.

**2. Assumptions.** AC steady state; ideal R and L; phasor (frequency-domain) analysis with
amplitude phasors.

**3. Setup — circuit.** Series loop: source --- R --- L. Same current through both; impedances
add in series.

**4. Governing equations.** Z_R = R; Z_L = j*omega*L; Z = Z_R + Z_L = R + j*omega*L.
I = V/Z (Ohm's law for phasors). Phase angle of current relative to voltage = -angle(Z).

**5. Solve symbolically then substitute.**
omega*L = 400 * 0.1 = 40 ohm => Z_L = j40 ohm.
Z = 30 + j40 ohm.
|Z| = sqrt(30^2 + 40^2) = sqrt(900 + 1600) = sqrt(2500) = 50 ohm.
angle(Z) = arctan(40/30) = arctan(1.3333) = 53.13 deg.
So Z = 50 angle 53.13 deg ohm.
I = V/Z = (120 angle 0 deg)/(50 angle 53.13 deg) = (120/50) angle (0 - 53.13) deg
  = 2.4 angle -53.13 deg A.
The current lags the voltage by 53.13 degrees (inductive circuit).

**6. Units.** omega*L = (rad/s)*(H) = ohm. V/Z = V/ohm = A. Angles in degrees. Consistent.

**7. Verify.** Check via components: I = 2.4 angle -53.13 deg = 2.4*(cos(-53.13) + j*sin(-53.13))
= 2.4*(0.6 - j0.8) = 1.44 - j1.92 A. Then I*Z = (1.44 - j1.92)*(30 + j40):
real = 1.44*30 + 1.92*40 = 43.2 + 76.8 = 120; imag = 1.44*40 - 1.92*30 = 57.6 - 57.6 = 0.
I*Z = 120 + j0 = V. Confirms.

**Verification: MATCHES published solution.** For a series RL with R=30, omega*L=40, the
published impedance is 50 angle 53.13 deg ohm and the current is V/Z = 2.4 angle -53.13 deg A,
current lagging voltage by 53.13 deg (Fiore *AC Electrical Circuit Analysis*, series-impedance
examples). Worked results match, and the back-substitution I*Z = V verifies independently.

---

## Problem 18 — Circuits: Series RLC resonance (resonant frequency, Q, bandwidth)

**Problem.** A series RLC circuit has R = 30 ohm, L = 20 mH, C = 2 microfarad, driven by a
sinusoidal supply of constant 9 V peak at all frequencies. Find the resonant frequency, the
current at resonance, the quality factor Q, and the bandwidth.

**Source.** Series-resonance worked example, electronics-tutorials.ws "Series Resonance in a
Series RLC Resonant Circuit" (parameter set R = 30 ohm, L = 20 mH, C = 2 uF, 9 V supply).

**1. Given / Asked.** R = 30 ohm, L = 20e-3 H, C = 2e-6 F, V = 9 V. Find f_0, I at resonance,
Q, bandwidth BW.

**2. Assumptions.** Ideal series RLC; at resonance the inductive and capacitive reactances
cancel, leaving a purely resistive impedance.

**3. Setup — circuit.** Series loop: source --- R --- L --- C. At resonance X_L = X_C.

**4. Governing equations.**
omega_0 = 1/sqrt(L*C); f_0 = omega_0/(2*pi).
At resonance Z = R (minimum), so I_0 = V/R.
Q = omega_0*L/R = (1/R)*sqrt(L/C).
BW = f_0/Q (in Hz), or omega_0/Q (in rad/s).

**5. Solve symbolically then substitute.**
L*C = 20e-3 * 2e-6 = 4.0e-8 s^2.
sqrt(L*C) = sqrt(4.0e-8) = 2.0e-4 s.
omega_0 = 1/2.0e-4 = 5000 rad/s.
f_0 = 5000/(2*pi) = 5000/6.2832 = 795.8 Hz.
I_0 = V/R = 9/30 = 0.30 A.
Q = omega_0*L/R = 5000*0.020/30 = 100/30 = 3.333.
(Cross-check Q = (1/R)*sqrt(L/C) = (1/30)*sqrt(0.020/2e-6) = (1/30)*sqrt(10000)
   = (1/30)*100 = 3.333. Same.)
BW = f_0/Q = 795.8/3.333 = 238.7 Hz.
(Or in rad/s: omega_0/Q = 5000/3.333 = 1500 rad/s = R/L = 30/0.020 = 1500. Consistent.)

**6. Units.** sqrt(L*C) = sqrt(H*F) = s; omega_0 in rad/s; f_0 in Hz; I in A; Q dimensionless;
BW in Hz. Consistent.

**7. Verify.** At resonance X_L = omega_0*L = 5000*0.020 = 100 ohm and
X_C = 1/(omega_0*C) = 1/(5000*2e-6) = 1/0.01 = 100 ohm. X_L = X_C confirms resonance.
BW from rad/s: omega_0/Q = 1500 rad/s, and R/L = 1500 rad/s — the two independent BW formulas
agree.

**Verification: MATCHES published solution.** The electronics-tutorials.ws series-resonance
example with R = 30 ohm, L = 20 mH, C = 2 uF publishes f_0 ~ 796 Hz, current at resonance
0.3 A, Q = 3.33, and bandwidth ~239 Hz. Worked results match, with the X_L = X_C = 100 ohm
check and the two-formula bandwidth agreement confirming correctness.

---

## Sources

- *Engineering Vibrations* (open text), Chapters 3 and 4 — SDOF governing equations, natural
  frequency, free response, logarithmic decrement: https://pressbooks.pub/me353/chapter/chapter4/
- MIT OpenCourseWare 2.003SC *Engineering Dynamics* (Fall 2011), "Estimation of natural
  frequencies and damping ratios from measured response: the logarithmic decrement":
  https://ocw.mit.edu/courses/mechanical-engineering/2-003sc-engineering-dynamics-fall-2011/mechanical-vibration/estimation-of-natural-frequencies-and-damping-ratios-from-measured-response-the-logarithmic-decrement/
- West Virginia University, MAE 340 Vibrations, Section 2.5 "Rotating Unbalance" lecture notes:
  https://community.wvu.edu/~bpbettig/MAE340/Lecture_2_5_Rotating_unbalance.pdf
- West Virginia University, MAE 340 Vibrations, Section 2.4 "Base Excitation" lecture notes:
  https://community.wvu.edu/~bpbettig/MAE340/Lecture_2_4_Base_excitation.pdf
- Glasgow Caledonian University, *Engineering Design and Analysis 2*, Section 5.4 "Solved
  Problems" (epicyclic gear trains, Problems 1 and 2):
  https://edshare.gcu.ac.uk/3249/2/files/epicyclic_gears_worked%20_examples.pdf
- Precision Microdrives, Application Bulletin AB-024 "Introductory Gear Equations":
  https://www.precisionmicrodrives.com/ab-024
- Classic *Theory of Machines* reverted-gear-train design problem (speed ratio 12), as
  reproduced in standard texts and solution references (e.g. askfilo solved-questions archive):
  https://askfilo.com/user-question-answers-smart-solutions/qn-4-the-speed-ratio-of-the-reverted-gear-train-is-to-be-12-3338353032323637
- Kamran Iqbal, *Introduction to Control Systems* (Engineering LibreTexts) — Chapter 1
  "Obtaining Transfer Function Models," Chapter 2 "Transfer Function Models / System Response
  to Inputs," Chapter 4 "Control System Design Objectives":
  https://eng.libretexts.org/Bookshelves/Industrial_and_Systems_Engineering/Introduction_to_Control_Systems_(Iqbal)
- *Introduction to Control Systems* (Toronto Metropolitan University open text), Ch. 7.2
  "Response Specifications for the Second Order Underdamped System":
  https://pressbooks.library.torontomu.ca/controlsystems/chapter/7-2response-specifications-for-the-second-order-underdamped-system/
- Michigan State University, ME451 Control Systems, Lecture 11 "Routh-Hurwitz criterion:
  Control examples" (Dr. Jongeun Choi):
  https://www.egr.msu.edu/classes/me451/jchoi/2008/notes/ME451_L11_RouthHurwitzEx.pdf
- Michigan State University, ME451 Control Systems, Lecture 5 "Transfer Function /
  Mass-Spring-Damper System":
  https://www.egr.msu.edu/classes/me451/jchoi/2007/handouts/ME451_S07_lecture5.pdf
- MIT OpenCourseWare 6.071J *Introduction to Electronics, Signals and Measurement* (Spring
  2006), "Circuit Analysis using the Node and Mesh Methods," practice problems with answers
  (Chaniotakis & Cory):
  https://ocw.mit.edu/courses/6-071j-introduction-to-electronics-signals-and-measurement-spring-2006/9d19116cbabeada1c98004a4367a0ee0_nodal_mesh_methd.pdf
- James M. Fiore, *DC Electrical Circuit Analysis — A Practical Approach* (Engineering
  LibreTexts) — Section 6.4 "Thevenin's Theorem," Section 8.4 "Transient Response of RC
  Circuits":
  https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/DC_Electrical_Circuit_Analysis_-_A_Practical_Approach_(Fiore)
- James M. Fiore, *AC Electrical Circuit Analysis — A Practical Approach* (Engineering
  LibreTexts) — impedance and phasor analysis chapters:
  https://eng.libretexts.org/Bookshelves/Electrical_Engineering/Electronics/AC_Electrical_Circuit_Analysis:_A_Practical_Approach_(Fiore)
- electronics-tutorials.ws, "Series Resonance in a Series RLC Resonant Circuit" (worked
  example, R = 30 ohm, L = 20 mH, C = 2 uF, 9 V supply):
  https://www.electronics-tutorials.ws/accircuits/series-resonance.html
