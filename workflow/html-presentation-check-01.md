# HTML Presentation Check — Run 01

- **Date:** 2026-11-10
- **Target:** `presentation/index.html`

## Structural checks

| Check item | Result |
|---|---|
| HTML file exists | PASS |
| CSS file exists | PASS |
| Total slides = 11 | PASS |
| Prev / Next buttons exist | PASS |
| Slide sidebar navigation exists | PASS |
| Source lines included on each slide | PASS |

## Content checks

| Check item | Result |
|---|---|
| Slide 4 clearly marks `--geno 0.02` as example | PASS |
| Slide 5 clearly marks `--maf 0.01` and `--hwe 1e-6` as examples | PASS |
| Slide 6 warns that LD-pruned set is not automatically the final GWAS SNP set | PASS |
| Slide 9 uses verified phenotype / covariate format from S08 | PASS |
| Slide 10 describes `P < 5 × 10^-8` as common GWAS convention | PASS |
| Slide 11 states QQ deviation cannot alone prove one cause | PASS |

## Decision

The HTML presentation is ready for GitHub upload / GitHub Pages deployment.


## Slide 10 wording revision

Original wording:

`常見 convention：P < 5 × 10^-8`

was revised to:

`GWAS 常用的全基因組顯著性門檻：P < 5 × 10⁻⁸`

**Recheck:** PASS
