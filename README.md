# Italian Olive Oil — Data Visualisation & Reporting

![R](https://img.shields.io/badge/R-R_Markdown-276DC3?style=flat&logo=r&logoColor=white)
![ggplot2](https://img.shields.io/badge/ggplot2-visualisation-blue?style=flat)
![University](https://img.shields.io/badge/Università_Vanvitelli-BSc_Data_Analytics-darkred?style=flat)

**Course:** Data Visualisation and Reporting  
**Institution:** Università degli Studi della Campania 'Luigi Vanvitelli'  
**Degree:** BSc in Data Analytics · 2023–2024

---

## Overview

An exploratory data analysis and visualisation report on 572 Italian olive oil samples, produced as an **R Markdown** document rendered to interactive HTML. The analysis explores the geographical distribution of samples across Italian regions and areas, and the fatty acid composition profiles that distinguish them.

The report is fully reproducible: all code is embedded in the `.Rmd` source with `code_folding: hide`, making it readable as a clean narrative while keeping the full pipeline accessible.

---

## Dataset

**Source:** Gasteiger & Zupan (1999), *Neural Networks in Chemistry and Drug Design*  
**Originally collected:** October 8, 1999  
**Field:** Computational Chemistry and Molecular Modelling  
**Original purpose:** Benchmarking classification methods (backpropagation vs. Kohonen networks) on chemical composition data

| Property | Value |
|---|---|
| Observations | 572 olive oil samples |
| Variables | 11 |
| Missing values | None |

**Variables:**

| Variable | Type | Description |
|---|---|---|
| `region` | Factor (3 levels) | Southern Italy · Sardinia · Northern Italy |
| `area` | Factor (9 levels) | North-Apulia, Calabria, South-Apulia, Sicily, Inland-Sardinia, Coast-Sardinia, Umbria, East-Liguria, West-Liguria |
| `palmitic` | Numeric | % palmitic acid |
| `palmitoleic` | Numeric | % palmitoleic acid |
| `stearic` | Numeric | % stearic acid |
| `oleic` | Numeric | % oleic acid |
| `linoleic` | Numeric | % linoleic acid |
| `linolenic` | Numeric | % linolenic acid |
| `arachidic` | Numeric | % arachidic acid |
| `eicosenoic` | Numeric | % eicosenoic acid |

---

## Analysis Structure

**Data quality checks** — NA count per variable (no missing values found); boxplot-based outlier inspection per region and area.

**Descriptive summary** — Full `dfSummary()` table via `summarytools`, covering frequency distributions, histograms, and summary statistics for all 11 variables.

**Geographical composition** — Sample distribution across the 3 regions and 9 areas visualised via pie charts and an interactive hierarchical treemap (`treemap` + `d3treeR`), showing the two-level region → area nesting.

**Fatty acid profiles** — Average percentage of each of the 8 fatty acids computed at three levels of granularity:
- Overall (all 572 samples) — pie chart
- By region (Southern Italy, Sardinia, Northern Italy) — 3-panel pie chart grid via `ggpubr::ggarrange()`
- By area (all 9 areas) — 3×3 grid of pie charts via `gridExtra::grid.arrange()`

---

## Visualisation Techniques

| Chart type | Purpose | Package |
|---|---|---|
| Pie chart | Region/area composition; fatty acid breakdown | `ggplot2` + `coord_polar` |
| Interactive treemap | Hierarchical region → area drill-down | `treemap` + `d3treeR` |
| Boxplot | Outlier detection per region | `ggplot2` |
| Multi-panel grids | Per-region and per-area fatty acid comparisons | `ggpubr`, `gridExtra`, `patchwork` |
| Interactive data tables | Dataset and summary exploration | `DT` |

---

## Repository Structure

```
italian-olive-eda/
├── Olive_oil_DVR.Rmd     # R Markdown source (fully reproducible)
├── Olive_oil_DVR.html    # Rendered interactive HTML report
├── data/
│   └── Olive.pdf
└── README.md
```

To reproduce: open `Olive_oil_DVR.Rmd` in RStudio and knit to HTML. Requires the `olive.csv` dataset to be placed at the path specified in the script, or update the `read.csv()` path accordingly.

---

## R Dependencies

```r
library(tidyverse)      # data wrangling
library(DT)             # interactive tables
library(summarytools)   # dfSummary
library(ggpubr)         # multi-panel arrangement
library(gridExtra)      # grid.arrange
library(patchwork)      # plot composition
library(treemap)        # static treemap
library(d3treeR)        # interactive D3 treemap
library(waffle)         # waffle charts
library(circlepackeR)   # circle packing
```
