# S04 — PLINK 1.9 Identity-by-Descent

- **Source ID:** S04
- **Source type:** Official documentation
- **Title:** Identity-by-descent — PLINK 1.9
- **URL:** https://www.cog-genomics.org/plink/1.9/ibd
- **Retrieved:** 2026-11-10
- **Primary use:** Relatedness, IBD, PI_HAT

## Key knowledge extracted

The PLINK 1.9 documentation explicitly notes that its IBD calculations are **not LD-aware**, so LD-based pruning is usually advisable before running them.

`--genome` performs IBS/IBD calculations over autosomal SNPs and writes a `.genome` report.

Important fields include:

- `Z0`: estimated probability of sharing 0 alleles IBD
- `Z1`: estimated probability of sharing 1 allele IBD
- `Z2`: estimated probability of sharing 2 alleles IBD
- `PI_HAT`: estimated proportion IBD

The documented relationship is:

`PI_HAT = Z2 + 0.5 × Z1`

`--min` and `--max` can filter report rows by PI_HAT.

## Teaching points allowed from this source

- Explain relatedness/IBD at a beginner level.
- Explain PI_HAT and its formula.
- Explain why LD pruning should precede this calculation.

## Cautions

- The documentation does not establish one universal PI_HAT cutoff for every study.
- `--genome` reports pairwise information; deciding which sample to remove requires an analysis rule beyond the command itself.

## Suggested Wiki mapping

- `wiki/05-relatedness.md`
