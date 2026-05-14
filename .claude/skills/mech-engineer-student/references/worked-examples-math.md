# Worked Examples — Mathematics

Verified practice problems with solutions checked against published answer keys.

Each problem is worked using a 7-step rigor protocol: (1) restate given/asked, (2) state assumptions, (3) sketch/setup, (4) name the governing theorem or method, (5) solve symbolically then substitute, (6) carry units/notation, (7) verify. The final answer is then compared to the published solution.

---

## Problem 1 — Limits (indeterminate form 0/0)

**Problem statement:** Evaluate lim(y→7) [(y² − 4y − 21) / (3y² − 17y − 28)], if it exists.

**Source:** Paul's Online Math Notes — Calculus I, Computing Limits, Practice Problem 5. https://tutorial.math.lamar.edu/Solutions/CalcI/ComputingLimits/Prob5.aspx

**Solution:**

1. **Given/asked:** A rational function of y; asked for its limit as y → 7.
2. **Assumptions:** Polynomial numerator and denominator are continuous everywhere; the only obstacle is a possible shared zero at y = 7.
3. **Setup:** Test direct substitution. Numerator at y=7: 49 − 28 − 21 = 0. Denominator at y=7: 3(49) − 119 − 28 = 147 − 147 = 0. Form is 0/0 — indeterminate, so factor.
4. **Governing method:** Limit laws + factor-and-cancel. For rational functions giving 0/0, a common linear factor (y − 7) must divide both numerator and denominator; cancel it, then the limit of the reduced (continuous) expression equals its value at y = 7.
5. **Solve symbolically:**
   - Numerator: y² − 4y − 21 = (y − 7)(y + 3).
   - Denominator: 3y² − 17y − 28 = (3y + 4)(y − 7).
   - For y ≠ 7: (y − 7)(y + 3) / [(3y + 4)(y − 7)] = (y + 3)/(3y + 4).
   - lim(y→7) (y + 3)/(3y + 4) = (7 + 3)/(21 + 4) = 10/25 = 2/5.
6. **Notation:** Dimensionless ratio; answer is the exact rational 2/5.
7. **Verify:** Factorizations check: (y−7)(y+3) = y² − 4y − 21 ✓; (3y+4)(y−7) = 3y² − 17y − 28 ✓. Sanity: plug y = 7.001 → (10.001)/(25.003) ≈ 0.39999, consistent with 2/5 = 0.4.

**Verification: MATCHES published solution** (2/5).

---

## Problem 2 — Related Rates (conical tank)

**Problem statement:** A conical water tank is being filled at 12 m³/sec. The tank has a base radius of 26 m and a height of 8 m. Find the rate at which the water depth is changing when the radius of the water surface is 10 m.

**Source:** Paul's Online Math Notes — Calculus I, Related Rates, Practice Problem 10. https://tutorial.math.lamar.edu/Solutions/CalcI/RelatedRates/Prob10.aspx

**Solution:**

1. **Given/asked:** dV/dt = 12 m³/s. Tank cone: R = 26 m, H = 8 m. Find dh/dt when r = 10 m.
2. **Assumptions:** Water forms a cone similar to the tank (apex down); incompressible water; tank geometry fixed.
3. **Setup/sketch:** Cone of water with surface radius r and depth h. Similar triangles to the tank: r/h = R/H = 26/8 = 13/4, so r = (13/4)h.
4. **Governing method:** Implicit differentiation of the cone volume V = (1/3)πr²h with respect to time (related rates).
5. **Solve symbolically then substitute:**
   - Eliminate r: V = (1/3)π[(13/4)h]²h = (1/3)π(169/16)h³ = (169/48)π h³.
   - Differentiate: dV/dt = (169/48)π · 3h² · dh/dt = (169/16)π h² dh/dt.
   - At r = 10: h = (4/13)(10) = 40/13 m.
   - h² = 1600/169, so (169/16)π h² = (169/16)π · (1600/169) = 100π.
   - 12 = 100π · dh/dt → dh/dt = 12/(100π) = 3/(25π) m/s ≈ 0.0382 m/s.
6. **Units:** (m³/s) / (m²) = m/s ✓. dh/dt = 3/(25π) m/s.
7. **Verify:** Limiting-case sanity — depth rises slowly because the surface is wide (r = 10 m → cross-section ≈ π·100 ≈ 314 m²; 12/314 ≈ 0.038 m/s) ✓. Positive rate, as expected when filling.

**Verification: MATCHES published solution** (dh/dt = 3/(25π) m/s ≈ 0.0382 m/s).

---

## Problem 3 — Optimization (open box from cardboard)

**Problem statement:** A piece of cardboard 50 cm by 20 cm has squares cut from each corner and the sides folded up to form an open box. Determine the height of the box that gives maximum volume.

**Source:** Paul's Online Math Notes — Calculus I, Optimization, Practice Problem 8. https://tutorial.math.lamar.edu/Solutions/CalcI/Optimization/Prob8.aspx

**Solution:**

1. **Given/asked:** Sheet 50 × 20 cm; cut corner squares of side h, fold up. Find h maximizing volume V.
2. **Assumptions:** Cuts are congruent squares; folds are exact right angles; material has zero thickness.
3. **Setup:** After cutting side-h squares, base dimensions are (50 − 2h) and (20 − 2h), box height h. Constraint domain: 0 ≤ h ≤ 10 (the box collapses when 2h = 20).
4. **Governing method:** Closed-interval (extreme value theorem) optimization — find critical points of V(h), compare with endpoints.
5. **Solve symbolically then substitute:**
   - V(h) = h(50 − 2h)(20 − 2h) = h(1000 − 140h + 4h²) = 4h³ − 140h² + 1000h.
   - V'(h) = 12h² − 280h + 1000. Set V' = 0: divide by 4 → 3h² − 70h + 250 = 0.
   - h = [70 ± √(4900 − 3000)] / 6 = [70 ± √1900]/6 = [70 ± 43.589]/6.
   - h ≈ 18.93 (rejected, outside [0,10]) or h ≈ 4.4018 cm.
   - Endpoints: V(0) = 0, V(10) = 0. Critical point: V(4.4018) ≈ 4(85.30) − 140(19.38) + 1000(4.4018) ≈ 2030.34 cm³.
6. **Units:** h in cm; V in cm³. Maximum at h ≈ 4.4018 cm.
7. **Verify:** V' changes sign + → − across h ≈ 4.40 (V'(4) = 192 − 1120 + 1000 = 72 > 0; V'(5) = 300 − 1400 + 1000 = −100 < 0) → local max ✓. It beats both zero-volume endpoints ✓.

**Verification: MATCHES published solution** (h ≈ 4.4018 cm, V_max ≈ 2030.34 cm³).

---

## Problem 4 — Integration by Parts (polynomial × trig)

**Problem statement:** Evaluate ∫ (3t + t²) sin(2t) dt.

**Source:** Paul's Online Math Notes — Calculus II, Integration by Parts, Practice Problem 3. https://tutorial.math.lamar.edu/Solutions/CalcII/IntegrationByParts/Prob3.aspx

**Solution:**

1. **Given/asked:** Indefinite integral of a degree-2 polynomial times sin(2t).
2. **Assumptions:** Standard antiderivative; constant of integration included.
3. **Setup:** Polynomial × trig → integration by parts, letting u be the polynomial so each pass lowers its degree. Two passes needed (degree 2 → 1 → 0).
4. **Governing method:** Integration by parts, ∫ u dv = uv − ∫ v du.
5. **Solve symbolically:**
   - **Pass 1:** u = 3t + t², dv = sin(2t) dt → du = (3 + 2t) dt, v = −(1/2)cos(2t).
     ∫ = −(1/2)(3t + t²)cos(2t) + (1/2)∫ (3 + 2t)cos(2t) dt.
   - **Pass 2:** for ∫ (3 + 2t)cos(2t) dt, u = 3 + 2t, dv = cos(2t) dt → du = 2 dt, v = (1/2)sin(2t).
     ∫ (3 + 2t)cos(2t) dt = (1/2)(3 + 2t)sin(2t) − ∫ sin(2t) dt = (1/2)(3 + 2t)sin(2t) + (1/2)cos(2t).
   - Combine: ∫ = −(1/2)(3t + t²)cos(2t) + (1/2)[(1/2)(3 + 2t)sin(2t) + (1/2)cos(2t)]
     = −(1/2)(3t + t²)cos(2t) + (1/4)(3 + 2t)sin(2t) + (1/4)cos(2t) + c.
6. **Notation:** Result is a function of t plus arbitrary constant c.
7. **Verify (differentiate the answer):**
   - d/dt[−(1/2)(3t+t²)cos2t] = −(1/2)(3+2t)cos2t + (3t+t²)sin2t.
   - d/dt[(1/4)(3+2t)sin2t] = (1/2)sin2t + (1/2)(3+2t)cos2t.
   - d/dt[(1/4)cos2t] = −(1/2)sin2t.
   - Sum: the ±(1/2)(3+2t)cos2t cancel, the ±(1/2)sin2t cancel, leaving (3t + t²)sin(2t) ✓.

**Verification: MATCHES published solution** (−½(3t + t²)cos(2t) + ¼(3 + 2t)sin(2t) + ¼cos(2t) + c).

---

## Problem 5 — Improper Integral (convergence test)

**Problem statement:** Determine whether ∫_{−∞}^{0} (1 + 2x)e^{−x} dx converges or diverges; if it converges, find its value.

**Source:** Paul's Online Math Notes — Calculus II, Improper Integrals, Practice Problem 2. https://tutorial.math.lamar.edu/Solutions/CalcII/ImproperIntegrals/Prob2.aspx

**Solution:**

1. **Given/asked:** An integral with an infinite lower limit; decide convergence and evaluate if finite.
2. **Assumptions:** Integrand (1 + 2x)e^{−x} is continuous on (−∞, 0]; only the −∞ limit is improper.
3. **Setup:** Rewrite as a limit: ∫_{−∞}^{0} = lim(t→−∞) ∫_{t}^{0} (1 + 2x)e^{−x} dx.
4. **Governing method:** Definition of improper integral as a limit; antiderivative via integration by parts.
5. **Solve symbolically:**
   - Antiderivative: ∫ (1 + 2x)e^{−x} dx. Let u = 1 + 2x, dv = e^{−x}dx → du = 2dx, v = −e^{−x}.
     = −(1 + 2x)e^{−x} + ∫ 2e^{−x} dx = −(1 + 2x)e^{−x} − 2e^{−x} = −(3 + 2x)e^{−x}.
   - Evaluate t to 0: [−(3 + 2x)e^{−x}]_{t}^{0} = −(3)e^{0} − [−(3 + 2t)e^{−t}] = −3 + (3 + 2t)e^{−t}.
   - Take the limit: lim(t→−∞) [(3 + 2t)e^{−t} − 3]. As t → −∞, (3 + 2t) → −∞ and e^{−t} → +∞, so the product → −∞.
6. **Notation:** The limit is −∞, not a finite number.
7. **Verify:** Sign/growth check — for very negative x, e^{−x} blows up exponentially while (1 + 2x) only grows linearly negative, so the integrand is large-negative and its integral cannot settle to a finite value ✓.

**Verification: MATCHES published solution** (the integral DIVERGES).

---

## Problem 6 — Series Convergence (Ratio Test)

**Problem statement:** Determine whether the series Σ_{n=1}^{∞} 3^{1−2n} / (n² + 1) converges or diverges.

**Source:** Paul's Online Math Notes — Calculus II, Ratio Test, Practice Problem 1. https://tutorial.math.lamar.edu/Solutions/CalcII/RatioTest/Prob1.aspx

**Solution:**

1. **Given/asked:** A positive-term series; decide convergence/divergence.
2. **Assumptions:** All terms a_n = 3^{1−2n}/(n²+1) > 0, so |a_{n+1}/a_n| = a_{n+1}/a_n.
3. **Setup:** Form factor 3^{1−2n} suggests a geometric-type decay; the Ratio Test is well suited.
4. **Governing method:** Ratio Test — L = lim(n→∞) |a_{n+1}/a_n|; L < 1 ⇒ converges, L > 1 ⇒ diverges, L = 1 ⇒ inconclusive.
5. **Solve symbolically:**
   - a_{n+1} = 3^{1−2(n+1)} / ((n+1)² + 1) = 3^{−1−2n} / (n² + 2n + 2).
   - a_{n+1}/a_n = [3^{−1−2n} / (n² + 2n + 2)] · [(n² + 1) / 3^{1−2n}]
     = 3^{(−1−2n) − (1−2n)} · (n² + 1)/(n² + 2n + 2) = 3^{−2} · (n² + 1)/(n² + 2n + 2).
   - L = lim(n→∞) (1/9) · (n² + 1)/(n² + 2n + 2) = (1/9)(1) = 1/9.
6. **Notation:** L = 1/9, dimensionless.
7. **Verify:** 1/9 < 1 ⇒ series converges (absolutely). Cross-check: 3^{1−2n} = 3·9^{−n}, so a_n ≤ 3·9^{−n}, a convergent geometric series — comparison confirms convergence ✓.

**Verification: MATCHES published solution** (L = 1/9 < 1, series CONVERGES).

---

## Problem 7 — Multivariable: Directional Derivative

**Problem statement:** Determine D_u f(3, −1, 0) for f(x,y,z) = 4x − y² e^{3xz} in the direction of v = ⟨−1, 4, 2⟩.

**Source:** Paul's Online Math Notes — Calculus III, Directional Derivatives, Practice Problem 5. https://tutorial.math.lamar.edu/Solutions/CalcIII/DirectionalDeriv/Prob5.aspx

**Solution:**

1. **Given/asked:** Scalar field f, evaluation point (3, −1, 0), direction v. Find the directional derivative.
2. **Assumptions:** f is differentiable (composition of polynomial and exponential), so D_u f = ∇f · u with u the unit vector along v.
3. **Setup:** Compute ∇f, evaluate at the point, normalize v, take the dot product.
4. **Governing method:** D_u f = ∇f · u, where u = v/‖v‖.
5. **Solve symbolically then substitute:**
   - f_x = 4 − y²·(3z)e^{3xz} = 4 − 3y²z e^{3xz}.
   - f_y = −2y e^{3xz}.
   - f_z = −y²·(3x)e^{3xz} = −3xy² e^{3xz}.
   - At (3, −1, 0): e^{3·3·0} = e^0 = 1.
     - f_x = 4 − 3(1)(0)(1) = 4.
     - f_y = −2(−1)(1) = 2.
     - f_z = −3(3)(1)(1) = −9.
   - ∇f(3,−1,0) = ⟨4, 2, −9⟩.
   - ‖v‖ = √((−1)² + 4² + 2²) = √(1 + 16 + 4) = √21. u = (1/√21)⟨−1, 4, 2⟩.
   - D_u f = ⟨4, 2, −9⟩ · (1/√21)⟨−1, 4, 2⟩ = (1/√21)(−4 + 8 − 18) = −14/√21.
6. **Notation:** D_u f = −14/√21 (≈ −3.055), a rate of change per unit length along u.
7. **Verify:** |D_u f| = 14/√21 ≈ 3.06 ≤ ‖∇f‖ = √(16+4+81) = √101 ≈ 10.05 — directional derivative cannot exceed gradient magnitude ✓. Negative sign means f decreases in direction v at that point.

**Verification: MATCHES published solution** (D_u f = −14/√21).

---

## Problem 8 — Multivariable: Lagrange Multipliers

**Problem statement:** Find the maximum and minimum values of f(x,y) = 81x² + y² subject to the constraint 4x² + y² = 9.

**Source:** Paul's Online Math Notes — Calculus III, Lagrange Multipliers, Practice Problem 1. https://tutorial.math.lamar.edu/Solutions/CalcIII/LagrangeMultipliers/Prob1.aspx

**Solution:**

1. **Given/asked:** Extremize f on the ellipse g(x,y) = 4x² + y² = 9.
2. **Assumptions:** Constraint set is a closed, bounded ellipse → f (continuous) attains a global max and min on it (extreme value theorem).
3. **Setup:** ∇f = λ∇g plus the constraint. ∇f = ⟨162x, 2y⟩, ∇g = ⟨8x, 2y⟩.
4. **Governing method:** Method of Lagrange multipliers.
5. **Solve symbolically:**
   - Equations: (i) 162x = 8λx; (ii) 2y = 2λy; (iii) 4x² + y² = 9.
   - From (ii): 2y(1 − λ) = 0 ⇒ y = 0 or λ = 1.
   - **Case y = 0:** (iii) gives 4x² = 9 ⇒ x = ±3/2. Points: (±3/2, 0). (Eqn (i): 162(±3/2) = 8λ(±3/2) ⇒ λ = 162/8 = 20.25, consistent.)
   - **Case λ = 1:** (i) gives 162x = 8x ⇒ 154x = 0 ⇒ x = 0. (iii): y² = 9 ⇒ y = ±3. Points: (0, ±3).
   - Evaluate f:
     - f(±3/2, 0) = 81(9/4) + 0 = 729/4 = 182.25.
     - f(0, ±3) = 0 + 9 = 9.
6. **Notation:** Dimensionless function values.
7. **Verify:** Both candidate points satisfy 4x² + y² = 9: 4(9/4)+0 = 9 ✓ and 0 + 9 = 9 ✓. Max 729/4 > min 9, and f ≥ 0 everywhere so min must be positive ✓.

**Verification: MATCHES published solution** (maximum = 729/4 at (±3/2, 0); minimum = 9 at (0, ±3)).

---

## Problem 9 — Multivariable: Double Integral over a General Region

**Problem statement:** Evaluate ∬_D (42y² − 12x) dA where D = {(x,y) | 0 ≤ x ≤ 4, (x − 2)² ≤ y ≤ 6}.

**Source:** Paul's Online Math Notes — Calculus III, Double Integrals over General Regions, Practice Problem 1. https://tutorial.math.lamar.edu/Solutions/CalcIII/DIGeneralRegion/Prob1.aspx

**Solution:**

1. **Given/asked:** A double integral over a region bounded below by the parabola y = (x−2)² and above by y = 6, for x ∈ [0,4].
2. **Assumptions:** Integrand is a polynomial — continuous, so the iterated integral equals the double integral (Fubini).
3. **Setup/sketch:** Vertical strips: for each x in [0,4], y runs from (x−2)² up to 6. Integrate y first, then x.
4. **Governing method:** Fubini's theorem — iterated integration over a Type I region.
5. **Solve symbolically then substitute:**
   - Inner: ∫_{(x−2)²}^{6} (42y² − 12x) dy = [14y³ − 12xy]_{(x−2)²}^{6}
     = (14·216 − 72x) − (14(x−2)⁶ − 12x(x−2)²)
     = 3024 − 72x − 14(x−2)⁶ + 12x(x−2)².
   - Expand 12x(x−2)² = 12x(x² − 4x + 4) = 12x³ − 48x² + 48x.
   - Outer: ∫_0^4 [3024 − 72x − 14(x−2)⁶ + 12x³ − 48x² + 48x] dx
     = ∫_0^4 [3024 − 24x + 12x³ − 48x² − 14(x−2)⁶] dx.
   - Term by term over [0,4]:
     - ∫ 3024 dx = 3024·4 = 12096.
     - ∫ −24x dx = −12x² |₀⁴ = −192.
     - ∫ 12x³ dx = 3x⁴ |₀⁴ = 3·256 = 768.
     - ∫ −48x² dx = −16x³ |₀⁴ = −16·64 = −1024.
     - ∫ −14(x−2)⁶ dx = −2(x−2)⁷ |₀⁴ = −2[(2)⁷ − (−2)⁷] = −2[128 − (−128)] = −2(256) = −512.
   - Sum: 12096 − 192 + 768 − 1024 − 512 = 11136.
6. **Notation:** Pure number (area integral of a scalar field).
7. **Verify:** Recheck the (x−2)⁶ antiderivative: d/dx[−2(x−2)⁷] = −14(x−2)⁶ ✓. Arithmetic: 12096 − 192 = 11904; +768 = 12672; −1024 = 11648; −512 = 11136 ✓.

**Verification: MATCHES published solution** (11136).

---

## Problem 10 — Numerical Methods: Newton's Method

**Problem statement:** Use Newton's Method to find the root of 2x² + 5 = e^x, accurate to six decimal places, in the interval [3, 4].

**Source:** Paul's Online Math Notes — Calculus I, Newton's Method, Practice Problem 4. https://tutorial.math.lamar.edu/Solutions/CalcI/NewtonsMethod/Prob4.aspx

**Solution:**

1. **Given/asked:** Solve 2x² + 5 = e^x on [3,4] to 6 decimals via Newton iteration.
2. **Assumptions:** Root reformulated as f(x) = 0; f is smooth (C^∞), f' ≠ 0 near the root, so Newton converges quadratically from a good start.
3. **Setup:** f(x) = 2x² + 5 − e^x. f(3) = 18 + 5 − e³ ≈ 23 − 20.0855 = 2.9145 > 0; f(4) = 32 + 5 − e⁴ ≈ 37 − 54.598 = −17.598 < 0 → sign change ⇒ root in (3,4). Take x₀ = 3.5.
4. **Governing method:** Newton's Method: x_{n+1} = x_n − f(x_n)/f'(x_n), with f'(x) = 4x − e^x.
5. **Iterate:**
   - x₀ = 3.5: f(3.5) = 2(12.25) + 5 − e^{3.5} = 29.5 − 33.1155 = −3.6155; f'(3.5) = 14 − 33.1155 = −19.1155.
     x₁ = 3.5 − (−3.6155)/(−19.1155) = 3.5 − 0.18914 = 3.310862334.
   - x₂ = 3.276614422.
   - x₃ = 3.275601951.
   - x₄ = 3.275601089.
   - x₃ and x₄ agree to 6 decimal places (3.275601) ⇒ stop.
6. **Notation:** Root x ≈ 3.275601089 (dimensionless).
7. **Verify:** Published note states the true root is 3.27560108884732 — x₄ matches to all shown digits ✓. Also x₄ ∈ [3,4] as required ✓. Quadratic convergence is visible: the error roughly squares each step.

**Verification: MATCHES published solution** (x ≈ 3.275601089).

---

## Problem 11 — First-Order Linear ODE (integrating factor)

**Problem statement:** Solve the differential equation dv/dt = 9.8 − 0.196v (a falling-body model with linear drag).

**Source:** Paul's Online Math Notes — Differential Equations, Linear Differential Equations, Example 1. https://tutorial.math.lamar.edu/classes/de/linear.aspx

**Solution:**

1. **Given/asked:** First-order ODE for velocity v(t); find the general solution.
2. **Assumptions:** Constant coefficients; v(t) differentiable; the model is linear in v.
3. **Setup:** Write in standard linear form v' + p(t)v = g(t): dv/dt + 0.196v = 9.8, so p(t) = 0.196, g(t) = 9.8.
4. **Governing method:** Integrating-factor method for first-order linear ODEs: μ(t) = e^{∫p dt}.
5. **Solve symbolically:**
   - μ(t) = e^{∫0.196 dt} = e^{0.196t}.
   - Multiply through: e^{0.196t} v' + 0.196 e^{0.196t} v = 9.8 e^{0.196t}.
   - Left side is (e^{0.196t} v)' (product rule): (e^{0.196t} v)' = 9.8 e^{0.196t}.
   - Integrate both sides: e^{0.196t} v = 9.8 · (1/0.196) e^{0.196t} + c = 50 e^{0.196t} + c.
   - Solve for v: v(t) = 50 + c e^{−0.196t}.
6. **Units:** v in m/s (terminal velocity term 9.8/0.196 = 50 m/s); c set by an initial condition.
7. **Verify (substitute back):** v' = −0.196c e^{−0.196t}. RHS: 9.8 − 0.196v = 9.8 − 0.196(50 + c e^{−0.196t}) = 9.8 − 9.8 − 0.196c e^{−0.196t} = −0.196c e^{−0.196t} = v' ✓. Limiting case: as t → ∞, v → 50 m/s (terminal velocity), physically correct ✓.

**Verification: MATCHES published solution** (v(t) = 50 + c e^{−0.196t}).

---

## Problem 12 — Second-Order Linear ODE: Laplace Transform IVP

**Problem statement:** Solve the initial value problem y″ − 6y′ + 5y = 3e^{2t}, y(0) = 2, y′(0) = 3, using Laplace transforms.

**Source:** LibreTexts — Differential Equations, "Solution of Initial Value Problems," Example 8.3.2 (Trench, *Elementary Differential Equations with Boundary Value Problems*). https://math.libretexts.org/Courses/Monroe_Community_College/MTH_225_Differential_Equations/08:_Laplace_Transforms/8.03:_Solution_of_Initial_Value_Problems

**Solution:**

1. **Given/asked:** Nonhomogeneous constant-coefficient 2nd-order IVP; find y(t).
2. **Assumptions:** y and y′ exist and are of exponential order so Laplace transforms apply; L{y} = Y(s).
3. **Setup:** Use L{y′} = sY − y(0), L{y″} = s²Y − s y(0) − y′(0), L{e^{2t}} = 1/(s−2).
4. **Governing method:** Laplace transform → algebraic equation in Y(s) → partial fractions → inverse transform.
5. **Solve symbolically then substitute:**
   - Transform: [s²Y − 2s − 3] − 6[sY − 2] + 5Y = 3/(s−2).
   - (s² − 6s + 5)Y − 2s − 3 + 12 = 3/(s−2) → (s−1)(s−5)Y + (9 − 2s) = 3/(s−2).
   - (s−1)(s−5)Y = 3/(s−2) + 2s − 9.
   - Y = 3/[(s−2)(s−1)(s−5)] + (2s − 9)/[(s−1)(s−5)].
   - Partial fractions (combining both pieces): Y(s) = −1/(s−2) + (1/2)·1/(s−5) + (5/2)·1/(s−1).
     (Check the −1/(s−2) coefficient: 3/[(s−2)(s−1)(s−5)] at s=2 → 3/[(1)(−3)] = −1 ✓.)
   - Inverse transform termwise: L^{−1}{1/(s−a)} = e^{at}.
   - y(t) = −e^{2t} + (1/2)e^{5t} + (5/2)e^{t}.
6. **Notation:** y(t) dimensionless; sum of exponentials.
7. **Verify (initial conditions):**
   - y(0) = −1 + 1/2 + 5/2 = 2 ✓.
   - y′(t) = −2e^{2t} + (5/2)e^{5t} + (5/2)e^{t}; y′(0) = −2 + 5/2 + 5/2 = 3 ✓.
   - Particular part: plug y_p = −e^{2t} into LHS: 4(−e^{2t}) − 6(−2e^{2t}) + 5(−e^{2t}) = (−4 + 12 − 5)e^{2t} = 3e^{2t} ✓.

**Verification: MATCHES published solution** (y = −e^{2t} + ½e^{5t} + (5/2)e^{t}).

---

## Problem 13 — Probability: Binomial Distribution

**Problem statement:** Suppose each student independently refuses a request with probability p = 0.35. If 8 students are asked, what is the probability that exactly 3 of them refuse?

**Source:** OpenIntro Statistics (Diez, Barr, Çetinkaya-Rundel), *Distributions of Random Variables*, Binomial Distribution, Example 3.2 (via LibreTexts mirror). https://stats.libretexts.org/Bookshelves/Introductory_Statistics/OpenIntro_Statistics_(Diez_et_al)./03:_Distributions_of_Random_Variables/3.04:_Binomial_Distribution_(Special_Topic)

**Solution:**

1. **Given/asked:** n = 8 independent trials, success ("refuse") probability p = 0.35, find P(exactly k = 3 successes).
2. **Assumptions:** (1) fixed n = 8, (2) two outcomes per trial, (3) independent trials, (4) constant p — the four binomial conditions hold.
3. **Setup:** X ~ Binomial(n = 8, p = 0.35); want P(X = 3).
4. **Governing method:** Binomial probability formula P(X = k) = C(n,k) p^k (1−p)^{n−k}, with C(n,k) = n!/[k!(n−k)!].
5. **Solve symbolically then substitute:**
   - C(8,3) = 8!/(3!·5!) = (8·7·6)/(3·2·1) = 336/6 = 56.
   - p^k = (0.35)³ = 0.042875.
   - (1−p)^{n−k} = (0.65)⁵ = 0.1160290625.
   - P(X = 3) = 56 × 0.042875 × 0.1160290625 ≈ 56 × 0.0049751 ≈ 0.2786.
6. **Notation:** Probability, dimensionless, ≈ 0.279 (about 28%).
7. **Verify:** Sanity — expected number of refusals is np = 8(0.35) = 2.8, so k = 3 is near the mode; a probability of ≈ 0.28 for the most-likely-ish value is reasonable ✓. Bounds 0 ≤ 0.279 ≤ 1 ✓. Published text rounds (0.35)³(0.65)⁵ ≈ 0.005 and reports 56 × 0.005 = 0.28.

**Verification: MATCHES published solution** (P ≈ 0.28; full precision ≈ 0.2786).

---

## Sources

- Paul's Online Math Notes (Paul Dawkins, hosted at Lamar University) — Calculus I, II, III and Differential Equations notes and practice problems:
  - Computing Limits, Practice Problem 5: https://tutorial.math.lamar.edu/Solutions/CalcI/ComputingLimits/Prob5.aspx
  - Related Rates, Practice Problem 10: https://tutorial.math.lamar.edu/Solutions/CalcI/RelatedRates/Prob10.aspx
  - Optimization, Practice Problem 8: https://tutorial.math.lamar.edu/Solutions/CalcI/Optimization/Prob8.aspx
  - Newton's Method, Practice Problem 4: https://tutorial.math.lamar.edu/Solutions/CalcI/NewtonsMethod/Prob4.aspx
  - Integration by Parts, Practice Problem 3: https://tutorial.math.lamar.edu/Solutions/CalcII/IntegrationByParts/Prob3.aspx
  - Improper Integrals, Practice Problem 2: https://tutorial.math.lamar.edu/Solutions/CalcII/ImproperIntegrals/Prob2.aspx
  - Ratio Test, Practice Problem 1: https://tutorial.math.lamar.edu/Solutions/CalcII/RatioTest/Prob1.aspx
  - Directional Derivatives, Practice Problem 5: https://tutorial.math.lamar.edu/Solutions/CalcIII/DirectionalDeriv/Prob5.aspx
  - Lagrange Multipliers, Practice Problem 1: https://tutorial.math.lamar.edu/Solutions/CalcIII/LagrangeMultipliers/Prob1.aspx
  - Double Integrals over General Regions, Practice Problem 1: https://tutorial.math.lamar.edu/Solutions/CalcIII/DIGeneralRegion/Prob1.aspx
  - Linear Differential Equations, Example 1: https://tutorial.math.lamar.edu/classes/de/linear.aspx
- LibreTexts Mathematics — Differential Equations, "Solution of Initial Value Problems," Example 8.3.2 (from W. F. Trench, *Elementary Differential Equations with Boundary Value Problems*): https://math.libretexts.org/Courses/Monroe_Community_College/MTH_225_Differential_Equations/08:_Laplace_Transforms/8.03:_Solution_of_Initial_Value_Problems
- OpenIntro Statistics (David Diez, Mine Çetinkaya-Rundel, Christopher Barr), *Distributions of Random Variables* — Binomial Distribution, Example 3.2, via LibreTexts Statistics mirror: https://stats.libretexts.org/Bookshelves/Introductory_Statistics/OpenIntro_Statistics_(Diez_et_al)./03:_Distributions_of_Random_Variables/3.04:_Binomial_Distribution_(Special_Topic)
- OpenStax *Introductory Statistics 2e* — Using the Normal Distribution (consulted for the normal-distribution method; not used as a numbered problem above): https://openstax.org/books/introductory-statistics-2e/pages/6-2-using-the-normal-distribution
