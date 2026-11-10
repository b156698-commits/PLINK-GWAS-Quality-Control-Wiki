# Wiki Generation Log

- **Run:** Wiki Generation 01
- **Date:** 2026-11-10
- **Input:** S01–S07 raw source notes
- **Output:** 8 Wiki chapters

## Source-mapping validation

| Wiki file | Expected sources | Found | Sources section | Threshold/context check |
|---|---|---|---|---|
| `01-plink-basics.md` | S01 | S01 | Pass | Pass |
| `02-missingness.md` | S02 | S02 | Pass | Pass |
| `03-maf-hwe.md` | S02 | S02 | Pass | Pass |
| `04-ld-pruning.md` | S03 | S03 | Pass | Pass |
| `05-relatedness.md` | S04 | S04 | Pass | Review |
| `06-pca.md` | S05 | S05 | Pass | Pass |
| `07-association.md` | S05, S06 | S05, S06 | Pass | Pass |
| `08-gwas-results.md` | S07 | S07 | Pass | Pass |

## Findings

### Pass

- All 8 chapters contain a `Sources` section.
- All chapters include the expected Source IDs.
- Missingness, MAF/HWE, LD pruning, relatedness and GWAS significance chapters explicitly distinguish examples/defaults from universal standards.
- `08-gwas-results.md` explicitly separates Manhattan/QQ interpretation from PLINK QC commands.

### Issue discovered during Wiki generation

`07-association.md` exposed a source-coverage gap. The current raw sources support logistic regression and covariates conceptually, but do **not yet fully support the exact teaching format** for:

- phenotype file columns
- covariate file columns
- `--pheno-name`
- `--covar-name`

Instead of letting the model fill these details from memory, the Wiki marks this section as **尚待驗證**.

## Workflow implication

This is the first concrete example showing why source validation should happen **before presentation generation**.
Before the HTML presentation is created, any unsupported detail must either:

1. be removed from the teaching content, or
2. trigger a source-retrieval loop to obtain additional documentation.

This finding is recorded as an execution issue, but the final reflection will only be written after the complete Wiki → presentation workflow has been run once.

## Resolution after Source Retrieval Loop 01

The Association Analysis source gap triggered a return to source retrieval.

- Added source: **S08**
- Source type: PLINK 1.9 official input + file format documentation
- Updated: `wiki/07-association.md`
- Revalidation: **Pass**

The previously unsupported phenotype/covariate format section is now backed by S08.

This demonstrates an actual graph edge:

```text
Wiki generation
→ source check failed
→ source retrieval
→ ingest S08
→ validate
→ regenerate Wiki
→ pass
```
