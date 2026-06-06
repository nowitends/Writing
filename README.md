# Lectures Notes Old School!

This repository contains three separate LaTeX lecture-note projects.

## Projects

```text
mathematical_lectures/basic_mathematics
mathematical_lectures/probabilistic_methods
physics_lectures/physics_basics
```

Each project has its own `main.tex` source file and compiled `main.pdf` output.

## Related Repositories

These lecture notes are connected with separate problem repositories:

- [dchorazkiewicz/Math_Problems_Repo](https://github.com/dchorazkiewicz/Math_Problems_Repo)
- [dchorazkiewicz/Physics_Problems_Repo](https://github.com/dchorazkiewicz/Physics_Problems_Repo)

Shared visual styling is kept in:

```text
shared/styles.tex
```

The project-local `styles.tex` files load this shared file so that all lecture
notes use the same theorem boxes, colors, and heading styles.

Shared mathematical notation macros are kept in:

```text
shared/macros.tex
```

The project-local `macros.tex` files load this shared file so that symbols such
as `\R`, `\Prob`, `\E`, and `\Var` stay consistent across projects.

Shared LaTeX package setup is kept in:

```text
shared/preamble.tex
```

The project-local `preamble.tex` files load this shared file so package choices,
page layout, hyperlinks, TikZ setup, and typography stay consistent.

## Figures

Course figures should be written as TikZ source whenever practical and stored in
the relevant project's `figures/` directory, preferably inside topic-specific
subdirectories.

## Build

From a project directory, compile with:

```bash
pdflatex main.tex
pdflatex main.tex
```

Some projects also include a local `build.sh` script.

## Repository Tree

`tree.txt` is regenerated automatically by GitHub Actions after pushes that change
repository contents. The workflow commits the updated `tree.txt` only when the
generated file differs from the committed version.
