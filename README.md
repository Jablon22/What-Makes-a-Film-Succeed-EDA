# What Makes a Film Succeed? — Exploratory Data Analysis

**Author:** Jakub Groblicki  
**Language:** R · R Markdown  
**Output:** HTML report

![R](https://img.shields.io/badge/R-%3E%3D4.1-276DC3?style=flat-square&logo=r&logoColor=white)
![Status](https://img.shields.io/badge/status-exploratory-orange?style=flat-square)

---

## Overview

This project is a structured exploratory data analysis of a feature-film dataset spanning several decades of theatrical releases. The report examines financial performance, IMDb audience ratings, and the characteristics of industry-recognised productions, rendered as a self-contained HTML document with collapsible code blocks and a floating table of contents.

All findings are descriptive — they identify patterns and associations in the data and do not establish causal relationships.

---

## Research Questions

1. What factors are associated with a film posting a negative financial result?
2. What influences a film's IMDb rating?
3. Do industry-recognised films differ systematically from the rest?

---

## Dataset

Source file: `movies_data.csv` — one row per film, 16 variables.

| Variable | Type | Description |
|---|---|---|
| `Movie` | Text | Film title |
| `Director` | Text | Director's name |
| `Running time` | Numeric | Duration in minutes |
| `Actor 1–3` | Text | Lead and supporting cast |
| `Genre` | Categorical | Film genre (e.g. Action, Drama) |
| `Budget` | Numeric | Production budget (USD) |
| `Box Office` | Numeric | Total theatrical revenue (USD) |
| `Earnings` | Numeric | Box Office − Budget (USD) |
| `Actors Box Office %` | Numeric | % of cast's prior films with revenue ≥ 2× budget |
| `Director Box Office %` | Numeric | % of director's prior films with revenue ≥ 2× budget |
| `Oscar and Golden Globes nominations` | Numeric | Total nominations received |
| `Oscar and Golden Globes awards` | Numeric | Total awards won |
| `Release year` | Numeric | Year of theatrical release |
| `IMDb score` | Numeric | Mean audience rating (1–10 scale) |

> **Note on earnings:** `Earnings` reflects theatrical box office only. Real-world profitability would additionally include home video, streaming rights, television licensing, and merchandise — none of which are captured here.

---

## How to Run

1. Install R (≥ 4.1) and RStudio.

2. Place `movies_data.csv` in the same directory as the `.Rmd` file.

3. Install required packages:
```r
   install.packages(c(
     "tidyverse", "psych", "gridExtra", "mice",
     "corrplot", "nortest", "scales", "dunn.test"
   ))
```

4. Open the `.Rmd` file in RStudio and click **Knit**, or run from the console:
```r
   rmarkdown::render("eda_films.Rmd")
```

5. The output is a self-contained `.html` file in the same directory — open it in any browser.

---

## R Packages Used

| Package | Purpose |
|---|---|
| `tidyverse` | Data wrangling and ggplot2 visualisations |
| `psych` | Extended descriptive statistics (skewness, kurtosis) |
| `gridExtra` | Multi-panel plot layouts |
| `mice` | Missing data pattern visualisation |
| `corrplot` | Correlation matrix heatmap |
| `nortest` | Anderson-Darling normality test |
| `scales` | Axis label formatting (currency, percentages) |
| `dunn.test` | Dunn post-hoc test with BH correction |

---

## Key Findings

**Financial outcomes**  
Earnings differ significantly across genres (Kruskal-Wallis, p < 0.001). Drama and Biography show the highest loss rates among well-represented genres. Budget is statistically higher for profitable films, but the effect size is modest and distributional overlap is large — no single variable reliably predicts profit.

**IMDb ratings**  
Award wins and nominations are the strongest predictors of high, consistent ratings. Budget and box office show only negligible-to-small associations with IMDb scores. Newer films score marginally lower on average, most plausibly due to survivorship bias rather than any genuine decline in quality.

**Industry-recognised films**  
Award-winning films are systematically longer and rated higher than non-nominated films. The co-occurrence of high audience ratings and industry recognition is consistent across multiple analyses.

---

## Statistical Methods

All financial variables are strongly right-skewed; robust and non-parametric methods are used throughout:

- **Spearman rank correlation** — monotonic associations between continuous variables
- **Wilcoxon rank-sum test** — comparison of two independent groups
- **Kruskal-Wallis test** — comparison across multiple groups (genre)
- **Dunn post-hoc test** — pairwise comparisons with Benjamini-Hochberg FDR correction
- **Anderson-Darling test** — normality assessment

Effect sizes are interpreted using Cohen's benchmarks: |ρ| < 0.10 negligible, 0.10–0.30 small, 0.30–0.50 medium, > 0.50 large.

---
