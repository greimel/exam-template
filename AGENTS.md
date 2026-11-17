# AGENTS.md

Guidance for coding agents (Claude Code, Codex, …) working in this exam repository. The
README explains the setup for people; this file holds the rules an agent must keep.

## Build and check

- `latexmk` builds all four PDFs with LuaLaTeX (`.latexmkrc`); `latexmk exam.tex` one of them.
- After a change, build all four and check the logs for errors (`grep '^!' *.log`) and for
  undefined references. "Label `question@1' multiply defined" in the collection is expected
  (question numbers restart in every section); ignore it.
- Look at the PDFs, not only the logs: a box that spills onto the next page or a page that ends
  half empty shows up only on the page. `pdftoppm -r 50 -png exam.pdf /tmp/exam` renders pages
  to look at; `pdfinfo exam.pdf` gives the page count.

## Structure

- Root files differ only in the `answers` option of `\documentclass`; everything else is in
  `exam-body.tex`, `collection-body.tex` and `preamble.tex`. Never toggle solutions by editing
  the body; never copy the body into a root file.
- Exercises are fragments in topic folders (`centrality/…`): no `\documentclass`, no
  `\begin{document}`, no packages. If an exercise needs a package or macro, add it to
  `preamble.tex` (shared by the exam and the collection), with a comment naming the exercise.
- Paths inside an exercise (figures, `\input`) are relative to the main folder, not to the
  exercise's folder.
- A new exercise goes into its topic folder and into `collection-sections/<topic>.tex`, so the
  collection always holds every exercise; an exam `\input`s a selection in `exam-body.tex`.
- A new topic: a folder, a `collection-sections/<topic>.tex`, and a line in
  `\collectionsections` in `collection-body.tex`.

## Writing exercises

- `\titledquestion{Title}` with `\part[points]`, or `\titledquestion{Title}[points]` without
  parts. Every part has points; the exam's grade table adds them up.
- Every part that students answer has a `solutionorbox` with a complete solution: the same
  file is the exam, the solutions and the collection.
- Box heights as `\boxheight{cm}`, never a bare length; each fragment starts with
  `\providecommand\boxheight[1]{#1cm}`. The exam may redefine `\boxheight` as `\stretch`
  (boxes fill their pages), which needs every exam page to end in `\clearpage` or `\exambreak`.
- A part that needs a fresh page in the printed exam: `\ifdefined\exambreak\exambreak\fi` before
  `\part`.
- The exam prints in black and white: figures must read without colour.

## What stays the lecturer's

Points, the choice of exercises for an exam, and the wording of questions are the lecturer's
decisions. Propose changes to them; do not make them silently. Report the page count of
`exam.pdf` after every change to the exam.
