# S02 — PLINK 1.9 Input Filtering

- **Source ID:** S02
- **Source type:** Official documentation
- **Title:** Input filtering — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/filter
- **Retrieved:** 2026-11-10
- **Primary use:** Missingness, MAF/MAC, Hardy-Weinberg equilibrium

## Key knowledge extracted

### Missing genotype rate

- `--geno [maximum per-variant]` removes variants whose missing call rate exceeds the specified value.
- `--mind [maximum per-sample]` performs the analogous filtering for samples.
- The documentation lists a default value of `0.1` when these parameters are omitted.

### Minor allele frequency / count

- `--maf [minimum freq]` removes variants with MAF below the supplied threshold.
- The documentation lists a default MAF threshold of `0.01` when `--maf` is invoked without a value.
- `--mac` and related options can filter on minor allele count.

### Hardy-Weinberg equilibrium

- `--hwe <p-value>` filters variants with HWE exact-test p-values below the supplied threshold.
- The PLINK documentation recommends using a low threshold because severe genotyping problems often produce extremely small HWE p-values, while genuine trait association can also cause some deviation.
- `midp` and `include-nonctrl` are available modifiers.

## Teaching points allowed from this source

- Differentiate variant-level missingness (`--geno`) from sample-level missingness (`--mind`).
- Explain MAF filtering.
- Explain HWE filtering and why overly aggressive HWE filtering can be problematic.

## Cautions

- A PLINK default value is not the same as a universally recommended GWAS QC threshold.
- Any classroom example such as `--geno 0.02` or `--hwe 1e-6` must be labeled as an example unless separately supported by a study protocol.

## Suggested Wiki mapping

- `wiki/02-missingness.md`
- `wiki/03-maf-hwe.md`
