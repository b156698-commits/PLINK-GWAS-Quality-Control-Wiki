# S07 — Basic Statistical Analysis in Genetic Case-Control Studies

- **Source ID:** S07
- **Source type:** Peer-reviewed methods article
- **Title:** Basic statistical analysis in genetic case-control studies
- **Journal:** Nature Protocols
- **Year:** 2011
- **PMCID:** PMC3154648
- **URL:** https://pmc.ncbi.nlm.nih.gov/articles/PMC3154648/
- **Retrieved:** 2026-11-10
- **Primary use:** GWAS result visualization and interpretation

## Key knowledge extracted

The article describes basic statistical analysis for genetic case-control studies, including association testing, multiple-testing control, visualization, interpretation, and replication.

### QQ plot

The article describes quantile-quantile plots as a way to compare observed association statistics with what would be expected under the null hypothesis.

In its worked GWAS example, most points follow the null expectation while the strongest signals depart in the upper tail.

### Manhattan plot

The article describes a Manhattan plot as showing association-test p-values across chromosomal position, commonly on a `-log10(P)` scale.

Its example highlights genome-wide significant regions using:

`P < 5 × 10^-8`

This should be described as a widely used GWAS convention / the threshold used in the example, not as a logical constant applying to every genetic analysis.

### Interpretation

Strong association signals still require additional scrutiny and replication; statistical significance alone does not establish causality.

## Teaching points allowed from this source

- Explain the axes and purpose of Manhattan plots.
- Explain the basic purpose of QQ plots.
- Introduce genome-wide significance and multiple testing.
- Explain why replication remains important.

## Cautions

- The article is a methods protocol from 2011; it should be used for foundational concepts rather than claims about the newest GWAS software.
- Do not equate association with causation.
- Do not treat every deviation in a QQ plot as proof of one specific problem.

## Suggested Wiki mapping

- `wiki/08-gwas-results.md`
