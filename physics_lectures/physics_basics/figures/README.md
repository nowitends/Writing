# Physics figures

This directory stores figures used by the physics lecture notes. Prefer TikZ
source files for course diagrams whenever practical.

Recommended structure:

```text
figures/
├── kinematics/
├── mathematical_foundations/
├── dynamics/
└── electromagnetism/
```

Each topic directory contains TikZ source files included from the corresponding
chapter or section.

Suggested naming convention:

```text
<short_description>.tex
```

Examples:

```text
kinematics/position_vector.tex
dynamics/free_body_diagram.tex
electromagnetism/electric_field_lines.tex
```

External image formats such as `.png`, `.jpg`, or `.svg` should be used only
when TikZ is not a good fit.
