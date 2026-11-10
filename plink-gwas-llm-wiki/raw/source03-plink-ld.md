# S03 — PLINK 1.9 Linkage Disequilibrium

- **Source ID:** S03
- **Source type:** Official documentation
- **Title:** Linkage disequilibrium — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/ld
- **Retrieved:** 2026-11-10
- **Primary use:** LD pruning and `--indep-pairwise`

## Key knowledge extracted

PLINK provides LD-based variant pruning commands including `--indep`, `--indep-pairwise`, and `--indep-pairphase`.

For:

`--indep-pairwise <window size> <step size> <r^2 threshold>`

the three core parameters are:

1. window size,
2. number of variants by which the window moves,
3. pairwise squared-correlation (`r²`) threshold.

The procedure produces:

- `plink.prune.in`: variants retained in the approximately linkage-equilibrium subset
- `plink.prune.out`: variants excluded by pruning

These files can later be supplied to `--extract` or `--exclude`.

## Teaching points allowed from this source

- Explain LD pruning conceptually.
- Explain the three `--indep-pairwise` parameters.
- Explain `.prune.in` and `.prune.out`.
- Explain why an approximately LD-independent set is useful for analyses such as PCA or relatedness.

## Cautions

- Do not imply that the LD-pruned subset must replace the full post-QC dataset for the final genome-wide association scan.
- Parameter values such as `50 5 0.2` should be presented as examples, not universal standards.

## Suggested Wiki mapping

- `wiki/04-ld-pruning.md`
