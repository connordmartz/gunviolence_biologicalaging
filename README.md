# Neighborhood Gun Violence and Biological Aging in Adolescence

Replication code for:

> Martz, C.D., et al. (2026). *Residential exposure to deadly gun violence and accelerated biological aging in a national sample of U.S. adolescents*. *SSM – Population Health*. https://doi.org/10.1016/j.ssmph.2026.101937

---

## Overview

This repository contains the R code used to produce all analyses reported in the above paper, which examines whether exposure to neighborhood gun violence is associated with accelerated biological aging in adolescence. The study uses geocoded data from the Future of Families and Child Wellbeing Study (FFCWS) linked to the Gun Violence Archive (GVA). Epigenetic clock measures (GrimAge, PhenoAge, DunedinPACE) were assayed at ages ~9 (Year 5 wave) and ~15 (Year 6 wave). Propensity score matching (PSM) was used to address residential sorting and confounding by socioeconomic and neighborhood conditions.

---

## Data Availability

The FFCWS data used in this study are **restricted-use** and not publicly available. Researchers may apply for access through the [FFCWS Data Archive](https://ffcws.princeton.edu/data-and-documentation). The geocoded restricted-use contract data (tract-level, GVA, and UCR linkages) require a separate data use agreement. Epigenetic clock data are publically available at the [FFCWS Study Website](https://fragilefamilies.princeton.edu/).

This repository provides the analytic code only; no data files are included. 

---

## Repository Contents

| File | Description |
|------|-------------|
| `Data Cleaning` | Imports and merges FFCWS core, DNAm, tract-level, GVA, and UCR data; constructs epigenetic clock residuals and standardized scores; creates gun violence exposure variables (binary, count, categorical, distance-band); codes all covariates |
| `stepwise regression models` | Constructs latent biological aging summary scores (CFA); runs the primary stepwise OLS regression models (Models 1–5) with heteroscedasticity-robust SEs |
| `propensity score matching & weighted regression models` | Estimates full matching PSM model (`MatchIt`); assesses covariate balance; runs ATT-standardized weighted outcome regression models with cluster-robust SEs |
| `sensitivity analyses` | Eleven supplementary analyses including alternative exposure operationalizations (any/none, categorical, closer distance buffers), adjustment for concurrent violent crime rates, restriction to participants with ≥1 year of GVA exposure data, residential mobility adjustment, measurement invariance tests, and race/ethnicity moderation |

---

## Analytic Overview

**Sample:** FFCWS participants with DNA methylation data at both ages ~9 and ~15, linked to geocoded neighborhood data (N = 1,781).

**Exposure:** Incident gun violence events within 1,600 meters of the participant's home address in the year prior to the age-15 DNAm sample (Gun Violence Archive), operationalized as:
- Binary (any vs. none)
- Continuous count
- Categorical intensity (low/moderate/high)
- Distance-banded counts at 100m intervals (500m–1600m)

**Outcomes:** Three epigenetic clocks measured at age ~15, residualized on chronological age:
- GrimAge acceleration
- PhenoAge acceleration
- DunedinPACE (standardized)

A latent biological aging summary score was derived via confirmatory factor analysis (CFA) across the three clocks.

**Primary approach:** Full propensity score matching (logistic, ATT estimand) with exact matching on race/ethnicity and calipers on poverty, tract poverty, and prior violent crime; weighted outcome regression with subclass-clustered robust standard errors.

**Stepwise models:** Five sequential OLS models progressively adjusting for biological covariates, individual SES, neighborhood SES, race/ethnicity, and prior biological aging at age 9 and prior violent crime.

---

## Software and Key Packages

All analyses were conducted in **R**. Key packages include:

| Package | Use |
|---------|-----|
| `MatchIt` | Propensity score matching |
| `cobalt` | Covariate balance assessment |
| `lavaan` | CFA and measurement invariance testing |
| `sandwich` / `lmtest` | Robust and clustered standard errors |
| `marginaleffects` | Average marginal effects and predicted value calculations |
| `survey` / `weights` | Weighted analyses |
| `tidyverse` | Data wrangling |
| `haven` | Importing Stata `.dta` files |

A full list of loaded packages is at the top of the `Data Cleaning` script.

---

## Citation

If you use this code, please cite the published paper:

> Martz CD, Farina MP, Fleckman JM, et al. Residential exposure to deadly gun violence and accelerated biological aging in a national sample of U.S. adolescents. *SSM - Population Health*. 2026;35:101937. doi:10.1016/j.ssmph.2026.101937

---
