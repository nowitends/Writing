# Lecture Notes — General Agent Working Rules

## 1. Purpose

This document defines the general rules for working with lecture-note projects inside this repository.

The repository is used to develop academic lecture notes in LaTeX. The final output of each project is a compiled PDF document.

The work is performed interactively with AI agents. The human author gives small, precise instructions. The agent modifies the relevant source files, compiles the document, checks the result, and reports what was changed.

The most important principle is:

```text
small change → compilation → PDF review → next small change
```

The agent should not try to complete or rewrite whole lecture courses unless explicitly instructed to do so.

---

## 2. Main projects

The repository contains five LaTeX lecture-note projects:

```text
Lectures_notes_old_school/
├── mathematical_lectures/
│   ├── basic_mathematics/
│   ├── probabilistic_methods/
│   └── general_notes_experiments/
└── physics_lectures/
    ├── physics_basics/
    └── general_notes_experiments/
```

The projects are:

1. `mathematical_lectures/basic_mathematics`
   General mathematics lecture notes.

2. `mathematical_lectures/probabilistic_methods`
   Probabilistic methods lecture notes.

3. `physics_lectures/physics_basics`
   General physics lecture notes.

4. `mathematical_lectures/general_notes_experiments`
   Independent mathematical notes, sketches, and larger exploratory ideas.

5. `physics_lectures/general_notes_experiments`
   Independent physics notes, models, thought experiments, and larger exploratory ideas.

Each project should be treated as a separate LaTeX project.

The two `general_notes_experiments` projects are incubators. They are meant for
loose thoughts, AI-assisted discussions, exploratory notes, and self-contained
larger ideas that may later be moved into a formal course project.

---

## 3. Language policy

All visible teaching materials should be written in **English**, unless the human author explicitly requests another language.

This includes:

* chapter titles,
* section titles,
* definitions,
* examples,
* theorems,
* explanations,
* tables,
* figure captions,
* PDF-visible notes and comments.

Polish may be used only for internal repository notes, temporary TODO comments, or when explicitly requested.

---

## 4. Document class and page layout

All lecture-note projects should use the LaTeX `report` class.

Default setup:

```latex
\documentclass[11pt,a4paper]{report}
```

The page margins should be 2.5 cm:

```latex
\usepackage[a4paper,margin=2.5cm]{geometry}
```

The standard compilation engine is `pdflatex`, unless the project later explicitly requires another engine.

Preferred compilation command:

```bash
pdflatex main.tex
pdflatex main.tex
```

The second run is needed for references, the table of contents, numbering, and cross-references.

---

## 5. Modular LaTeX principle

The lecture notes must not be written as one huge monolithic LaTeX file.

Each project should have a clear `main.tex`, but the main file should only assemble the document.

The main file should:

1. declare the document class,
2. load the preamble,
3. load macros,
4. load visual styles,
5. start the document,
6. include the table of contents,
7. include chapter files,
8. end the document.

The actual teaching content should be stored in smaller files.

A typical structure is:

```text
CourseFolder/
├── main.tex
├── preamble.tex
├── macros.tex
├── styles.tex
├── chapters/
│   ├── topic_one/
│   │   ├── first_section.tex
│   │   └── second_section.tex
│   ├── topic_two/
│   │   └── first_section.tex
│   ├── chapter_topic_one.tex
│   └── chapter_topic_two.tex
├── figures/
└── output/
```

The `chapters` directory contains:
- A subdirectory for each topic, containing the `.tex` files for the sections of that chapter.
- A `chapter_*.tex` file for each chapter, which acts as a "table of contents" for that chapter, including the section files.

In the `general_notes_experiments` projects, a `chapter_*.tex` file usually
represents one independent note or experiment rather than a chapter in a linear
course. The same modular structure is kept so a mature note can later be copied
or adapted into a formal lecture-note project.

The goal is to make each file readable, reviewable, and easy to edit.

A single source file should usually correspond to a chapter, section, or substantial subsection. It does not need to be extremely small, but it should not become so large that it is difficult to inspect.

---

## 6. Repository organization rules

Shared technical files used by all lecture-note projects live in:

```text
shared/
├── preamble.tex
├── macros.tex
└── styles.tex
```

Project-local `preamble.tex`, `macros.tex`, and `styles.tex` files should remain
thin wrappers that load the corresponding shared files. Do not duplicate shared
LaTeX setup separately in each project unless the human author explicitly asks
for a project-specific exception.

Each lecture-note project should keep its course-specific files in predictable
locations:

```text
CourseFolder/
├── chapters/
├── figures/
├── problems/
├── main.tex
├── preamble.tex
├── macros.tex
├── styles.tex
└── titlepage.tex
```

Not every project must have every topic folder immediately, but when a category
is used it should be placed in the appropriate top-level folder.

For `general_notes_experiments` projects, new ideas should normally be added as
new independent files:

```text
chapters/chapter_001_short_descriptive_name.tex
chapters/chapter_002_another_independent_idea.tex
```

Do not force experimental notes into a single growing chapter file. Keep each
substantial idea movable, reviewable, and easy to promote into a formal course
later.

### 6.1 Figures and diagrams

Lecture-note graphics should be written as TikZ source whenever practical.
Prefer repository-native TikZ files over external bitmap images for mathematical
and physics diagrams, plots, geometric sketches, vectors, probability trees, and
schematic illustrations.

TikZ figures should be stored in the relevant project's `figures/` directory,
inside a topic-specific subdirectory:

```text
figures/linear_algebra/matrix_transformation.tex
figures/calculus/tangent_line.tex
figures/combinatorics/tree_counting.tex
figures/kinematics/position_time_graph.tex
```

Use lowercase `snake_case` names. Avoid vague names such as `diagram.tex`,
`figure1.tex`, or `new_picture.tex`.

Figures should be included from lecture content files by inputting the TikZ
source from the project root, for example:

```latex
\input{figures/kinematics/position_time_graph}
```

External image formats such as `.png`, `.jpg`, or `.svg` should be used only
when TikZ is not a good fit, for example for scanned source material or an
externally produced illustration explicitly requested by the human author.

### 6.2 Problems

Problem sets should live in the relevant project's `problems/` directory. Use
topic-specific subdirectories when the number of files grows:

```text
problems/algebra/
problems/calculus/
problems/geometry/
```

Problem files should use meaningful lowercase `snake_case` names, optionally
prefixed with a two-digit order number.

### 6.3 Generated files

Compiled PDFs may be committed when they are the intended output of a project.
Temporary LaTeX build artifacts such as `.aux`, `.log`, `.out`, `.toc`, `.fls`,
`.fdb_latexmk`, and `.synctex.gz` should not be committed.

GitHub Actions includes a workflow that rebuilds lecture `main.pdf` files after
pushes that change LaTeX sources, shared TeX setup, or project build scripts.
The workflow commits updated PDFs only when the rebuilt files differ from the
committed versions.

---

## 7. Main-file rule

Every project must have a `main.tex`.

A typical `main.tex` should look like this:

```latex
\documentclass[11pt,a4paper]{report}

\input{preamble}
\input{macros}
\input{styles}

\begin{document}

\tableofcontents

\include{chapters/chapter_topic_one}
\include{chapters/chapter_topic_two}

\end{document}
```

Each `chapter_*.tex` file may then include smaller section files from its dedicated folder:

```latex
% In chapters/chapter_linear_algebra.tex
\chapter{Linear Algebra}

\input{chapters/linear_algebra/vectors}
\input{chapters/linear_algebra/matrices}
\input{chapters/linear_algebra/systems_of_linear_equations}
```

The agent should normally work on the smallest relevant file.

---

## 8. Editing discipline

When the human author asks for a change, the agent should first classify the request as one of the following:

1. **Local change**
   A change affecting one section, example, table, figure, or paragraph.

2. **Structural change**
   A change affecting chapter order, included files, project structure, or the `main.tex`.

3. **Document-wide style change**
   A change affecting shared styles, macros, theorem boxes, table formatting, layout, or typography.

For a local change, edit only the relevant content file.

For a structural change, edit the relevant `chapter.tex`, `main.tex`, or folder structure.

For a document-wide style change, edit shared files such as:

```text
preamble.tex
macros.tex
styles.tex
```

For visual styles shared by all lecture-note projects, edit:

```text
shared/styles.tex
```

The project-local `styles.tex` files should remain thin wrappers that load the
shared style file.

For mathematical notation macros shared by all lecture-note projects, edit:

```text
shared/macros.tex
```

The project-local `macros.tex` files should remain thin wrappers that load the
shared macros file.

For LaTeX package setup shared by all lecture-note projects, edit:

```text
shared/preamble.tex
```

The project-local `preamble.tex` files should remain thin wrappers that load the
shared preamble file.

The agent should not mix these levels unless necessary.

For example, if the task is:

```text
Add two examples explaining acceleration in one-dimensional motion.
```

then the agent should probably edit only:

```text
chapters/kinematics/one_dimensional_motion.tex
```

If the task is:

```text
Make all definition boxes more colorful.
```

then the agent should probably edit:

```text
styles.tex
```

and then recompile.

---

## 9. Incremental work

The work should proceed through small, controlled steps.

Preferred workflow:

```text
inspect project → identify target file → edit small part → compile → report result
```

The agent should not rewrite unrelated files.

The agent should not reorganize the project unless explicitly asked.

The agent should not generate large amounts of new lecture content unless explicitly asked.

Good tasks:

```text
Add a short subsection about matrix multiplication.
```

```text
Add a table comparing velocity and acceleration.
```

```text
Improve the explanation of conditional probability.
```

```text
Add a TikZ diagram for one-dimensional motion.
```

```text
Make theorem boxes visually clearer.
```

Bad tasks, unless explicitly confirmed:

```text
Rewrite the whole document.
```

```text
Create the full course content at once.
```

```text
Change all chapters without asking.
```

---

## 10. Compilation rule

After every substantial change, the agent should compile the document.

Default command:

```bash
pdflatex main.tex
pdflatex main.tex
```

If a project has a build script, the agent may use it instead, for example:

```bash
latexmk -pdf main.tex
```

or:

```bash
./build.sh
```

but only if the project already uses such a workflow.

Even though GitHub Actions can rebuild and commit PDFs after a push, the agent
should still compile locally after substantial source changes whenever possible.
Local compilation catches LaTeX errors before the changes reach GitHub.

The agent must check the compilation log.

The agent should not claim that compilation succeeded unless it actually ran the compilation command and confirmed success.

---

## 11. Reporting rule

After editing, the agent should report briefly:

```text
Changed:
- Added ...
- Updated ...
- Modified ...

Compilation:
- pdflatex completed successfully.
- Output PDF: main.pdf
```

If compilation fails, the agent should report:

```text
Changed:
- ...

Compilation:
- pdflatex failed.
- Error: ...
- Suggested fix: ...
```

If the cause is clear, the agent should fix it and recompile.

---

## 12. Mathematical writing style

The notes should be written in a clear academic style.

The style should be:

* precise,
* pedagogical,
* structured,
* readable,
* mathematically correct,
* suitable for students.

The agent should avoid vague statements such as:

```text
It is obvious that...
```

Prefer explanatory reasoning.

For example, instead of:

```text
Clearly, the function is continuous.
```

write:

```text
The function is continuous because it is a polynomial, and every polynomial is continuous on the whole real line.
```

Definitions, formulas, examples, and interpretations should be connected by explanatory text.

---

## 13. Mathematical notation

Mathematical notation should be written using real LaTeX mathematics.

Inline mathematics:

```latex
Let \( f : \mathbb{R} \to \mathbb{R} \) be a function.
```

Display mathematics:

```latex
\[
\lim_{x \to a} f(x) = L.
\]
```

Use standard notation consistently:

```latex
\mathbb{R}
\mathbb{N}
\mathbb{Z}
\varepsilon
\delta
\forall
\exists
\Rightarrow
\iff
```

Do not use fake mathematical notation in plain text when proper LaTeX notation is needed.

---

## 14. Visual style

The PDF should not look like raw, plain LaTeX output.

A moderate visual style is encouraged:

* colored definition boxes,
* example boxes,
* theorem boxes,
* remark boxes,
* clean tables,
* simple diagrams,
* highlighted summaries.

Color should improve readability, not decorate the document excessively.

Recommended packages include:

```latex
\usepackage{xcolor}
\usepackage{tcolorbox}
\usepackage{booktabs}
\usepackage{array}
\usepackage{tikz}
\usepackage{graphicx}
\usepackage{hyperref}
```

Tables should preferably use `booktabs`.

Avoid heavy table borders unless explicitly requested.

---

## 15. Naming conventions

Use English names for folders and files.

Use lowercase `snake_case`.

Good examples:

```text
linear_algebra
analytic_geometry
calculus
mathematical_preliminaries
one_dimensional_motion
systems_of_linear_equations
electric_charge_and_field
```

Avoid Polish folder names in the LaTeX project structure unless explicitly requested.

Avoid spaces in file names.

Avoid vague names such as:

```text
part1.tex
new_file.tex
notes.tex
stuff.tex
```

Prefer meaningful file names.

---

## 16. Course-specific writing expectations

### 16.1 Mathematics

The mathematics notes should be written as pure mathematical lecture notes.

They should emphasize:

* definitions,
* examples,
* theorem statements,
* proofs where appropriate,
* intuitive explanations,
* connections between concepts,
* precise notation.

Avoid unnecessary physics motivation unless explicitly requested.

---

### 16.2 Probabilistic Methods

The probabilistic methods notes should combine mathematical precision with interpretation.

They should emphasize:

* probability spaces,
* events,
* conditional probability,
* independence,
* random variables,
* distributions,
* expectation,
* variance,
* limit theorems,
* probabilistic modelling,
* examples and interpretations.

The notes should explain not only formulas, but also what the formulas mean.

---

### 16.3 Physics

The physics notes should combine physical meaning with mathematical formulation.

They should emphasize:

* physical interpretation,
* mathematical models,
* units,
* dimensional analysis,
* examples,
* diagrams,
* connection between formulas and phenomena.

Equations should not be presented as isolated formulas. They should be explained in terms of physical meaning.

---

## 17. Core rule

This repository is developed interactively.

The agent should work on small, meaningful LaTeX files rather than huge monolithic documents.

Every course has a `main.tex` file that assembles the document from chapters and smaller section files.

Most changes should be local, followed by compilation and PDF review.

Large document-wide changes are allowed only when the human author explicitly requests them.

---

## 18. Useful links

Useful external references may be consulted when improving the technical quality
of the lecture notes.

TikZ examples and documentation:

```text
https://tikz.dev/
```

Use this reference when creating or improving TikZ diagrams, checking TikZ
syntax, or looking for clean examples of diagrams that can be adapted to the
course style.
