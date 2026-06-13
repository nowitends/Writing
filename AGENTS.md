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

The repository contains nine LaTeX lecture-note projects:

```text
.
├── mathematical_lectures/
│   ├── basic_mathematics/
│   ├── probabilistic_methods/
│   └── general_notes_experiments/
└── physics_lectures/
    ├── classical_field_theory_I/
    ├── classical_field_theory_II/
    ├── physics_basics/
    ├── praktyczna_mechanika_kwantowa/
    ├── quantum_field_theory/
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

6. `physics_lectures/classical_field_theory_I`
   Classical Field Theory I lecture notes.

7. `physics_lectures/classical_field_theory_II`
   Classical Field Theory II lecture notes.

8. `physics_lectures/praktyczna_mechanika_kwantowa`
   Practical Quantum Mechanics lecture notes, written in Polish by explicit author request.

9. `physics_lectures/quantum_field_theory`
   Quantum Field Theory lecture notes, complementary to Classical Field Theory I--II.

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
