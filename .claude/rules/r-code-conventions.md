---
paths:
  - "**/*.R"
  - "Figures/**/*.R"
  - "scripts/**/*.R"
---

# R Code Standards

**Standard:** Senior Principal Data Engineer + PhD researcher quality

---

## 1. Reproducibility

- `set.seed()` called ONCE at top (YYYYMMDD format)
- All packages loaded at top via `library()` (not `require()`)
- All paths relative to repository root
- `dir.create(..., recursive = TRUE)` for output directories

## 2. Function Design

- `snake_case` naming, verb-noun pattern
- Roxygen-style documentation
- Default parameters, no magic numbers
- Named return values (lists or tibbles)

## 3. Domain Correctness (Spatial/Data Economics)

- Verify spatial equilibrium solver convergence (iteration residuals below tolerance)
- Gravity regression: use PPML for zeros in trade flows (`fixest::fepois`)
- Trade share construction: columns must sum to 1 for each destination
- Counterfactual welfare: verify ACR sufficient statistics formula used correctly
- Data valuation: nonrival goods require careful aggregation (not simple summation of marginal values)
- Fixed effects in spatial panels: region FE and time FE interact with gravity structure
- Hat algebra: percentage changes must properly cancel calibrated parameters

## 4. Visual Identity

```r
# --- Tsinghua University palette ---
tsinghua_purple <- "#660874"    # Tsinghua purple (primary)
tsinghua_gold   <- "#C89B40"    # Gold accent
tsinghua_red    <- "#A4070B"    # Tsinghua red (secondary)
accent_gray     <- "#525252"
positive_green  <- "#15803d"
negative_red    <- "#b91c1c"
```

### Custom Theme
```r
theme_tsinghua <- function(base_size = 14) {
  theme_minimal(base_size = base_size) +
    theme(
      plot.title = element_text(face = "bold", color = tsinghua_purple),
      plot.subtitle = element_text(color = accent_gray),
      legend.position = "bottom"
    )
}
```

### Figure Dimensions for Beamer
```r
ggsave(filepath, width = 12, height = 5, bg = "transparent")
```

## 5. RDS Data Pattern

**Heavy computations saved as RDS; slide rendering loads pre-computed data.**

```r
saveRDS(result, file.path(out_dir, "descriptive_name.rds"))
```

## 6. Common Pitfalls

| Pitfall | Impact | Prevention |
|---------|--------|------------|
| Missing `bg = "transparent"` | White boxes on slides | Always include in ggsave() |
| Hardcoded paths | Breaks on other machines | Use relative paths |
| `sf::st_read()` silent CRS drop | Spatial joins fail silently | Always check and set CRS explicitly |
| `fixest::fepois` convergence | PPML may not converge with many zeros | Check convergence flag, try `glm.iter` |
| Sparse matrix to dense | Memory explosion for large spatial models | Use `Matrix::sparseMatrix` throughout |
| Trade shares not summing to 1 | Invalid counterfactual | Add assertion: `stopifnot(all(abs(colSums(pi_matrix) - 1) < 1e-10))` |
| `log(0)` in trade flows | NaN propagation | Use `log1p()` or add small epsilon with documentation |

## 7. Line Length & Mathematical Exceptions

**Standard:** Keep lines <= 100 characters.

**Exception: Mathematical Formulas** -- lines may exceed 100 chars **if and only if:**

1. Breaking the line would harm readability of the math (influence functions, matrix ops, finite-difference approximations, formula implementations matching paper equations)
2. An inline comment explains the mathematical operation:
   ```r
   # Sieve projection: inner product of residuals onto basis functions P_k
   alpha_k <- sum(r_i * basis[, k]) / sum(basis[, k]^2)
   ```
3. The line is in a numerically intensive section (simulation loops, estimation routines, inference calculations)

**Quality Gate Impact:**
- Long lines in non-mathematical code: minor penalty (-1 to -2 per line)
- Long lines in documented mathematical sections: no penalty

## 8. Code Quality Checklist

```
[ ] Packages at top via library()
[ ] set.seed() once at top
[ ] All paths relative
[ ] Functions documented (Roxygen)
[ ] Figures: transparent bg, explicit dimensions
[ ] RDS: every computed object saved
[ ] Comments explain WHY not WHAT
```

## 9. Multi-Language Interop

- R is primary; Python and Julia scripts go in `scripts/Python/` and `scripts/Julia/`
- Use `reticulate` for R-Python interop when needed
- Use `JuliaCall` for R-Julia interop when needed
- All cross-language data exchange via CSV or Parquet files
- When translating spatial solvers from Julia/Python to R, explicitly match convergence criteria and solver algorithms
