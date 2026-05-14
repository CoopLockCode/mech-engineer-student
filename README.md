# mech-engineer-student

A Claude Code skill that turns Claude into a mechanical engineering tutor —
statics, dynamics, thermo, fluids, heat transfer, mechanics of materials,
machine design, and the rest of the ME core.

## What it does

- **Tutor mode (default)** — teaches the method step-by-step so you can do the
  next problem yourself.
- **Solve mode** — say "just solve it" for a full worked solution without the
  teaching narration.
- **Full rigor on every problem** — states assumptions, draws the FBD/system
  sketch, names the governing equation, solves symbolically, carries units, and
  runs dimensional + limiting-case + order-of-magnitude checks before reporting.

## How to use it

The skill lives at `.claude/skills/mech-engineer-student/`. Claude Code
auto-discovers skills in the `.claude/skills/` folder of whatever project you're
working in.

**Option A — use it inside this project:**
```
cd C:\Users\CooperLockridge\Projects\mech-engineer-student
claude
```
Then just ask: *"help me with this statics problem: ..."* — the skill triggers
automatically on ME-flavored questions.

**Option B — make it available everywhere on this machine:**
Copy the skill folder into your global skills directory:
```
xcopy /E /I ".claude\skills\mech-engineer-student" "%USERPROFILE%\.claude\skills\mech-engineer-student"
```
Now it's available in every Claude Code session, any project.

You can also invoke it explicitly with `/mech-engineer-student`.

## About "helping people around the world"

Right now this is a **personal** skill — it makes *your* Claude better at ME
problems. It doesn't reach anyone else on its own.

To actually share it with other students you'd need one of:
- **Publish the skill** so others can install it into their own Claude Code.
- **Wrap it in an app** — a web app where students paste a problem and get a
  tutored walkthrough back. The skill's `SKILL.md` becomes the system prompt /
  behavior spec for that app's Claude API calls.

The app route is the real "around the world" path. The skill is the brain;
the app would be the front door. This repo is structured so it can grow into
that later — the skill is self-contained and portable.

## Reference library

`references/` holds a comprehensive, PhD-level reference file for **every course
in the KSU B.S. Mechanical Engineering curriculum** — ~12,000 lines covering
calculus through controls. Each file has definitions, theorems, full formula
sets, derivations, solution procedures, worked-example patterns, and common
pitfalls, built from open-access textbooks (OpenStax, LibreTexts, MIT OCW,
Mechanics Map, Felippa's IFEM, Lienhard's *A Heat Transfer Textbook*, and more).

The skill reads the matching reference file before solving a problem, so answers
come from verified material rather than memory. `SKILL.md` has the full topic →
file routing table.

> Note: the deep references were assembled by research agents mining open
> textbooks. Where a source PDF wouldn't fetch cleanly, content was written from
> standard engineering canon and cross-checked against sources that did load.
> It's stable, well-established undergraduate material — but if you hit anything
> that looks off, it's worth verifying against your course textbook.

## License

Mechanical Engineering Student Skill © 2026 Cooper Lockridge, licensed under
[CC BY-NC-SA 4.0](LICENSE) (Attribution–NonCommercial–ShareAlike).

The reference files were synthesized from open-access textbooks — OpenStax,
LibreTexts, MIT OpenCourseWare, Mechanics Map, Felippa's IFEM, Lienhard's
*A Heat Transfer Textbook*, and others. Each reference file lists its sources in
an "Open-source sources used" section. Because several of those sources are
themselves NonCommercial / ShareAlike, this repo carries a compatible license.
Free to use and adapt for non-commercial, educational purposes with attribution.

## Structure

```
mech-engineer-student/
├── README.md
└── .claude/skills/mech-engineer-student/
    ├── SKILL.md                      # the skill — behavior, modes, rigor protocol, routing
    └── references/                   # 23 PhD-level course references
        ├── formula-reference.md      # quick formulas, all domains
        ├── calculus.md
        ├── differential-equations.md
        ├── probability-statistics.md
        ├── numerical-methods.md
        ├── physics-mechanics.md
        ├── physics-em.md
        ├── chemistry.md
        ├── statics.md
        ├── dynamics.md
        ├── strength-of-materials.md
        ├── machine-design.md
        ├── thermodynamics.md
        ├── fluid-mechanics.md
        ├── heat-transfer.md
        ├── materials-science.md
        ├── manufacturing.md
        ├── cae-fea.md
        ├── engineering-graphics.md
        ├── vibrations.md
        ├── machine-kinematics.md
        ├── controls.md
        └── circuits.md
```
