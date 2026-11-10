# Source Manifest

## Current ingest set

本專案目前已納入 **8 份來源資料**。

第一次 ingest 為 S01–S07；Wiki Generation 01 發現 Association Analysis 的來源覆蓋不足後，
觸發 source-retrieval loop，新增 **S08**。

| ID | Raw file | Source | Main Wiki use | Status |
|---|---|---|---|---|
| S01 | `source01-plink-input.md` | PLINK 1.9 Standard data input | PLINK Basics | Ingested |
| S02 | `source02-plink-filtering.md` | PLINK 1.9 Input filtering | Missingness, MAF, HWE | Ingested |
| S03 | `source03-plink-ld.md` | PLINK 1.9 Linkage disequilibrium | LD Pruning | Ingested |
| S04 | `source04-plink-ibd.md` | PLINK 1.9 Identity-by-descent | Relatedness / PI_HAT | Ingested |
| S05 | `source05-plink-pca.md` | PLINK 1.9 Population stratification | PCA | Ingested |
| S06 | `source06-plink-association.md` | PLINK 1.9 Association analysis | Association Analysis | Ingested |
| S07 | `source07-gwas-results-paper.md` | GWAS methods article | GWAS Results | Ingested |
| S08 | `source08-plink-pheno-covar.md` | PLINK 1.9 input + format reference | Phenotype, covariates, association output | Ingested after retrieval loop |

## Source URLs

- S01: https://www.cog-genomics.org/plink/1.9/input
- S02: https://www.cog-genomics.org/plink/1.9/filter
- S03: https://www.cog-genomics.org/plink/1.9/ld
- S04: https://www.cog-genomics.org/plink/1.9/ibd
- S05: https://www.cog-genomics.org/plink/1.9/strat
- S06: https://www.cog-genomics.org/plink/1.9/assoc
- S07: https://pmc.ncbi.nlm.nih.gov/articles/PMC3154648/
- S08:
  - https://www.cog-genomics.org/plink/1.9/input
  - https://www.cog-genomics.org/plink/1.9/formats

## Ingest rule

`raw/` 保存的是「可追溯來源筆記」，不是逐字複製完整網頁。

每份 raw file 必須保留：

1. Source ID
2. 原始 URL
3. 主要知識
4. 可支撐的教學內容
5. 注意事項
6. 對應 Wiki 章節

若 Wiki generation 發現來源不足，應回到 source retrieval，而不是直接用模型記憶補完。
