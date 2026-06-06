# Lectures Notes Old School!

This repository contains three separate LaTeX lecture-note projects.

## Projects

```text
mathematical_lectures/basic_mathematics
mathematical_lectures/probabilistic_methods
physics_lectures/physics_basics
```

Each project has its own `main.tex` source file and compiled `main.pdf` output.

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
