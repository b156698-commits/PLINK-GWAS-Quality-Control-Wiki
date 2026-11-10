# S08 — PLINK 1.9 Phenotype and Covariate Input

- **Source ID:** S08
- **Source type:** Official documentation
- **Primary title:** Standard data input — PLINK 1.9
- **Supporting title:** File format reference — PLINK 1.9
- **URL 1:** https://www.cog-genomics.org/plink/1.9/input
- **URL 2:** https://www.cog-genomics.org/plink/1.9/formats
- **Retrieved:** 2026-11-10
- **Primary use:** phenotype/covariate file layout, `--pheno-name`, `--covar-name`, phenotype coding, `.assoc.logistic` output

## Why this source was retrieved

During Wiki Generation 01, `wiki/07-association.md` exposed a source-coverage gap.

The previous sources supported logistic regression and the idea of covariates, but did not yet fully support teaching:

- exact phenotype file layout,
- exact covariate file layout,
- `--pheno-name`,
- `--covar-name`,
- case/control phenotype coding,
- `.assoc.logistic` output fields.

This source-retrieval step was triggered before presentation generation.

---

## Phenotype input

PLINK 1.9 `--pheno <filename>` loads phenotype values from a space- or tab-delimited file.

The first two columns must contain:

1. `FID` — family ID
2. `IID` — within-family / individual ID

By default, the phenotype is read from the third column.

Example without selecting by column name:

```text
F001 I001 1
F001 I002 2
F002 I003 2
```

With a header, a phenotype can be selected by name:

```text
FID IID STATUS
F001 I001 1
F001 I002 2
F002 I003 2
```

Command:

```bash
--pheno phenotype.txt --pheno-name STATUS
```

For `--pheno-name` to work, the file must have a header whose first two entries are `FID` and `IID`.

### Case/control coding

PLINK 1.9 normally expects case/control phenotypes as:

- `1` = unaffected / control
- `2` = affected / case
- `0` = alternate missing value
- missing phenotype is normally represented by `-9`

If the `--1` flag is used, PLINK instead interprets:

- `0` = unaffected / control
- `1` = affected / case

---

## Covariate input

`--covar <filename>` loads covariates.

The basic covariate file layout follows the same ID convention:

```text
FID IID AGE SEX PC1 PC2 PC3
F001 I001 70 1 -0.012 0.031 -0.004
F001 I002 66 2  0.008 0.022  0.011
F002 I003 74 1 -0.020 0.015  0.006
```

The first two columns are `FID` and `IID`; remaining columns contain covariates.

A header is optional for `--covar`, but a header is needed when selecting covariates by name.

`--covar-name` selects covariates by column name.

For example:

```bash
--covar covariates.txt --covar-name AGE,SEX,PC1-PC3
```

Ranges can be specified with a dash when the columns occur in sequence.

By default, if a covariate is missing for a sample, the main phenotype is set to missing for that analysis. PLINK provides the `keep-pheno-on-missing-cov` modifier if that behavior needs to be changed.

---

## Logistic regression

For a case/control phenotype:

```bash
--logistic
```

performs logistic regression and can incorporate covariates loaded with `--covar`.

A complete teaching example is:

```bash
plink   --bfile qc_final   --pheno phenotype.txt   --pheno-name STATUS   --covar covariates.txt   --covar-name AGE,SEX,PC1-PC3   --logistic hide-covar   --out gwas_logistic
```

This example assumes that:

- `phenotype.txt` has `FID IID STATUS`,
- `covariates.txt` has `FID IID AGE SEX PC1 PC2 PC3`,
- IDs match those in the genotype dataset,
- the chosen covariates are appropriate for the study design.

---

## `.assoc.logistic` output

PLINK's file format reference states that `--logistic` produces an `.assoc.logistic` report.

Typical fields include:

- `CHR`
- `SNP`
- `BP`
- `A1`
- `TEST`
- `NMISS`
- `OR` (or `BETA` with `--logistic beta`)
- `STAT`
- `P`

`NMISS` is the number of observations with nonmissing genotype, phenotype, and covariates.

---

## Teaching points allowed from this source

- Teach exact basic layout of phenotype and covariate files.
- Teach the use of `--pheno`, `--pheno-name`, `--covar`, and `--covar-name`.
- Teach normal PLINK case/control coding.
- Give a complete logistic-regression command example.
- Explain the main `.assoc.logistic` fields.

## Cautions

- Covariate choice is study-specific; AGE, SEX, and PCs are examples, not a mandatory universal set.
- The number of PCs is not fixed.
- Users must verify that sample IDs match the genotype dataset.
- Do not silently mix PLINK 1.9 coding conventions with other software conventions.

## Suggested Wiki mapping

- `wiki/07-association.md`
