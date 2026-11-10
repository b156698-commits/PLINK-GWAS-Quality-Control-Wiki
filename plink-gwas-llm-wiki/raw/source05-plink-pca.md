# S05 — PLINK 1.9 Population Stratification / PCA

- **Source ID:** S05
- **Source type:** Official documentation
- **Title:** Population stratification — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/strat
- **Retrieved:** 2026-11-10
- **Primary use:** PCA and population structure

## Key knowledge extracted

PLINK 1.9 provides principal components analysis with:

`--pca [count]`

The documentation states that PLINK calculates PCA from the variance-standardized relationship matrix.

By default, `--pca` extracts the top 20 principal components; a different count can be requested.

Primary outputs are:

- `plink.eigenvec`: sample principal-component scores
- `plink.eigenval`: corresponding eigenvalues

The documentation notes that top PCs are commonly included as covariates in association regressions to help correct for population stratification.

## Teaching points allowed from this source

- Explain what PCA is doing in GWAS at a conceptual level.
- Explain `.eigenvec` and `.eigenval`.
- Explain why PCs may be used as covariates.
- Explain that the number of PCs included in a study is a modeling decision rather than a universal constant.

## Cautions

- Do not state that exactly 10 or 20 PCs must always be used.
- A default output count is not equivalent to the appropriate number of covariates for every analysis.

## Suggested Wiki mapping

- `wiki/06-pca.md`
