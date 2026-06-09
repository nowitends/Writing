# Lectures Notes!

This repository contains eight separate LaTeX lecture-note projects.

## Projects

```text
mathematical_lectures/basic_mathematics
mathematical_lectures/probabilistic_methods
mathematical_lectures/general_notes_experiments
physics_lectures/physics_basics
physics_lectures/general_notes_experiments
physics_lectures/classical_field_theory_I
physics_lectures/classical_field_theory_II
physics_lectures/praktyczna_mechanika_kwantowa
```

Each project has its own `main.tex` source file and compiled `main.pdf` output.

The `general_notes_experiments` projects are incubators for independent notes,
loose ideas, AI-assisted discussions, sketches, and larger exploratory drafts.
Each new substantial idea should usually become its own `chapter_*.tex` file so
it can later be moved into a formal lecture-note project if it matures.

## Related Repositories

These lecture notes are connected with separate problem repositories:

- [nowitend/Math_Problems_Repo](https://github.com/nowitends/Math_Problems_Repo)
- [nowitends/Physics_Problems_Repo](https://github.com/nowitends/Physics_Problems_Repo)

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

## Lecture PDF Page

The repository includes a minimal MkDocs site that lists direct links to all
compiled lecture PDFs.

Preview locally:

```bash
python3 -m venv .venv
.venv/bin/python -m pip install -r requirements-docs.txt
.venv/bin/python -m mkdocs serve
```

Deploy to GitHub Pages:

```bash
.venv/bin/python -m mkdocs gh-deploy
```

## Repository Tree

`tree.txt` is regenerated automatically by GitHub Actions after pushes that change
repository contents. The workflow commits the updated `tree.txt` only when the
generated file differs from the committed version.

## PDF Builds

Lecture `main.pdf` files are rebuilt automatically by GitHub Actions after
pushes that change LaTeX sources, shared TeX setup, or project build scripts.
The workflow commits updated PDFs only when the rebuilt files differ from the
committed versions. PDF builds run in a prebuilt TeX Live container instead of
installing LaTeX packages during every workflow run.
