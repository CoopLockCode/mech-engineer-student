# Engineering Graphics Reference

Study companion for Engineering Graphics.
Covers orthographic & isometric projection, multiview drawing, sectioning, auxiliary views, dimensioning, conventional tolerancing, GD&T fundamentals, and CAD modeling concepts. Written at a depth that supports a graduate-level tutor explaining the *why* behind every convention.

Math is in plain text: subscripts inline, `x^2` = x squared.

---

## 1. The Purpose & Language of Engineering Graphics

Engineering drawings are the **unambiguous, universal language** of design — they communicate geometry, dimensions, tolerances, materials, and manufacturing intent from designer to manufacturer to inspector. A correct drawing has exactly **one interpretation**. The governing standards in the US are **ASME Y14.x** (Y14.1 sheet sizes, Y14.2 line conventions, Y14.3 multiview/sectional views, Y14.5 dimensioning & tolerancing/GD&T); the international counterpart is **ISO**.

Two key projection families:
- **Multiview (orthographic) projection** — multiple 2-D views, each true-shape; the working-drawing standard.
- **Pictorial projection** (isometric, oblique, perspective) — a single 3-D-looking view; used for visualization, assembly instructions, and communication with non-technical audiences.

---

## 2. Projection Theory

### 2.1 Orthographic projection
The object is viewed along **parallel projectors perpendicular to the plane of projection**. Each view shows two of the three dimensions in true length, with no foreshortening (unless a surface is inclined/oblique).

- **Third-angle projection** — the US standard. The projection plane is *between* the observer and the object; each view is placed on the side of the object it represents (top view above the front, right-side view to the right). Symbol: a truncated cone with the small end toward the viewer.
- **First-angle projection** — the ISO/European standard. The object is *between* the observer and the plane; views are placed on the opposite side (top view below the front). Symbol: the truncated-cone symbol mirrored.
- Confusing the two is a classic and costly error — always check the projection symbol in the title block.

### 2.2 The six principal views and the glass-box model
Imagine the object inside a transparent box; project each face outward onto the six box walls (front, top, bottom, left, right, rear), then unfold the box into the plane of the paper. The **front view** is chosen to show the most characteristic shape with the fewest hidden lines and is usually the object's natural/functional orientation.

### 2.3 View selection and alignment
- Choose the **minimum number of views** that fully describe the object — typically **three** (front, top, right side). A simple prism may need two; a part of revolution may need one (with a diameter callout).
- **Alignment rules:** the top view aligns *vertically* with the front; the side view aligns *horizontally* with the front. Use the **45° miter line** to transfer depth between the top and side views.
- The three views share dimensions: front & top share **width**; front & side share **height**; top & side share **depth**. ("Width transfers between front and top; depth transfers between top and side via the miter line.")

### 2.4 Surface types in multiview
- **Normal surface** — parallel to a principal plane; appears true-shape in one view, as an edge (line) in the other two.
- **Inclined surface** — perpendicular to one principal plane, tilted to the others; appears as an edge in one view and **foreshortened** (not true-shape) in the others. Its true shape requires an **auxiliary view**.
- **Oblique surface** — not perpendicular to any principal plane; foreshortened in *all* principal views; true shape needs a secondary auxiliary view.

### 2.5 Pitfalls
- Mixing first- and third-angle conventions on one drawing.
- Showing more views than needed (clutter) or too few (ambiguity).
- Drawing an inclined surface as true-shape in a principal view — it must appear foreshortened.

---

## 3. Pictorial (3-D) Projections

### 3.1 Isometric projection
- The three principal axes are spaced **120° apart**; the object is rotated so all three are equally foreshortened.
- **Isometric drawing** (the practical version): measurements along the three isometric axes are drawn at *true length* (the ~0.816 isometric scale factor is ignored for convenience).
- **Isometric lines** (parallel to the three axes) are measured true; **non-isometric lines** (e.g. the slope of an inclined face, a diagonal) are **not** true length and must be located by their endpoints — never measured directly along the line.
- Circles on isometric faces become **ellipses** — drawn with the four-center approximation or an ellipse template; the major axis is perpendicular to the axis of the cylindrical feature.

### 3.2 Oblique projection
One face is drawn true-shape (parallel to the picture plane) with depth lines receding at an angle (commonly 30°/45°/60°):
- **Cavalier** — full-scale depth (looks elongated).
- **Cabinet** — depth at half scale (more realistic proportions).

### 3.3 Perspective projection
Receding lines converge to **vanishing points** (one-, two-, or three-point perspective). Most realistic, but distances are not measurable — used for presentation, not for working drawings.

### 3.4 Pitfalls
- Measuring non-isometric lines directly along their length (must locate endpoints).
- Drawing isometric circles as true circles instead of ellipses.

---

## 4. Line Conventions (the "Alphabet of Lines")

| Line | Weight | Use |
|------|--------|-----|
| **Visible (object) line** | Thick, continuous | Visible edges and contours |
| **Hidden line** | Thin, short dashes | Edges/features hidden from view |
| **Center line** | Thin, long-short-long | Axes of symmetry, centers of holes/circles, bolt circles |
| **Dimension line** | Thin, continuous, with arrowheads | Indicates the measured extent |
| **Extension line** | Thin, continuous | Projects from the feature to the dimension line (small visible gap from the object) |
| **Leader line** | Thin, continuous, angled | Points to a feature for a note or dimension |
| **Section line (hatching)** | Thin, continuous, evenly spaced (usually 45°) | Indicates cut solid material in a section view |
| **Cutting-plane line** | Thick, long dash + two short dashes, with arrows | Shows where a section is cut and the viewing direction |
| **Phantom line** | Thin, long-dash-dash | Alternate positions, adjacent parts, repeated detail |
| **Break line** | Thick freehand (short) or thin ruled zig-zag (long) | Shortened/broken-out views |

**Line precedence** when lines coincide: visible line > hidden line > center line.

---

## 5. Sectioning (Section Views)

### 5.1 Purpose
Section views expose **interior features** that would otherwise be a confusing tangle of hidden lines. An imaginary **cutting plane** slices the object; the near half is removed; the cut solid faces are crosshatched (**section lining**). The cutting-plane line on the adjacent view shows the cut location, and its arrows show the **viewing direction**.

### 5.2 Types of section views
| Type | Description |
|------|-------------|
| **Full section** | Cutting plane passes entirely through the object |
| **Half section** | Plane cuts halfway (one quarter removed); shows interior on one half, exterior on the other — ideal for symmetric parts |
| **Offset section** | Cutting plane is stepped/jogged to pass through several features not in a straight line |
| **Broken-out section** | Only a small portion is broken away to expose a local interior feature |
| **Revolved section** | Cross-sectional shape revolved 90° in place onto the view (e.g. for a spoke, rib, arm) |
| **Removed section** | Like revolved, but placed off to the side along a reference line |
| **Aligned section** | Angled features (spokes, holes, ribs) are rotated into the cutting plane for clarity |

### 5.3 Section conventions
- **Hidden lines are generally omitted** in section views (the section already shows the interior).
- **Section lining (hatch)** is angled (usually 45°), evenly spaced; different parts in an assembly use **different hatch angles/spacing** to distinguish them; the same part keeps the *same* hatch in every view.
- **Features NOT sectioned even when the plane passes through them** ("non-sectioned" parts): ribs, webs, spokes, gear teeth, fasteners (bolts, nuts, screws, rivets), shafts, keys, pins, ball/roller bearings. Sectioning these would be misleading — a rib drawn solid would look like a thick disk.
- Thin features (gaskets, sheet metal) are shown solid black rather than hatched.

### 5.4 Pitfalls
- Crosshatching a rib, web, shaft, or fastener that the plane passes through (convention says don't).
- Leaving hidden lines in a section view.
- Forgetting the cutting-plane arrows define the viewing direction (the section shows what you see *looking in the arrow direction*).

---

## 6. Auxiliary Views

When an **inclined surface** appears foreshortened in all principal views, an **auxiliary view** is projected on a plane *parallel to the inclined surface*, showing its **true shape and size**.
- **Primary auxiliary view** — projected from one principal view to show a surface inclined to one principal plane.
- **Secondary auxiliary view** — projected from a primary auxiliary view to show an **oblique** surface (inclined to all principal planes) in true shape.
- The depth dimension in the auxiliary view is transferred from the principal view it is *not* projected from, measured perpendicular to the folding/reference line.
- Only the inclined surface of interest is usually drawn true-shape (a **partial auxiliary view**); the rest is omitted to reduce clutter.

---

## 7. Dimensioning

### 7.1 Principles
- **Dimension for function and manufacture** — locate features the way they are used and made; reference from functional datum surfaces, not arbitrary edges.
- **Each dimension stated once** — no duplicate dimensions.
- **No redundant / over-dimensioning** — every feature fully defined, nothing dimensioned twice; do not dimension to hidden lines.
- **Place dimensions in the view that shows the feature's true shape / contour.**
- **Group and align** dimensions; keep them off the object where possible; smallest dimensions nearest the object, larger ones farther out (avoid crossing extension/dimension lines).
- **Chain vs baseline (datum) dimensioning:** chain dimensioning accumulates tolerance stack-up; **baseline dimensioning** (all from one origin) avoids accumulation and is preferred for precision features.

### 7.2 Size vs location
- **Size dimensions** define how big a feature is (length, diameter, radius, angle).
- **Location dimensions** define where a feature is relative to a datum or another feature.

### 7.3 Standard dimensioning practices and symbols
| Symbol / abbreviation | Meaning |
|-----------------------|---------|
| ⌀ (or DIA) | Diameter |
| R | Radius |
| □ | Square feature |
| SR / S⌀ | Spherical radius / spherical diameter |
| ⌴ | Counterbore / spotface |
| ⌵ | Countersink |
| ↧ | Depth / deep |
| × | "by" / number of places (e.g. "4× ⌀6" = four 6 mm holes) |
| ( ) | Reference dimension (informational only, not toleranced) |
| TYP | Typical — the dimension repeats on like features |
| THRU | Feature goes completely through |

- **Cylinders** are dimensioned with a diameter (⌀) in the rectangular (non-circular) view; **holes** with diameter + depth; **arcs/fillets/rounds** with a radius (R).
- **Angles** in degrees; chamfers as a length × angle or two lengths.
- **Notes** carry repetitive or general information ("ALL FILLETS R3 UNLESS NOTED").

### 7.4 Pitfalls
- Dimensioning to hidden lines instead of the view that shows true shape.
- Over-dimensioning (giving the same information twice → conflicting requirements).
- Using chain dimensioning on precision features (tolerance stack-up).

---

## 8. Tolerancing — Conventional (Limit) Dimensioning

### 8.1 Core definitions
- **Tolerance** — the total permissible variation of a dimension = (upper limit − lower limit). No part is made perfectly; tolerance states how imperfect is acceptable.
- **Nominal size** — the designation used for general identification (e.g. ⌀10).
- **Basic size** — the theoretical size from which limits are derived.
- **Limits** — the maximum and minimum permissible sizes.
- **Bilateral tolerance** — variation in both directions (10 ±0.1). **Unilateral tolerance** — variation in one direction only (10 +0.2/−0.0).

### 8.2 Fits between mating parts
- **Clearance fit** — the internal feature is always smaller than the external; there is always a gap (free-running parts).
- **Interference (press/force) fit** — the internal feature is always larger; there is always overlap (the parts must be pressed/shrunk together — bearings, dowels).
- **Transition fit** — depending on where the actual sizes fall, the assembly could be a slight clearance or slight interference (locating fits).
- **Allowance** — the *intentional* (minimum) clearance or *maximum* interference between mating parts = the tightest possible assembly condition. (Distinct from tolerance, which is the *permitted variation*.)
- **Hole-basis** vs **shaft-basis** systems — one member is held at a standard limit and the fit is created by varying the other.

### 8.3 Tolerance stack-up
The accumulation of individual tolerances along a chain of dimensions. **Worst-case** analysis sums tolerances arithmetically (guaranteed but conservative); **statistical (RSS)** analysis takes the root-sum-square (realistic for high-volume production). Baseline dimensioning minimizes stack-up.

### 8.4 Pitfalls
- Confusing **allowance** (intentional tightest fit) with **tolerance** (permitted variation).
- Specifying tight tolerances "to be safe" — cost rises steeply with tightness.
- Ignoring stack-up when chain-dimensioning.

---

## 9. GD&T Fundamentals (ASME Y14.5)

### 9.1 Why GD&T
Conventional ± tolerancing creates **rectangular tolerance zones** and cannot fully express functional intent (e.g. "this hole must be round AND located AND perpendicular"). **Geometric Dimensioning & Tolerancing** defines tolerance *zones* for geometric characteristics, ties them to **datums** (a coordinate reference frame), and unambiguously communicates design intent across design, manufacturing, and inspection. It can also yield **bonus tolerance**, increasing the number of acceptable parts without compromising function.

### 9.2 The 14 geometric characteristic symbols
| Symbol | Name | Category | Datum needed? | Modifiers? |
|--------|------|----------|---------------|-----------|
| ⏤ | Straightness | Form | No | Yes (feature of size) |
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

- **Form (4)** — never reference a datum; control a feature's shape relative to itself (a flat surface should be flat; a cylinder should be cylindrical).
- **Orientation (3)** — always reference a datum; control an angular relationship (90°, parallel, or a specified angle).
- **Profile (2)** — the most versatile; can control size, form, orientation, and location of a surface or line, with or without datums.
- **Location (3)** — Position is the workhorse for holes/bosses; Concentricity and Symmetry are deprecated (use Position or Profile instead).
- **Runout (2)** — always reference a datum axis; circular runout is checked at single cross-sections, total runout over the whole surface; runout combines form + orientation + location error as a part is rotated.

### 9.3 The feature control frame
Read left to right, the **feature control frame** is the sentence of GD&T:
`[ geometric symbol | ⌀ (if cylindrical zone) + tolerance value + material modifier | primary datum + modifier | secondary datum | tertiary datum ]`
- A leader/arrow connects it to the controlled feature: pointing at a **surface** controls that surface; pointing at a **size dimension** controls the feature's **axis or center plane**.
- Compartment 1 — the geometric characteristic symbol.
- Compartment 2 — the tolerance: optional ⌀ (cylindrical zone), the numeric value, and an optional material-condition modifier.
- Compartments 3–5 — up to three datum references in **precedence order** (primary, secondary, tertiary).

### 9.4 Datums and the Datum Reference Frame (DRF)
- A **datum** is a theoretically exact point, axis, or plane from which measurements are taken — the GD&T equivalent of a coordinate system's origin.
- A **datum feature** is the actual (imperfect) part surface used to establish a datum; it is labeled with a **datum feature symbol** (a letter in a box attached to a triangle).
- The **Datum Reference Frame** is three mutually perpendicular datum planes — a full coordinate system.
- **3-2-1 rule** of part location: the **primary datum** contacts the part at a minimum of 3 points (constrains 3 DOF), the **secondary** at 2 points (2 more DOF), the **tertiary** at 1 point (the last DOF) — together fully locating the part for inspection.
- Datum precedence (order in the feature control frame) reflects function — it is **not alphabetical**.

### 9.5 Material-condition modifiers and bonus tolerance
| Modifier | Symbol | Meaning |
|----------|--------|---------|
| Maximum Material Condition | Ⓜ (MMC) | Feature has the most material — largest shaft / smallest hole. Permits **bonus tolerance**. |
| Least Material Condition | Ⓛ (LMC) | Feature has the least material — smallest shaft / largest hole. |
| Regardless of Feature Size | (RFS) | Default; the geometric tolerance is fixed regardless of the feature's actual size — no bonus. |
| Projected Tolerance Zone | Ⓟ | The tolerance zone is projected beyond the part surface (for threaded/press-fit holes that locate a mating part). |

- **Bonus tolerance** — when Ⓜ is applied, as the feature departs from MMC toward LMC, the *available* geometric tolerance grows: `bonus = |actual feature size − MMC size|`. Total positional tolerance = stated tolerance + bonus. This rewards parts made away from worst-case and improves yield with no loss of function.
- **Virtual condition** — the worst-case mating boundary = MMC size combined with the geometric tolerance (subtract for a hole, add for a shaft). It is the size of the functional gage that checks the feature.

### 9.6 Pitfalls
- Putting a datum on a **form** control (form tolerances never use datums).
- Forgetting bonus tolerance under MMC — rejecting good parts or under-using available tolerance.
- Treating datum letters as a sequence (A, B, C) — the *order in the frame* sets precedence, and you can use any letters in any order.
- Pointing the feature control frame leader at the wrong target (surface vs. axis control).

---

## 10. CAD Modeling Concepts

### 10.1 Modeling paradigms
- **2-D drafting** — electronic drawing board; lines, arcs, dimensions; no 3-D intelligence.
- **Wireframe** — edges only; ambiguous (no surface/solid information).
- **Surface modeling** — defines skins/faces; good for complex aesthetic shapes (automotive, consumer products); no inherent mass/volume.
- **Solid modeling** — fully defined 3-D volume; supports mass properties, interference checking, FEA, CAM. The standard for mechanical design.

### 10.2 Parametric, feature-based modeling
Modern CAD (SolidWorks, Inventor, Creo, Fusion 360, NX) is **parametric** and **feature-based**:
- The model is built as a **history tree** of **features** (extrude, revolve, sweep, loft, hole, fillet, chamfer, shell, pattern, rib, draft).
- Geometry is driven by **parameters** (dimensions) and **constraints/relations** — change a parameter and the model regenerates ("design intent" is captured, not just geometry).
- **Sketches** are 2-D profiles, controlled by **geometric constraints** (coincident, parallel, perpendicular, tangent, concentric, equal, symmetric) and **dimensional constraints**; a sketch should be **fully constrained** (defined) before being used to create a feature — under-constrained sketches move unpredictably; over-constrained sketches conflict.
- **Design intent** — model so that intended relationships survive edits (e.g. a hole stays centered, a wall stays a fixed offset). Good feature ordering and reference choice make later edits robust.

### 10.3 Assemblies
- Components are positioned with **mates/constraints** (coincident, concentric, distance, angle).
- **Bottom-up** assembly — parts modeled first, then assembled. **Top-down** — geometry created in the assembly context, parts referencing each other.
- Assemblies support **interference detection**, motion studies, exploded views, and bill-of-materials generation.

### 10.4 The model-drawing-manufacturing chain
3-D solid model → 2-D **drawing** (auto-generated views, sections, dimensions — associative, so the drawing updates with the model) → optionally **MBD (model-based definition)**, where GD&T and PMI (product & manufacturing information) live on the 3-D model itself, no 2-D drawing → **CAM** toolpaths or **AM** slicing → inspection (CMM programs driven from the same model).

### 10.5 Pitfalls
- Leaving sketches under-defined — geometry shifts on edit.
- Building a brittle history tree (features referencing unstable geometry) — edits break the model.
- Modeling without design intent — the model is "right" once but unmaintainable.

---

## Quick-Reference Summary Tables

### Projection at a glance
| | Third-angle (US) | First-angle (ISO) |
|---|---|---|
| Plane location | Between observer and object | Object between observer and plane |
| Top view placed | Above front view | Below front view |
| Right-side view placed | Right of front view | Left of front view |

### Dimension transfer between the 3 standard views
| Shared dimension | Between views |
|---|---|
| Width | Front ↔ Top |
| Height | Front ↔ Side |
| Depth | Top ↔ Side (via 45° miter line) |

### GD&T category cheat-sheet
| Category | Symbols | Datum? |
|---|---|---|
| Form | straightness, flatness, circularity, cylindricity | Never |
| Orientation | angularity, perpendicularity, parallelism | Always |
| Profile | profile of a line, profile of a surface | Sometimes |
| Location | position, concentricity*, symmetry* | Usually |
| Runout | circular runout, total runout | Always |
*deprecated in ASME Y14.5-2018

---

## Open-source sources used

- **GD&T Basics — "GD&T Symbols Explained: Full Reference Guide"** (the 14 ASME Y14.5 symbols, categories, feature control frame, datums, material-condition modifiers, bonus tolerance). https://www.gdandtbasics.com/gdt-symbols/
- **Tec-Ease — GD&T Symbols & Terms free resource glossary** (datum reference frame, modifiers, terminology). https://www.tec-ease.com/gdt-symbols-terms.php
- **"Engineering Graphics" / "Technical Drawing" open educational resources** — open-textbook treatments of orthographic projection, multiview drawing, sectioning, auxiliary views, and dimensioning (OpenStax/community-college OER and BCcampus open texts on technical drawing).
- **MIT OpenCourseWare 2.007 / engineering design graphics materials** — CAD modeling, parametric/feature-based modeling, design intent. https://ocw.mit.edu/
- **Wikipedia — "Engineering drawing," "Orthographic projection," "Isometric projection," "Geometric dimensioning and tolerancing"** — cross-checked for standard conventions and ASME Y14.x references.
- General public university EDG/graphics course materials aligned with ASME Y14.5 and the Bertoline/Giesecke technical-graphics curriculum.
