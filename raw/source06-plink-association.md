# S06 — PLINK 1.9 Association Analysis

- **Source ID:** S06
- **Source type:** Official documentation
- **Title:** Association analysis — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/assoc
- **Retrieved:** 2026-11-10
- **Primary use:** Case-control association and logistic regression

## Key knowledge extracted

PLINK 1.9 offers several association procedures.

For a case/control phenotype:

- `--assoc` can run a basic 1-df allelic association test.
- `--logistic` performs logistic regression and supports covariates supplied through a covariate file.
- `hide-covar` can suppress covariate-specific rows from the main report.
- The `beta` modifier causes logistic regression coefficients to be reported instead of odds ratios.

The documentation also notes that PCA can be useful for handling population stratification in association analysis.

## Teaching points allowed from this source

- Explain why logistic regression is appropriate for a case/control GWAS.
- Explain the role of covariates such as age, sex, and PCs at a conceptual level.
- Explain odds ratio versus beta output at a basic level.

## Cautions

- Covariate selection must follow the study design; this source does not define one mandatory covariate set.
- Do not claim that association testing should be run only on the LD-pruned SNP subset.
- Exact phenotype/covariate file formats should be verified from the relevant PLINK input documentation before teaching those formats.

## Suggested Wiki mapping

- `wiki/07-association.md`
