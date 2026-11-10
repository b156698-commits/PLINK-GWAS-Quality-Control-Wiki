# Ingest Log

## Ingest 01 — Initial source set

- **Date:** 2026-11-10
- **Target:** At least 5 source documents
- **Actual:** 7 source documents
- **Sources:** S01–S07
- **Result:** Success

Initial validation identified several risks, including threshold wording and source-boundary issues.

---

## Ingest 02 — Source-retrieval loop

- **Trigger:** Wiki Generation 01
- **Problem:** Association Analysis lacked sufficient source support for phenotype/covariate file details.
- **Action:** Retrieve additional official PLINK input and format documentation.
- **New source:** S08
- **Current total:** 8 source notes
- **Result:** Success

### S08 validation

S08 now supports:

- `--pheno`
- phenotype file `FID IID` layout
- `--pheno-name`
- normal PLINK case/control coding
- `--covar`
- covariate file `FID IID` layout
- `--covar-name`
- `.assoc.logistic` main fields

### Decision

The Association Analysis Wiki chapter can now be regenerated without relying on unsupported model memory.
