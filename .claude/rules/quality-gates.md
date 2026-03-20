---
paths:
  - "Slides/**/*.tex"
  - "Quarto/**/*.qmd"
  - "scripts/**/*.R"
---

# Quality Gates & Scoring Rubrics

## Thresholds

- **80/100 = Commit** -- good enough to save
- **90/100 = PR** -- ready for deployment
- **95/100 = Excellence** -- aspirational

## Quarto Slides (.qmd)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Compilation failure | -100 |
| Critical | Equation overflow | -20 |
| Critical | Broken citation | -15 |
| Critical | Typo in equation | -10 |
| Major | Text overflow | -5 |
| Major | TikZ label overlap | -5 |
| Major | Notation inconsistency | -3 |
| Minor | Font size reduction | -1 per slide |
| Minor | Long lines (>100 chars) | -1 (EXCEPT documented math formulas) |

## R Scripts (.R)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors | -100 |
| Critical | Domain-specific bugs | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing set.seed() | -10 |
| Major | Missing figure generation | -5 |
| Critical | Trade shares don't sum to 1 | -30 |
| Critical | Equilibrium solver non-convergence undocumented | -20 |
| Major | Missing spatial weight matrix validation | -10 |
| Major | Counterfactual without base-period verification | -10 |

## Beamer Slides (.tex)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | XeLaTeX compilation failure | -100 |
| Critical | Undefined citation | -15 |
| Critical | Overfull hbox > 10pt | -10 |

## Enforcement

- **Score < 80:** Block commit. List blocking issues.
- **Score < 90:** Allow commit, warn. List recommendations.
- User can override with justification.

## Quality Reports

Generated **only at merge time**. Use `templates/quality-report.md` for format.
Save to `quality_reports/merges/YYYY-MM-DD_[branch-name].md`.

## Tolerance Thresholds (Spatial/Data Economics)

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| Equilibrium wages/prices | 1e-8 | Fixed-point convergence standard |
| Trade shares (column sums) | 1e-10 | Stochastic consistency |
| Welfare (% equiv. variation) | 0.01pp | Display precision |
| Population distribution | 1e-8 | Conservation law |
| Gravity coefficients | 1e-4 | PPML estimation precision |
| Migration transition probs | 1e-8 | Row stochastic consistency |
| Hat algebra counterfactuals | 1e-6 | Relative to base equilibrium |
| Coverage rates (MC) | +/- 0.02 | With B=1000 reps |
