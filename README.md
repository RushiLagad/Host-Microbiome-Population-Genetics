# Host-Microbiome-Population-Genetics

![R](https://img.shields.io/badge/R-4.4.1-blue) ![License](https://img.shields.io/badge/license-MIT-green) ![Status](https://img.shields.io/badge/status-active-brightgreen)

> Genomic heritability (GREML/AI-REML) and bivariate genetic correlation between rumen microbiome diversity and host production traits in livestock.

## Overview

This repository implements population genetics methods to quantify the host genetic contribution to rumen microbiome composition. The pipeline uses Genomic Relationship Matrices (GRM) and Average Information REML (AI-REML) to estimate SNP-based heritabilities and genetic correlations between microbial diversity and economically important livestock traits.

## Analysis Workflow

```
Genotype Matrix (n=600, m=2000 SNPs)
    |
    v
Van Raden GRM Construction (K = ZZ'/m)
    |
    v
Univariate AI-REML --> h2 (Shannon Diversity, RFI)
    |
    v
Bivariate AI-REML --> Genetic Correlation (rg)
    |
    v
Cholesky Simulation for Validation
```

## Repository Structure

```
Host-Microbiome-Population-Genetics/
├── data/               # Genotype matrices, phenotype files
├── scripts/            # R scripts
│   ├── 01_simulate_genotypes.R
│   ├── 02_grm_construction.R
│   ├── 03_greml_heritability.R
│   └── 04_bivariate_genetic_correlation.R
├── results/            # Heritability estimates, CI plots
├── README.md
├── LICENSE
└── .gitignore
```

## Key Methods

| Analysis | Method | Package |
|----------|--------|---------|
| GRM construction | Van Raden (2008) | Base R |
| Heritability estimation | AI-REML | `gaston` |
| Bivariate analysis | Bivariate AI-REML | `gaston` |
| Phenotype simulation | Cholesky decomposition | `MASS` |
| Visualization | Forest + CI plots | `ggplot2` |

## Key Results

| Trait | True h² | Estimated h² | SE |
|-------|---------|-------------|----|
| Shannon Diversity | 0.42 | 0.408 | 0.068 |
| Residual Feed Intake (RFI) | 0.31 | 0.326 | 0.071 |

- **Genetic correlation** (rg): 0.361 (95% CI: 0.145, 0.577); True = 0.38
- Positive rg suggests host genetics promoting microbial diversity partially overlaps with feed efficiency loci

## Dependencies

```r
library(gaston)
library(rrBLUP)
library(MASS)
library(tidyverse)
library(ggplot2)
```

## Reproducibility

All analyses use `set.seed(2026)`. Genotypes are simulated with known MAF (0.05–0.45) and Cholesky-decomposed phenotypes ensure exact genetic architecture.

## Author

**Rushikesh Lagad** | PhD Researcher, Genomics & Bioinformatics | University of Arkansas

## License

MIT License — see [LICENSE](LICENSE) for details.
