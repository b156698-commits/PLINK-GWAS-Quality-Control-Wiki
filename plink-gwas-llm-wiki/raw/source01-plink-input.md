# S01 — PLINK 1.9 Standard Data Input

- **Source ID:** S01
- **Source type:** Official documentation
- **Title:** Standard data input — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/input
- **Retrieved:** 2026-11-10
- **Primary use:** PLINK binary fileset and basic input concepts

## Key knowledge extracted

PLINK 1.9 commonly works with a PLINK 1 binary fileset consisting of:

- `.bed`: binary genotype data
- `.bim`: variant information
- `.fam`: sample/family information

The `--bfile <prefix>` flag refers to the three files sharing the same prefix:
`<prefix>.bed`, `<prefix>.bim`, and `<prefix>.fam`.

PLINK 1.9 treats the PLINK 1 binary fileset as its preferred input format and can convert many other formats to this representation during loading.

## Teaching points allowed from this source

- Explain what `.bed/.bim/.fam` represent at a basic level.
- Explain the purpose of `--bfile`.
- Introduce the idea that GWAS analysis starts from genotype and sample/variant metadata.

## Cautions

- Do not infer QC thresholds from this page.
- Do not use this page as the sole source for phenotype/covariate file details unless those details are separately verified.

## Suggested Wiki mapping

- `wiki/01-plink-basics.md`
