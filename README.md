# Exam template (LaTeX `exam` class)

One set of exercise files, four PDFs:

| File                       | What it is                                      |
|----------------------------|-------------------------------------------------|
| `exam.tex`                 | the exam to print: empty answer boxes           |
| `exam-solutions.tex`       | the same exam with solutions                    |
| `collection.tex`           | all exercises for students, no boxes            |
| `collection-solutions.tex` | all exercises with solutions                    |

Build everything with `latexmk` (LuaLaTeX, set in `.latexmkrc`), or one file with
`latexmk exam.tex`.

## How it works

- Each exercise is a fragment in a topic folder (`centrality/simple-complete.tex`): no
  `\documentclass`, just `\titledquestion`, `parts` and `solutionorbox`. The exam and the
  collection `\input` the same files, so a fixed typo is fixed everywhere.
- **With or without solutions** is only the `answers` option of the `exam` class. Each pair
  of root files differs in that option alone and shares a body: `exam-body.tex` and
  `collection-body.tex`.
- `solutionorbox[9cm]` is an empty 9 cm box in the exam and a shaded solution with
  `answers`. In the collection without solutions it prints nothing (see `collection-body.tex`),
  so students get the exercises without empty boxes.
- Box heights are written as `\boxheight{9}`, which means 9 cm. In the exam, `exam-body.tex`
  makes them shares of the page's free space instead, so the boxes fill their pages. Comment
  out that line for fixed heights.
- `\exambreak` in an exercise starts a new page in the printed exam only.
- Points: `\part[4]`, or `\titledquestion{Title}[10]` for a question without parts. The grade
  table on the exam's title page adds them up.
- Course name, lecturer and term live in `preamble.tex` (shared packages and the solution look).
- The collection's sections are `collection-sections/<topic>.tex`. A subset (e.g. a midterm
  collection) is a root file that defines `\collectionsections`, as the comment in
  `collection-body.tex` shows.

LaTeX warns "Label `question@1' multiply defined" for the collection: question numbers restart
in every section. You can ignore it.

## Working with an AI agent

`AGENTS.md` tells coding agents (Codex, Claude Code, …) how this repository works: how to build
and check, where exercises go, what stays your decision. `CLAUDE.md` only imports it, so Claude
Code reads the same rules. Open the folder in the agent and ask, e.g., "add an exercise on X to
centrality, with solution, and put it into the exam".

## The example exercises

`centrality/simple-complete.tex` (Katz-Bonacich centrality) and `connectedness/sci2.tex` (the
Social Connectedness Index) come from Fabian Greimel's course *Networks in Economics and
Finance* (University of Vienna). Replace them with your own; keep them if they are useful.

## Licence

Exercises: CC BY 4.0. Template files: MIT. See `LICENSE`.
