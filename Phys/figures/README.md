# Physics figures

This directory stores figures used by the physics lecture notes.

Recommended structure:

```text
figures/
├── tikz/   # TikZ source files included or compiled from LaTeX
├── pdf/    # vector PDF figures generated from TikZ or external tools
├── svg/    # editable vector graphics
└── png/    # raster exports, screenshots, or bitmap illustrations
```

Each format directory is divided by physics topic, for example `kinematics`, `dynamics`, or `electromagnetism`.

Suggested naming convention:

```text
<topic>_<short_description>.<extension>
```

Examples:

```text
kinematics_position_time_graph.tex
kinematics_projectile_motion.pdf
dynamics_free_body_diagram.svg
```

Prefer vector formats (`.tex`, `.pdf`, `.svg`) for lecture notes. Use `.png` only when a raster image is necessary.
