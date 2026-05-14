# Engineering Chemistry Reference

> Engineering Chemistry. Graduate-level study companion: precise definitions, governing laws, derivations, problem-solving procedures, worked-example patterns, constants, and common student pitfalls. Plain-text notation throughout.

---

## 0. Measurement, Units, and Math Foundations

### Key constants

| Quantity | Symbol | Value |
|---|---|---|
| Avogadro's number | N_A | 6.022 x 10^23 /mol |
| Ideal gas constant | R | 8.314 J/(mol·K) = 0.08206 L·atm/(mol·K) |
| Standard molar volume (STP, 0 °C, 1 atm) | V_m | 22.4 L/mol |
| Faraday constant | F | 96,485 C/mol |
| Speed of light | c | 2.998 x 10^8 m/s |
| Planck constant | h | 6.626 x 10^-34 J·s |
| Standard atmosphere | atm | 101,325 Pa = 760 mmHg/torr = 1.013 bar |
| Standard temperature | — | 0 °C = 273.15 K |

### Unit conversions and SI prefixes

- Temperature: K = °C + 273.15; °C = (°F - 32) × 5/9.
- Mass: 1 kg = 1000 g; volume: 1 L = 1000 mL = 1000 cm^3.
- Prefixes: nano (10^-9), micro (10^-6), milli (10^-3), centi (10^-2), kilo (10^3), mega (10^6).
- **Dimensional analysis (factor-label method):** multiply by conversion factors written as fractions so unwanted units cancel. This is the backbone of nearly every chemistry calculation.

### Significant figures

- All nonzero digits significant; captive zeros significant; leading zeros not; trailing zeros significant only with a decimal point.
- **Multiply/divide:** result keeps the fewest sig figs of any factor.
- **Add/subtract:** result keeps the fewest decimal places.
- Exact numbers (counts, defined conversions) have infinite sig figs.

### Accuracy vs precision

Accuracy = closeness to the true value. Precision = reproducibility / closeness of repeated measurements to each other. Systematic error hurts accuracy; random error hurts precision.

**Pitfall:** Rounding intermediate steps — carry extra digits and round only the final answer.

---

## 1. Matter and Its Classification

### 1.1 Definitions

- **Matter:** anything with mass and volume.
- **Element:** cannot be broken down chemically (one type of atom).
- **Compound:** two or more elements chemically bonded in fixed ratio.
- **Mixture:** physical combination, variable composition. Homogeneous (uniform, "solution") vs heterogeneous (non-uniform).
- **Pure substance:** element or compound; fixed composition.

### 1.2 States of matter

Solid (fixed shape & volume), liquid (fixed volume, takes container shape), gas (fills container). Plasma at extreme conditions.

### 1.3 Properties and changes

- **Physical property:** observed without changing identity (density, melting point, color).
- **Chemical property:** describes how a substance reacts (flammability, reactivity).
- **Physical change:** identity preserved (phase change, dissolving).
- **Chemical change:** new substances formed (signs: gas evolution, precipitate, color change, energy release/absorption, hard to reverse).
- **Law of Conservation of Mass:** mass is neither created nor destroyed in a chemical reaction.
- **Law of Definite Proportions:** a compound always contains the same elements in the same mass ratio.
- **Law of Multiple Proportions:** when two elements form more than one compound, the masses of one element combining with a fixed mass of the other are in small whole-number ratios.

### 1.4 Density

ρ = m / V (common units g/cm^3 or g/mL). A characteristic physical property; used to identify substances and as a conversion factor between mass and volume.

---

## 2. Atomic Structure

### 2.1 Subatomic particles

| Particle | Charge | Mass (amu) | Location |
|---|---|---|---|
| Proton | +1 | ~1.007 | nucleus |
| Neutron | 0 | ~1.009 | nucleus |
| Electron | -1 | ~0.00055 | electron cloud |

- **Atomic number Z** = number of protons = element identity.
- **Mass number A** = protons + neutrons.
- **Isotopes:** same Z, different number of neutrons (different A).
- **Ions:** atoms with unequal protons and electrons — cations (+, lost electrons), anions (−, gained electrons).
- **Atomic mass** (on the periodic table) = weighted average of isotope masses: atomic mass = Σ (isotope mass × fractional abundance).

### 2.2 Development of atomic theory (the key experiments)

- Dalton's atomic theory (atoms, conservation of mass, definite proportions).
- Thomson — cathode-ray tube → discovered the electron; "plum pudding" model.
- Millikan oil-drop — measured the charge of the electron.
- Rutherford gold-foil — dense, tiny, positively charged nucleus; atom is mostly empty space.
- Bohr — quantized electron orbits, explained the hydrogen line spectrum.
- Quantum mechanical model — electrons described by orbitals (probability distributions), not fixed paths.

### 2.3 Light, energy, and the quantum model

- Electromagnetic radiation: c = λ ν (speed = wavelength × frequency).
- Photon energy: E = h ν = h c / λ.
- **Bohr model / hydrogen spectrum:** electrons occupy discrete energy levels; emission/absorption corresponds to transitions. ΔE = E_final - E_initial; Rydberg-type relation: 1/λ = R_H (1/n1^2 − 1/n2^2).
- Lower n = lower (more negative) energy, closer to nucleus.

### 2.4 Quantum numbers and orbitals

| Quantum number | Symbol | Allowed values | Meaning |
|---|---|---|---|
| Principal | n | 1, 2, 3, ... | shell, size/energy |
| Angular momentum | l | 0 to n−1 | subshell shape (0=s, 1=p, 2=d, 3=f) |
| Magnetic | m_l | −l to +l | orbital orientation |
| Spin | m_s | +1/2 or −1/2 | electron spin |

Orbital capacities: s = 2, p = 6, d = 10, f = 14 electrons. Shapes: s = sphere, p = dumbbell, d = cloverleaf (mostly).

### 2.5 Electron configuration

Three rules:
1. **Aufbau principle:** fill lowest-energy orbitals first. Order: 1s 2s 2p 3s 3p 4s 3d 4p 5s 4d 5p 6s 4f 5d 6p 7s ...
2. **Pauli exclusion principle:** no two electrons in an atom have the same four quantum numbers → max 2 per orbital, opposite spins.
3. **Hund's rule:** fill degenerate orbitals singly with parallel spins before pairing.

- Condensed notation: [noble gas] + remaining. Example: Fe = [Ar] 4s^2 3d^6.
- Valence electrons = outermost s and p (and relevant d) electrons; they govern chemistry.
- **Anomalies:** Cr = [Ar]4s^1 3d^5 and Cu = [Ar]4s^1 3d^10 (half-filled / filled d-subshell stability).

**Pitfall:** Writing 3d before 4s in *order of filling* — fill 4s first, but when writing the final configuration list 3d after 3p by shell. For transition-metal cations, remove 4s electrons before 3d.

---

## 3. The Periodic Table and Periodic Trends

### 3.1 Organization

- Periods = rows (same n for the valence shell); groups/families = columns (same valence configuration → similar chemistry).
- Key groups: alkali metals (1), alkaline earth (2), halogens (17), noble gases (18). Blocks: s, p, d (transition metals), f (lanthanides/actinides).
- Metals (left, lose electrons), nonmetals (upper right, gain electrons), metalloids (staircase).

### 3.2 Trends (and the reasons)

Two competing factors drive every trend: **effective nuclear charge Z_eff** (increases left→right) and **shell number n / shielding** (increases top→bottom).

| Trend | Across period (L→R) | Down a group |
|---|---|---|
| Atomic radius | decreases (↑ Z_eff pulls electrons in) | increases (↑ n) |
| Ionization energy (IE) | increases | decreases |
| Electron affinity | becomes more negative (more favorable) | less negative |
| Electronegativity | increases | decreases |
| Metallic character | decreases | increases |

- **Ionization energy:** energy to remove an electron; successive IEs increase; large jump when you break into a noble-gas core.
- **Ionic radii:** cations smaller than parent atom; anions larger. Isoelectronic series: more protons → smaller radius.

**Pitfall:** Forgetting that noble gases generally have very high IE and that there are minor irregularities (e.g., IE of B < Be, O < N) caused by subshell stability.

---

## 4. Chemical Bonding and Molecular Geometry

### 4.1 Bond types

- **Ionic bond:** electron transfer between metal and nonmetal; electrostatic attraction of ions; forms a lattice. Large electronegativity difference (ΔEN ≳ 1.7).
- **Covalent bond:** electron sharing between nonmetals. Nonpolar (ΔEN ≈ 0–0.4), polar (ΔEN ≈ 0.4–1.7).
- **Metallic bond:** "sea of delocalized electrons" among metal cations.

### 4.2 Lewis structures

Procedure:
1. Count total valence electrons (add for negative charge, subtract for positive).
2. Choose central atom (least electronegative, never H).
3. Connect atoms with single bonds; distribute remaining electrons as lone pairs to satisfy the **octet rule** (H wants 2).
4. If the central atom lacks an octet, form double/triple bonds.
5. Check **formal charge** = (valence e−) − (lone-pair e−) − (1/2 bonding e−); the best structure minimizes formal charges and puts negative formal charge on the most electronegative atom.

- **Resonance:** when multiple valid Lewis structures exist, the real structure is a hybrid (e.g., ozone, nitrate, carbonate).
- **Exceptions to the octet:** incomplete octets (B, Be), odd-electron species (NO, NO2), expanded octets (period 3+ central atoms: SF6, PCl5).

### 4.3 VSEPR theory (molecular geometry)

Electron domains (bonds + lone pairs) around the central atom arrange to minimize repulsion. Lone pairs repel more strongly than bonding pairs.

| Electron domains | Electron geometry | Example shapes (by # lone pairs) |
|---|---|---|
| 2 | linear (180°) | linear |
| 3 | trigonal planar (120°) | trigonal planar (0 LP), bent (1 LP) |
| 4 | tetrahedral (109.5°) | tetrahedral (0), trigonal pyramidal (1), bent (2) |
| 5 | trigonal bipyramidal (90/120°) | seesaw, T-shaped, linear |
| 6 | octahedral (90°) | octahedral, square pyramidal, square planar |

### 4.4 Polarity

A molecule is polar if it has polar bonds AND the bond dipoles do not cancel by symmetry. Example: CO2 is nonpolar (linear, dipoles cancel); H2O is polar (bent). Net dipole moment determines polarity.

### 4.5 Valence bond theory and hybridization

- Bonds form by orbital overlap. **Sigma (σ)** bond = head-on overlap (single bonds, and one bond of every multiple bond). **Pi (π)** bond = side-on overlap of p orbitals (the extra bonds in double/triple bonds).
- **Hybridization** matches geometry: sp (2 domains, linear), sp2 (3, trigonal planar), sp3 (4, tetrahedral), sp3d (5), sp3d2 (6).
- A double bond = 1 σ + 1 π; a triple bond = 1 σ + 2 π.

### 4.6 Intermolecular forces (IMFs) — weakest to strongest

1. **London dispersion forces** — present in all molecules; stronger for larger, more polarizable molecules.
2. **Dipole–dipole** — between polar molecules.
3. **Hydrogen bonding** — special strong dipole–dipole when H is bonded to N, O, or F.
4. (Ion–dipole — relevant in solutions of ionic compounds.)

IMFs determine boiling/melting points, viscosity, surface tension, vapor pressure. **Pitfall:** confusing IMFs (between molecules) with intramolecular bonds (within a molecule) — boiling water breaks IMFs, not O–H bonds.

---

## 5. Chemical Nomenclature and Formulas

- **Ionic (metal + nonmetal):** name cation then anion; monatomic anion ends in -ide. Transition metals use Roman numerals for charge (Fe^2+ = iron(II)). Polyatomic ions memorized: nitrate NO3−, sulfate SO4^2−, carbonate CO3^2−, phosphate PO4^3−, ammonium NH4+, hydroxide OH−, etc. -ate vs -ite (one fewer oxygen).
- **Molecular (two nonmetals):** Greek prefixes (mono, di, tri, tetra...). Example: N2O4 = dinitrogen tetroxide.
- **Acids:** binary acids (H + nonmetal) → hydro-...-ic acid (HCl = hydrochloric). Oxyacids → -ate becomes -ic acid, -ite becomes -ous acid (H2SO4 sulfuric, H2SO3 sulfurous).

---

## 6. Stoichiometry — The Mole and Reaction Calculations

### 6.1 The mole

- 1 mole = 6.022 × 10^23 entities (Avogadro's number).
- **Molar mass** (g/mol) = sum of atomic masses; numerically equal to the formula mass in amu.
- Core conversions: mass ↔ moles (÷ or × molar mass); moles ↔ particles (× or ÷ N_A); for gases at STP, moles ↔ volume (× or ÷ 22.4 L/mol).

### 6.2 Composition

- **Percent composition:** %element = (mass of element in 1 mol / molar mass) × 100.
- **Empirical formula:** smallest whole-number ratio of atoms. Procedure: assume 100 g → grams of each element → moles → divide all by the smallest → multiply to whole numbers.
- **Molecular formula** = (molar mass / empirical formula mass) × empirical formula.

### 6.3 Balancing equations

Conserve atoms of each element (and charge). Adjust coefficients only — never subscripts. Balance metals, then nonmetals, then H, then O; use fractions then clear them.

### 6.4 Stoichiometric calculations

The mole ratio from the balanced equation is the bridge. General path:
```
mass A → moles A → (mole ratio) → moles B → mass B
```

### 6.5 Limiting reactant and yield

- **Limiting reactant:** the one that runs out first — limits product. Method: compute moles of product each reactant could make; the smaller is limiting. The other is in excess.
- **Theoretical yield:** maximum product from the limiting reactant.
- **Percent yield** = (actual yield / theoretical yield) × 100.

### 6.6 Solution stoichiometry

- **Molarity:** M = moles solute / liters solution.
- **Dilution:** M1 V1 = M2 V2.
- Titration: at equivalence point, moles relate by the balanced-equation ratio; used to find unknown concentrations.

**Pitfall:** Forgetting to convert volume to liters for molarity; using mass ratios instead of mole ratios; changing subscripts when balancing.

---

## 7. Reactions in Aqueous Solution and Reaction Types

### 7.1 Solubility and electrolytes

- Soluble ionic compounds dissociate into ions (strong electrolytes). Use solubility rules (most nitrates, group 1, ammonium soluble; many sulfides, carbonates, phosphates, hydroxides insoluble).
- Strong electrolytes fully dissociate; weak electrolytes partially; nonelectrolytes don't.
- **Molecular, complete ionic, and net ionic equations.** Spectator ions cancel; the net ionic equation shows the actual chemical change.

### 7.2 Reaction classes

| Type | Pattern | Example |
|---|---|---|
| Combination/synthesis | A + B → AB | 2H2 + O2 → 2H2O |
| Decomposition | AB → A + B | 2H2O2 → 2H2O + O2 |
| Single replacement | A + BC → AC + B | Zn + 2HCl → ZnCl2 + H2 |
| Double replacement | AB + CD → AD + CB | AgNO3 + NaCl → AgCl + NaNO3 |
| Combustion | hydrocarbon + O2 → CO2 + H2O | CH4 + 2O2 → CO2 + 2H2O |
| Acid–base (neutralization) | acid + base → salt + water | HCl + NaOH → NaCl + H2O |
| Precipitation | forms insoluble solid | per solubility rules |

### 7.3 Acids and bases (intro)

- **Arrhenius:** acid produces H+ in water; base produces OH−.
- **Brønsted–Lowry:** acid = proton (H+) donor; base = proton acceptor; conjugate acid–base pairs differ by one H+.
- Strong acids (HCl, HBr, HI, HNO3, H2SO4, HClO4) and strong bases (group 1/2 hydroxides) ionize completely.
- pH = −log[H+]; pOH = −log[OH−]; pH + pOH = 14 at 25 °C; neutral pH = 7.
- Kw = [H+][OH−] = 1.0 × 10^-14 at 25 °C.

### 7.4 Oxidation–reduction (redox)

- **Oxidation = loss of electrons** (oxidation number increases); **reduction = gain of electrons** ("OIL RIG").
- Oxidizing agent is reduced; reducing agent is oxidized.
- Oxidation-number rules: free element = 0; monatomic ion = its charge; O usually −2 (−1 in peroxides); H usually +1 (−1 with metals); sum = overall charge.
- Balance redox by half-reactions (mass and charge balanced separately, then combined).

---

## 8. Gases

### 8.1 Kinetic molecular theory (KMT)

Assumptions for an ideal gas: particles are point masses (negligible volume), in constant random motion, with no intermolecular forces, undergoing perfectly elastic collisions; average kinetic energy ∝ absolute temperature.

### 8.2 The gas laws

| Law | Relationship | Held constant |
|---|---|---|
| Boyle's law | P1 V1 = P2 V2 (P ∝ 1/V) | n, T |
| Charles's law | V1/T1 = V2/T2 (V ∝ T) | n, P |
| Gay-Lussac's law | P1/T1 = P2/T2 (P ∝ T) | n, V |
| Avogadro's law | V1/n1 = V2/n2 (V ∝ n) | P, T |
| Combined gas law | P1V1/T1 = P2V2/T2 | n |

### 8.3 Ideal gas law

```
P V = n R T
```
R = 0.08206 L·atm/(mol·K) or 8.314 J/(mol·K). **Always use absolute temperature (K).** Derived forms: density ρ = PM/(RT); molar mass M = ρRT/P = mRT/(PV).

### 8.4 Mixtures of gases

- **Dalton's law of partial pressures:** P_total = P1 + P2 + ... ; P_i = X_i P_total (X_i = mole fraction).
- Collecting gas over water: P_gas = P_total − P_water vapor.

### 8.5 Molecular speeds and effusion

- Average kinetic energy: KE_avg = (3/2) k_B T (per molecule); total = (3/2)nRT.
- Root-mean-square speed: u_rms = sqrt(3RT/M) — lighter molecules move faster at the same T.
- **Graham's law of effusion:** rate1/rate2 = sqrt(M2/M1).

### 8.6 Real gases

Deviate from ideal at **high pressure** (molecular volume not negligible) and **low temperature** (IMFs matter). The van der Waals equation corrects for both: [P + a(n/V)^2](V − nb) = nRT.

**Pitfall:** Using °C in gas-law calculations; forgetting to convert pressure units consistently; ignoring water vapor pressure in "collected over water" problems.

---

## 9. Thermochemistry

### 9.1 Definitions

- **System / surroundings / universe.** Internal energy E (or U).
- **Heat (q):** energy transferred due to a temperature difference. **Work (w):** energy transferred by a force acting through a distance; for gases w = −PΔV.
- **First Law of Thermodynamics (energy conservation):** ΔE = q + w. Energy of the universe is constant.
- Sign convention: q > 0 = heat absorbed by system (endothermic); q < 0 = heat released (exothermic); w > 0 = work done on system.
- **State function:** depends only on current state, not path (E, H, S, G, T, P, V). Heat and work are NOT state functions.

### 9.2 Enthalpy

- Enthalpy H = E + PV. At constant pressure, ΔH = q_p (heat of reaction).
- ΔH < 0 exothermic; ΔH > 0 endothermic.

### 9.3 Calorimetry

```
q = m c ΔT          (c = specific heat capacity, J/(g·°C))
q = C ΔT            (C = heat capacity of the object/calorimeter)
```
- Specific heat of water = 4.184 J/(g·°C).
- Coffee-cup calorimeter (constant P → ΔH); bomb calorimeter (constant V → ΔE).
- Conservation: q_lost by hot = −q_gained by cold (ignoring calorimeter losses).
- Phase changes occur at constant T: q = n·ΔH_fus (melting) or q = n·ΔH_vap (boiling).

### 9.4 Hess's Law

Because ΔH is a state function, the enthalpy of a reaction equals the sum of the enthalpies of any set of steps that add up to it. Reverse a reaction → reverse the sign of ΔH; multiply a reaction by a factor → multiply ΔH by the same factor.

### 9.5 Standard enthalpies of formation

- ΔH°_f = enthalpy change to form 1 mol of a compound from its elements in their standard states. ΔH°_f of an element in its standard state = 0.
- **Hess's law shortcut:**
```
ΔH°_rxn = Σ n ΔH°_f (products) − Σ n ΔH°_f (reactants)
```

### 9.6 Bond enthalpies

ΔH_rxn ≈ Σ (bond enthalpies broken) − Σ (bond enthalpies formed). Approximate — bonds broken cost energy, bonds formed release it.

**Pitfall:** Sign errors in Hess's law (reversing a reaction reverses ΔH's sign); forgetting to multiply ΔH by the stoichiometric coefficient; mixing up "broken − formed" vs "products − reactants" (they have opposite framings).

---

## 10. Introduction to Thermodynamics — Spontaneity

### 10.1 Entropy (S)

- Entropy is a measure of the dispersal of energy / number of accessible microstates (disorder).
- **Second Law of Thermodynamics:** the entropy of the universe increases for any spontaneous process: ΔS_universe = ΔS_system + ΔS_surroundings > 0.
- Entropy increases: solid → liquid → gas; dissolving (usually); increasing moles of gas; increasing temperature.
- **Third Law:** the entropy of a perfect crystal at 0 K is zero — gives an absolute reference. So absolute entropies S° are tabulated (always positive for substances above 0 K).
- ΔS°_rxn = Σ n S°(products) − Σ n S°(reactants).

### 10.2 Gibbs free energy (G)

```
ΔG = ΔH − T ΔS         (constant T, P)
```
- **ΔG < 0:** spontaneous (favorable) in the forward direction.
- **ΔG > 0:** nonspontaneous (reverse is spontaneous).
- **ΔG = 0:** system at equilibrium.

Temperature dependence of spontaneity:

| ΔH | ΔS | Result |
|---|---|---|
| − | + | spontaneous at all T |
| + | − | nonspontaneous at all T |
| − | − | spontaneous at low T |
| + | + | spontaneous at high T |

- ΔG° = ΣnΔG°_f(products) − ΣnΔG°_f(reactants).
- Relation to equilibrium: ΔG° = −RT ln K. K > 1 ↔ ΔG° < 0.

**Pitfall:** Using ΔS in J and ΔH in kJ without converting — both must be in the same energy unit before applying ΔG = ΔH − TΔS; and T must be in kelvin.

---

## 11. Introduction to Chemical Kinetics

### 11.1 Reaction rate

Rate = change in concentration per unit time. For aA + bB → cC + dD:
```
rate = −(1/a) Δ[A]/Δt = −(1/b) Δ[B]/Δt = (1/c) Δ[C]/Δt = (1/d) Δ[D]/Δt
```

### 11.2 Rate law

```
rate = k [A]^m [B]^n
```
- m, n = reaction orders (determined experimentally, NOT from coefficients); overall order = m + n.
- k = rate constant (its units depend on overall order).
- Determined by the **method of initial rates:** change one concentration at a time, see how the rate responds (double [A], rate doubles → first order in A; quadruples → second order).

### 11.3 Integrated rate laws

| Order | Integrated law | Linear plot | Half-life |
|---|---|---|---|
| Zero | [A] = [A]_0 − kt | [A] vs t | t½ = [A]_0/(2k) |
| First | ln[A] = ln[A]_0 − kt | ln[A] vs t | t½ = 0.693/k (constant) |
| Second | 1/[A] = 1/[A]_0 + kt | 1/[A] vs t | t½ = 1/(k[A]_0) |

### 11.4 Collision theory and activation energy

- Reactions occur when molecules collide with sufficient energy (≥ activation energy E_a) and correct orientation.
- **Arrhenius equation:** k = A e^(−E_a/RT). Higher T → larger fraction of effective collisions → faster.
- Two-temperature form: ln(k2/k1) = −(E_a/R)(1/T2 − 1/T1).

### 11.5 Catalysts and mechanisms

- A **catalyst** speeds up a reaction by providing a lower-E_a pathway; it is not consumed and does not change ΔH or the equilibrium position.
- A **reaction mechanism** is a sequence of elementary steps; the slowest step is the **rate-determining step**. The mechanism must sum to the overall reaction and be consistent with the observed rate law. Intermediates are produced then consumed.

**Pitfall:** Reading reaction orders off the balanced-equation coefficients — orders are experimental. Confusing rate (depends on concentration and changes over time) with the rate constant k (depends only on T and the catalyst).

---

## 12. General Problem-Solving Strategy (Chemistry)

1. **Identify what is asked and what is given;** write down units.
2. **Set up a dimensional-analysis chain** — most introductory chemistry problems are conversions through the mole.
3. For reactions: **balance the equation first**, then use mole ratios.
4. **Watch significant figures** and carry extra digits until the end.
5. **Sanity-check:** correct order of magnitude? Physically reasonable sign and direction? Units correct?

### Recurring student pitfalls (master list)

- Rounding intermediate results.
- Forgetting to convert temperature to kelvin (gas laws, thermodynamics, Arrhenius).
- Changing subscripts instead of coefficients when balancing.
- Using mass ratios instead of mole ratios in stoichiometry.
- Mixing kJ and J in ΔG = ΔH − TΔS.
- Reading reaction orders from coefficients instead of from experiment.
- Confusing IMFs with intramolecular bonds.
- Sign errors in Hess's law and in q (endo/exothermic).
- Forgetting water-vapor pressure in gas-collected-over-water problems.
- Treating weak acids/bases as fully ionized.
- Mixing up -ate/-ite and -ic/-ous in nomenclature.

---

## Open-source sources used

- OpenStax, *Chemistry 2e* — openstax.org/books/chemistry-2e — chapter outlines, key equations, key terms, and worked examples across atomic structure, periodicity, bonding, stoichiometry, gases, thermochemistry, thermodynamics, and kinetics.
- OpenStax, *Chemistry: Atoms First 2e* — openstax.org/books/chemistry-atoms-first-2e — alternative sequencing of atomic structure and bonding content.
- LibreTexts Chemistry, *General Chemistry* bookshelves, including the *Chemistry (OpenStax)* and *Map: Chemistry – The Central Science* texts — chem.libretexts.org — derivations, worked treatments of stoichiometry, gas laws, thermochemistry, and kinetics.
- LibreTexts, *ChemPRIME* and *Chem1 Virtual Textbook* — chem.libretexts.org — supplementary explanations of bonding, periodic trends, and thermodynamics.
