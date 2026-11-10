# Source Retrieval Loop — Run 01

## Trigger

During **Wiki Generation 01**, the Association Analysis node failed its source-coverage check.

The model was about to teach exact phenotype and covariate file formats, but S01–S07 did not yet provide enough explicit support for all of those details.

## Initial failed state

```text
S01–S07
   ↓
Generate Association Wiki
   ↓
Source coverage check
   ↓
FAIL:
phenotype/covariate exact format not fully supported
```

## Retrieval action

The workflow returned to the **source retrieval** node.

Additional official PLINK documentation was retrieved for:

- `--pheno`
- `--pheno-name`
- phenotype coding
- `--covar`
- `--covar-name`
- `.assoc.logistic` output

This material was ingested as **S08**.

## Validation after retrieval

```text
S08 retrieved
   ↓
Check exact statements against official documentation
   ↓
PASS
   ↓
Regenerate wiki/07-association.md
```

## Concrete changes after S08

The updated Wiki now includes verified examples of:

```text
FID IID STATUS
```

for phenotype files and:

```text
FID IID AGE SEX PC1 PC2 PC3
```

for covariate files.

It also includes a verified complete teaching command:

```bash
plink   --bfile qc_final   --pheno phenotype.txt   --pheno-name STATUS   --covar covariates.txt   --covar-name AGE,SEX,PC1-PC3   --logistic hide-covar   --out gwas_logistic
```

## Why this loop matters

If the workflow had generated the final HTML presentation before this source check, unsupported or incorrectly remembered file-format details could have been propagated into the slides.

The retrieval loop therefore keeps **source verification before presentation generation**.
