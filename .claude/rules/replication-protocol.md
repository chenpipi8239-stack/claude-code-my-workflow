---
paths:
  - "scripts/**/*.R"
  - "Figures/**/*.R"
---

# Replication-First Protocol

**Core principle:** Replicate original results to the dot BEFORE extending.

---

## Phase 1: Inventory & Baseline

Before writing any R code:

- [ ] Read the paper's replication README
- [ ] Inventory replication package: language, data files, scripts, outputs
- [ ] Record gold standard numbers from the paper:

```markdown
## Replication Targets: [Paper Author (Year)]

| Target | Table/Figure | Value | SE/CI | Notes |
|--------|-------------|-------|-------|-------|
| Main ATT | Table 2, Col 3 | -1.632 | (0.584) | Primary specification |
```

- [ ] Store targets in `quality_reports/LectureNN_replication_targets.md` or as RDS

---

## Phase 2: Translate & Execute

- [ ] Follow `r-code-conventions.md` for all R coding standards
- [ ] Translate line-by-line initially -- don't "improve" during replication
- [ ] Match original specification exactly (covariates, sample, clustering, SE computation)
- [ ] Save all intermediate results as RDS

### Stata to R Translation Pitfalls

| Stata | R | Trap |
|-------|---|------|
| `reg y x, cluster(id)` | `feols(y ~ x, cluster = ~id)` | Stata clusters df-adjust differently from some R packages |
| `areg y x, absorb(id)` | `feols(y ~ x \| id)` | Check demeaning method matches |
| `ppmlhdfe y x, absorb(id)` | `fixest::fepois(y ~ x \| id)` | Check convergence flag; zero handling may differ |
| `spmat` commands | `Matrix` + `spdep` | Spatial weight matrix construction conventions differ |
| `bootstrap, reps(999)` | Depends on method | Match seed, reps, and bootstrap type exactly |
| `eststo`/`esttab` | `modelsummary` | Column alignment and significance star conventions |

### Python to R Translation Pitfalls

| Python | R | Trap |
|--------|---|------|
| `geopandas.read_file()` | `sf::st_read()` | CRS handling differs; always verify EPSG |
| `scipy.optimize.fixed_point` | Custom iteration loop | Convergence criteria and damping factors may differ |
| `numpy` broadcasting | R vectorization | Matrix dimension conventions (row-major vs column-major) |
| `pandas` 0-indexed | R 1-indexed | Off-by-one errors in region indexing |

### Julia to R Translation Pitfalls

| Julia | R | Trap |
|-------|---|------|
| `Optim.jl` solvers | `optim()` / `nloptr` | Default algorithms differ; specify explicitly |
| `SparseArrays` | `Matrix::sparseMatrix` | Constructor API differs significantly |
| `DifferentialEquations.jl` | `deSolve` | Solver defaults and tolerances differ |
| `Threads.@threads` parallelism | `parallel` / `future` | Race conditions in spatial solver updates |

---

## Phase 3: Verify Match

### Tolerance Thresholds

| Type | Tolerance | Rationale |
|------|-----------|-----------|
| Integers (N, counts) | Exact match | No reason for any difference |
| Point estimates | < 0.01 | Rounding in paper display |
| Standard errors | < 0.05 | Bootstrap/clustering variation |
| P-values | Same significance level | Exact p may differ slightly |
| Percentages | < 0.1pp | Display rounding |
| Spatial equilibrium wages | < 1e-8 | Fixed-point convergence |
| Trade shares (column sums) | < 1e-10 | Must sum to exactly 1 |
| Welfare (% equiv. variation) | < 0.01pp | Numerical precision |
| Migration flows (row sums) | < 1e-8 | Stochastic matrix rows sum to 1 |
| Population distribution | < 1e-8 | Must sum to total population |

### If Mismatch

**Do NOT proceed to extensions.** Isolate which step introduces the difference, check common causes (sample size, SE computation, default options, variable definitions), and document the investigation even if unresolved.

### Replication Report

Save to `quality_reports/LectureNN_replication_report.md`:

```markdown
# Replication Report: [Paper Author (Year)]
**Date:** [YYYY-MM-DD]
**Original language:** [Stata/R/etc.]
**R translation:** [script path]

## Summary
- **Targets checked / Passed / Failed:** N / M / K
- **Overall:** [REPLICATED / PARTIAL / FAILED]

## Results Comparison

| Target | Paper | Ours | Diff | Status |
|--------|-------|------|------|--------|

## Discrepancies (if any)
- **Target:** X | **Investigation:** ... | **Resolution:** ...

## Environment
- R version, key packages (with versions), data source
```

---

## Phase 4: Only Then Extend

After replication is verified (all targets PASS):

- [ ] Commit replication script: "Replicate [Paper] Table X -- all targets match"
- [ ] Now extend with course-specific modifications (different estimators, new figures, etc.)
- [ ] Each extension builds on the verified baseline

---

## Spatial Economics Replication Pitfalls

| Issue | Example | Resolution |
|-------|---------|------------|
| Region aggregation | Paper uses 50 states; data has FIPS counties | Verify exact region definition before coding |
| Trade flow zeros | Zeros common in bilateral trade | Use PPML; document zero handling explicitly |
| Equilibrium solver non-convergence | Fixed-point iteration diverges | Try dampening, Anderson mixing, or Newton method |
| Calibration targets | Paper calibrates to year X; data version differs | Match exact data vintage and document |
| Welfare sensitivity to elasticities | Small $\theta$ or $\sigma$ changes → large welfare effects | Report sensitivity analysis alongside main results |
| Hat algebra baseline | Counterfactual requires exact base period match | Verify base equilibrium reproduces observed data before running counterfactuals |
