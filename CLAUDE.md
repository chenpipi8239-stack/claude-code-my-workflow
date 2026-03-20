# CLAUDE.MD -- Academic Project Development with Claude Code

**Project:** Quantitative Spatial Equilibrium and the Data Economy
**Institution:** Tsinghua University
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- Beamer `.tex` is authoritative; Quarto `.qmd` derives from it
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong -> right` to MEMORY.md

---

## Folder Structure

```
SpatialDataEcon/
├── CLAUDE.MD                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers (user-supplied theme)
├── Slides/                      # Beamer .tex files
├── Quarto/                      # RevealJS .qmd files + theme
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts (R/, Python/, Julia/)
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/      # Papers and existing slides
```

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# R scripts
Rscript scripts/R/filename.R

# Python scripts
python scripts/Python/filename.py

# Julia scripts
julia scripts/Julia/filename.jl

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh LectureN

# Quality score
python scripts/quality_score.py Quarto/file.qmd
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [LectureN]` | Render Quarto + sync to docs/ |
| `/extract-tikz [LectureN]` | TikZ -> PDF -> SVG |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/review-r [file]` | R code quality review |
| `/qa-quarto [LectureN]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer -> Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/create-lecture` | Full lecture creation |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/review-paper [file]` | Manuscript review |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/learn [skill-name]` | Extract discovery into persistent skill |
| `/context-status` | Show session health + context usage |
| `/deep-audit` | Repository-wide consistency audit |

---

## Beamer Custom Environments

Pending: user will supply custom Beamer preamble with theme definitions.
Update this table once `Preambles/header.tex` is populated.

| Environment | Effect | Use Case |
|-------------|--------|----------|
| *(to be filled)* | | |

## Quarto CSS Classes

| Class | Effect | Use Case |
|-------|--------|----------|
| `.tsinghuapurple` | Tsinghua purple text | Primary emphasis |
| `.tsinghugold` | Gold text | Secondary emphasis |
| `.tsinghured` | Red text | Highlights, alerts |
| `.keybox` | Gold-bordered box | Key results, takeaways |
| `.methodbox` | Purple-bordered box | Methods, estimators |
| `.highlightbox` | Red-accented box | Important highlights |
| `.assumptionbox` | Gold full-border box | Formal assumptions |
| `.resultbox` | Gold filled box | Main results |
| `.eqbox` | Light purple background | Equation display |
| `.softbox` | Light gold italic | Soft commentary |
| `.quotebox` | Quote with decorative mark | Block quotes |
| `.positive` | Green bold | Good/identified |
| `.negative` | Red bold | Bad/problematic |
| `.neutral` | Gray | Reference/context |
| `.hi` | Purple bold | Inline highlight |
| `.smaller` | 85% font | Dense content slides |
| `.smallest` | 80% font | Very dense content |
| `.compact` | Reduced spacing | Tight layouts |

---

## Current Project State

| Lecture | Beamer | Quarto | Key Content |
|---------|--------|--------|-------------|
| 1: Introduction & Motivation | `Lecture01_Intro.tex` | -- | Course overview, spatial + data economy motivation |
| 2: Foundations of Spatial Equilibrium | `Lecture02_Spatial_Eq.tex` | -- | Rosen-Roback, compensating differentials |
| 3: Quantitative Spatial Models | `Lecture03_QSM.tex` | -- | Gravity, EK, CES/Frechet, exact hat algebra |
| 4: Geography of Development | `Lecture04_Geography_Dev.tex` | -- | DNR (2018), dynamic spatial model |
| 5: Trade & Labor Dynamics I | `Lecture05_Trade_Labor_I.tex` | -- | CDP (2019), theory of dynamic spatial GE |
| 6: Trade & Labor Dynamics II | `Lecture06_Trade_Labor_II.tex` | -- | CDP (2019), computation & China trade shock |
| 7: Mechanics of Spatial Growth | `Lecture07_Spatial_Growth.tex` | -- | CCPX (2025), innovation diffusion |
| 8: Computational Methods | `Lecture08_Computation.tex` | -- | Fixed-point, Newton, hat algebra implementation |
| 9: Economics of Data: Nonrivalry | `Lecture09_Data_Nonrivalry.tex` | -- | JT (2020), data as factor of production |
| 10: Multi-Purpose Data & Growth | `Lecture10_Data_Growth.tex` | -- | Cong et al., endogenous growth with data |
| 11: Data Markets & Policy | `Lecture11_Data_Markets.tex` | -- | WJG (2023), China data market GE model |
| 12: Unified Framework I: Theory | `Lecture12_Unified_Theory.tex` | -- | Spatial equilibrium + data nonrivalry |
| 13: Unified Framework II: Computation | `Lecture13_Unified_Computation.tex` | -- | Solving unified model, counterfactuals |
| 14: Frontiers & Research Agenda | `Lecture14_Frontiers.tex` | -- | Privacy, digital trade, AI/data, student work |
