---
paths:
  - "Slides/**/*.tex"
  - "Quarto/**/*.qmd"
  - "scripts/**/*.R"
---

# Course Knowledge Base: Quantitative Spatial Equilibrium and the Data Economy

## Notation Registry

| Rule | Convention | Example | Anti-Pattern |
|------|-----------|---------|-------------|
| Regions | Lowercase $i, j, n$ for regions/locations | $i \in \{1, \ldots, N\}$ | Using $r, s$ inconsistently |
| Region count | $N$ for number of regions | $N$ locations | Using $n$ (conflicts with region index) |
| Trade costs | $d_{ij}$ for iceberg trade costs from $i$ to $j$ | $d_{ij} \geq 1$, $d_{ii} = 1$ | Mixing $d$ and $\tau$ in same lecture |
| Trade shares | $\pi_{ij}$ = share of $j$'s spending on goods from $i$ | $\sum_i \pi_{ij} = 1$ for each $j$ | Reversed subscript convention |
| Wages | $w_i$ for wage in region $i$ | -- | Using $w$ without subscript in spatial context |
| Population/Labor | $L_i$ for workers/population in region $i$ | $\sum_i L_i = \bar{L}$ | Using $N_i$ (conflicts with region count) |
| Data stock | $D_i$ for data stock in region $i$ | -- | Using $D$ for both data and distance |
| Welfare/Utility | $U_i$ for indirect utility in region $i$ | -- | Mixing $W$ and $U$ across lectures |
| Hat notation | $\hat{x} = x'/x$ for proportional changes (hat algebra) | $\hat{w}_i = w_i'/w_i$ | Using $\hat{\cdot}$ for econometric estimates (use $\hat{\beta}$ only) |
| Trade elasticity | $\theta$ for Frechet shape / trade elasticity | -- | Using $\sigma$ (conflicts with substitution elasticity) |
| Substitution elasticity | $\sigma$ for CES elasticity of substitution | -- | Using $\theta$ (conflicts with trade elasticity) |
| Migration | $\mu_{ij}$ for migration probability from $i$ to $j$ | $\sum_j \mu_{ij} = 1$ | Using $m_{ij}$ without defining |
| Productivity | $A_i$ for TFP / fundamental productivity in region $i$ | -- | Using $z$ for both productivity and Frechet draw |
| Amenities | $B_i$ for amenity value in region $i$ | -- | Mixing $a_i$ and $B_i$ |
| Data nonrivalry | $\rho \in [0,1]$ for degree of data nonrivalry | $\rho = 1$ fully nonrival | Not defining $\rho$ before use |
| Price index | $P_j$ for CES price index in region $j$ | -- | Using $p_j$ for both price index and individual price |

## Symbol Reference

| Symbol | Meaning | Introduced |
|--------|---------|------------|
| $\pi_{ij}$ | Trade share: fraction of $j$'s spending on goods from $i$ | Lecture 2 |
| $d_{ij}$ | Iceberg trade cost from $i$ to $j$ | Lecture 2 |
| $w_i$ | Wage in region $i$ | Lecture 2 |
| $L_i$ | Population/labor in region $i$ | Lecture 2 |
| $P_j$ | CES price index in region $j$ | Lecture 2 |
| $\sigma$ | CES elasticity of substitution | Lecture 2 |
| $\theta$ | Trade elasticity (Frechet shape parameter) | Lecture 3 |
| $A_i$ | Fundamental productivity in region $i$ | Lecture 3 |
| $B_i$ | Amenity value in region $i$ | Lecture 3 |
| $\mu_{ij}$ | Migration probability from $i$ to $j$ | Lecture 5 |
| $\hat{x}$ | Proportional change: $x'/x$ (hat algebra) | Lecture 3 |
| $D_i$ | Data stock in region $i$ | Lecture 9 |
| $\rho$ | Degree of data nonrivalry ($\rho = 1$ = fully nonrival) | Lecture 9 |

## Lecture Progression

| # | Title | Core Question | Key Notation | Key Method |
|---|-------|--------------|-------------|------------|
| 1 | Introduction & Motivation | Why combine spatial + data economics? | Overview of all notation | Conceptual framework |
| 2 | Foundations of Spatial Equilibrium | How do wages/rents adjust across space? | $w_i, r_i, L_i, P_j, \sigma$ | Rosen-Roback, CES aggregation |
| 3 | Quantitative Spatial Models | How to build and solve a spatial GE model? | $\pi_{ij}, d_{ij}, \theta, \hat{x}$ | EK gravity, hat algebra |
| 4 | Geography of Development | How does geography shape long-run development? | $A_i(t), L_i(t)$ dynamics | DNR dynamic spatial model |
| 5 | Trade & Labor Dynamics I | How do trade shocks propagate through space? | $\mu_{ij}, V_i$ value functions | CDP dynamic spatial GE |
| 6 | Trade & Labor Dynamics II | How to compute and estimate the China shock? | Counterfactual $\hat{w}_i$ | Calibration, counterfactuals |
| 7 | Mechanics of Spatial Growth | What drives spatial growth patterns? | Innovation diffusion | CCPX spatial growth mechanics |
| 8 | Computational Methods | How to solve these models numerically? | Convergence criteria | Fixed-point, Newton, dampening |
| 9 | Economics of Data: Nonrivalry | How does data's nonrivalry affect growth? | $D, \rho$ | JT growth model |
| 10 | Multi-Purpose Data & Growth | How does multi-purpose data change growth? | Data production function | Cong et al. endogenous growth |
| 11 | Data Markets & Policy | How should data markets be regulated? | Market design, taxes | WJG GE data market model |
| 12 | Unified Framework I: Theory | How to combine spatial models with data? | $D_i, \pi_{ij}^D$ data flows | Synthesis model |
| 13 | Unified Framework II: Computation | How to solve the unified model? | Hat algebra + data dynamics | Computational implementation |
| 14 | Frontiers & Research Agenda | What are the open questions? | -- | Student presentations |

## Empirical Applications

| Application | Paper | Dataset | Lecture(s) | Purpose |
|------------|-------|---------|------------|---------|
| US commuting zones & China shock | CDP (2019) | Census, trade flows | 5, 6 | Dynamic GE trade shock analysis |
| World development patterns | DNR (2018) | Cross-country spatial data | 4 | Geography and long-run development |
| Data economy measurement | JT (2020) | National accounts | 9, 12 | Data as production factor |
| China data market policy | WJG (2023) | Chinese administrative data | 11 | Fiscal/tax policy for data markets |
| Innovation diffusion & growth | CCPX (2025) | Patent/R&D data | 7 | Spatial growth mechanics |
| NAFTA trade effects | CP (2015) | Bilateral trade data | 3 | Structural gravity estimation |

## Design Principles

| Principle | Evidence | Lectures Applied |
|-----------|----------|-----------------|
| Build spatial intuition before math | Students need to "see" spatial equilibrium | Lecture 2 |
| Show partial before general equilibrium | GE feedback loops confuse without PE foundation | Lectures 2-3, then 5-6 |
| Always connect theory to computation | "How would you actually solve this?" after every model | Lectures 3, 6, 8, 13 |
| Bridge with explicit parallel structure | Same model structure in spatial and data sections | Lectures 3 vs 9, 6 vs 11 |

## Anti-Patterns (Don't Do This)

| Anti-Pattern | What Happened | Correction |
|-------------|---------------|-----------|
| Using $\hat{x}$ for both hat algebra and OLS estimates | Students confuse exact hat algebra with econometric hats | Use $\hat{\beta}$ for estimates, $\hat{x}$ only for proportional changes |
| Presenting welfare formula without derivation | Students memorize formula without understanding | Show CES aggregation step by step before welfare result |
| Jumping from partial to general equilibrium | Missing the feedback loop intuition | Always diagram the circular flow before writing equations |
| Writing trade shares as $\pi_{ji}$ instead of $\pi_{ij}$ | Subscript convention collision with other papers | Always define: $\pi_{ij}$ = share of $j$'s spending from $i$ |
| Treating data like a standard rival input | Misapplies standard production theory | Explicitly state and check nonrivalry in every data production function |

## R Code Pitfalls

| Bug | Impact | Fix |
|-----|--------|-----|
| `colSums(pi_matrix) != 1` after solver | Invalid trade equilibrium | Add `stopifnot()` check after every solver step |
| `fixest::fepois` silently drops obs | Gravity estimate biased | Check `nobs()` matches input data |
| CRS mismatch in `sf` spatial joins | Wrong region assignments | Always `st_transform()` to common CRS first |
| Dense matrix for large N | Memory crash | Use `Matrix::sparseMatrix` for trade cost/share matrices |
| `log(trade_flow)` with zeros | NaN propagation | Use PPML (no log transform needed) or document epsilon |
