---
paths:
  - "Slides/**/*.tex"
  - "Quarto/**/*.qmd"
---

# Beamer → Quarto Auto-Sync Rule (MANDATORY)

**Every edit to a Beamer `.tex` file MUST be immediately synced to the corresponding Quarto `.qmd` file — automatically, without the user asking.** This is non-negotiable.

## The Rule

When you modify a Beamer `.tex` file, you MUST also apply the equivalent change to the Quarto `.qmd` (if it exists) **in the same task**, before reporting completion. Do NOT wait to be asked. Do NOT just "flag the drift." Just do it.

## Lecture Mapping

| Lecture | Beamer | Quarto |
|---------|--------|--------|
| 1 | `Slides/Lecture01_Intro.tex` | `Quarto/Lecture1_Intro.qmd` |
| 2 | `Slides/Lecture02_Spatial_Eq.tex` | `Quarto/Lecture2_Spatial_Eq.qmd` |
| 3 | `Slides/Lecture03_QSM.tex` | `Quarto/Lecture3_QSM.qmd` |
| 4 | `Slides/Lecture04_Geography_Dev.tex` | `Quarto/Lecture4_Geography_Dev.qmd` |
| 5 | `Slides/Lecture05_Trade_Labor_I.tex` | `Quarto/Lecture5_Trade_Labor_I.qmd` |
| 6 | `Slides/Lecture06_Trade_Labor_II.tex` | `Quarto/Lecture6_Trade_Labor_II.qmd` |
| 7 | `Slides/Lecture07_Spatial_Growth.tex` | `Quarto/Lecture7_Spatial_Growth.qmd` |
| 8 | `Slides/Lecture08_Computation.tex` | `Quarto/Lecture8_Computation.qmd` |
| 9 | `Slides/Lecture09_Data_Nonrivalry.tex` | `Quarto/Lecture9_Data_Nonrivalry.qmd` |
| 10 | `Slides/Lecture10_Data_Growth.tex` | `Quarto/Lecture10_Data_Growth.qmd` |
| 11 | `Slides/Lecture11_Data_Markets.tex` | `Quarto/Lecture11_Data_Markets.qmd` |
| 12 | `Slides/Lecture12_Unified_Theory.tex` | `Quarto/Lecture12_Unified_Theory.qmd` |
| 13 | `Slides/Lecture13_Unified_Computation.tex` | `Quarto/Lecture13_Unified_Computation.qmd` |
| 14 | `Slides/Lecture14_Frontiers.tex` | `Quarto/Lecture14_Frontiers.qmd` |
<!-- Add rows as you create lectures -->

## Workflow (Every Time)

1. Apply fix to Beamer `.tex`
2. **Immediately** apply equivalent fix to Quarto `.qmd`
3. Compile Beamer (3-pass xelatex)
4. Render Quarto (`./scripts/sync_to_docs.sh LectureN`)
5. Only then report task complete

## LaTeX → Quarto Translation Reference

| Beamer | Quarto Equivalent |
| ------ | ----------------- |
| `\muted{text}` | `[text]{style="color: #525252;"}` |
| `\key{text}` | `[**text**]{.tsinghugold}` |
| `\textcolor{positive}{text}` | `[text]{.positive}` |
| `\textcolor{negative}{text}` | `[text]{.negative}` |
| `\item text` | `- text` |
| `\begin{highlightbox}` | `::: {.highlightbox}` |
| `\begin{methodbox}` | `::: {.methodbox}` |
| `$formula$` | `$formula$` (same) |

## When NOT to Sync

- Quarto file doesn't exist yet
- Change is LaTeX-only infrastructure (preamble, theme files)
- Explicitly told to skip Quarto sync

## Enforcement

Before marking any Beamer editing task as complete, check:
> "Did I also update the Quarto file?"

If the answer is no and a Quarto file exists, **you are NOT done.**

## When to Update This Table

After creating a new Quarto translation, add it to the mapping table above.
