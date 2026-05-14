# ME Formula Reference

Core relations by domain. Always check assumptions before applying — these hold
only under their stated conditions.

## Statics
- Equilibrium: ΣFx = 0, ΣFy = 0, ΣFz = 0, ΣM = 0 (about any point)
- 2D rigid body: 3 independent equations. Truss joint: 2. Frame member: 3.
- Centroid: x̄ = Σ(x_i A_i) / ΣA_i
- Second moment of area: I = ∫y² dA; parallel axis: I = I_c + A·d²
- Friction (impending motion): F = μ_s·N; kinetic: F = μ_k·N
- Distributed load → equivalent point load at the centroid of the load area

## Dynamics
- Kinematics (constant a): v = v₀ + at, x = x₀ + v₀t + ½at², v² = v₀² + 2a·Δx
- Newton's 2nd: ΣF = ma; rotational: ΣM = Iα
- Work–energy: W_net = ΔKE = ½mv² − ½mv₀²
- Impulse–momentum: ∫F dt = Δ(mv)
- Rotational KE: ½Iω²; rolling without slip: v = rω
- Normal/tangential: a_n = v²/ρ, a_t = dv/dt

## Mechanics of Materials
- Normal stress: σ = P/A; normal strain: ε = δ/L
- Hooke's law: σ = Eε; shear: τ = Gγ; G = E / [2(1+ν)]
- Axial deformation: δ = PL/(AE)
- Torsion (circular shaft): τ = Tr/J, φ = TL/(JG); solid shaft J = πd⁴/32
- Bending stress: σ = Mc/I; transverse shear: τ = VQ/(It)
- Beam deflection: EI·(d²y/dx²) = M(x) — integrate twice, apply BCs
- Thermal stress (constrained): σ = Eα·ΔT
- Combined / principal stresses: Mohr's circle; σ_1,2 = σ_avg ± R

## Thermodynamics
- First law (closed system): Q − W = ΔU; per unit mass: q − w = Δu
- First law (open, steady): Q̇ − Ẇ = ṁ[(h₂−h₁) + (V₂²−V₁²)/2 + g(z₂−z₁)]
- Ideal gas: PV = mRT; Pv = RT
- Work (closed, quasi-static): W = ∫P dV
- Specific heats: Δu = c_v·ΔT, Δh = c_p·ΔT (ideal gas); c_p − c_v = R; k = c_p/c_v
- Entropy: ΔS = ∫δQ/T (reversible); isentropic ideal gas: Tv^(k−1) = const
- Carnot efficiency: η = 1 − T_L/T_H; COP_ref = T_L/(T_H − T_L)

## Fluid Mechanics
- Hydrostatics: P = ρgh
- Continuity: ṁ = ρAV = const; incompressible: A₁V₁ = A₂V₂
- Bernoulli (inviscid, incompressible, steady, along streamline):
  P/ρ + V²/2 + gz = const
- Reynolds number: Re = ρVD/μ = VD/ν (pipe: laminar < 2300)
- Major head loss: h_f = f·(L/D)·(V²/2g) — f from Moody chart / Colebrook
- Minor loss: h_L = K·V²/2g
- Energy equation w/ losses & pumps: extends Bernoulli with h_pump, h_turbine, h_L

## Heat Transfer
- Conduction (Fourier): q = −kA·(dT/dx); plane wall: Q̇ = kA·ΔT/L
- Thermal resistance: R_cond = L/(kA), R_conv = 1/(hA); series/parallel like circuits
- Convection (Newton's cooling): Q̇ = hA·(T_s − T_∞)
- Radiation: Q̇ = εσA(T_s⁴ − T_surr⁴), σ = 5.67e−8 W/m²K⁴
- Fins, lumped capacitance (Bi < 0.1), LMTD for heat exchangers
- Dimensionless: Nu = hL/k, Pr = ν/α, Bi = hL_c/k, Fo = αt/L_c²

## Machine Design
- Factor of safety: n = strength / stress (yield or ultimate basis — state which)
- Fatigue: S-N curve, endurance limit S_e, Goodman / Soderberg for mean+alt stress
- Stress concentration: σ_max = K_t·σ_nom
- Bolted joints, weld sizing, shaft design (combined bending + torsion), gear tooth
  bending (Lewis), bearing life (L10)

## Vibrations
- Natural frequency: ω_n = √(k/m); f_n = ω_n/2π
- Damping ratio: ζ = c/(2√(km)); damped: ω_d = ω_n√(1−ζ²)
- Underdamped (ζ<1), critically damped (ζ=1), overdamped (ζ>1)
- Forced response: amplitude peaks near resonance r = ω/ω_n ≈ 1

## Useful constants
- g = 9.81 m/s² = 32.2 ft/s²
- R_universal = 8.314 J/mol·K = 1545 ft·lbf/lbmol·°R
- gc = 32.174 lbm·ft/(lbf·s²)  ← US-customary conversion factor
- σ_SB = 5.67×10⁻⁸ W/m²·K⁴
- Steel: E ≈ 200 GPa, ν ≈ 0.3 | Aluminum: E ≈ 69 GPa, ν ≈ 0.33
