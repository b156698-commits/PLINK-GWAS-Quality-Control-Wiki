# Presentation Content Check — Run 01

- **Date:** 2026-11-10
- **Input:** `workflow/wiki-query-log-01.md`
- **Candidate output:** `presentation/outline.md`
- **Check performed before HTML generation**

## Check 1 — 每張教學投影片是否能追到 Wiki？

| Slide | Topic | Wiki mapping | Result |
|---|---|---|---|
| 1 | Overview | `wiki/index.md` | PASS |
| 2 | PLINK Basics | `01-plink-basics.md` | PASS |
| 3 | QC Workflow | `index.md` + chapters | PASS |
| 4 | Missingness | `02-missingness.md` | PASS |
| 5 | MAF & HWE | `03-maf-hwe.md` | PASS |
| 6 | LD Pruning | `04-ld-pruning.md` | PASS |
| 7 | Relatedness | `05-relatedness.md` | PASS |
| 8 | PCA | `06-pca.md` | PASS |
| 9 | Association | `07-association.md` | PASS |
| 10 | Manhattan / significance | `08-gwas-results.md` | PASS |
| 11 | QQ Plot | `08-gwas-results.md` | PASS |

## Check 2 — 是否出現 Wiki 沒有支撐的內容？

### Result
PASS

本輪刻意不加入：

- suggestive threshold
- λGC 完整教學
- imputation
- mixed models
- PRS
- fine-mapping

因為它們不是目前 Wiki 的主要支撐範圍。

## Check 3 — Threshold 是否被寫成 universal rule？

### Result
PASS

簡報大綱中：

- `--geno 0.02`
- `--maf 0.01`
- `--hwe 1e-6`
- `--indep-pairwise 50 5 0.2`

皆明確標示為範例或示範。

`P < 5 × 10^-8` 則描述為常見 GWAS convention，而不是所有 genetic analysis 都固定不變的定律。

## Check 4 — LD-pruned SNP 是否被錯誤用於 final GWAS？

### Result
PASS

Slide 6 明確提醒：

> LD-pruned set 常用於 PCA / relatedness，但不要直接推論 final GWAS 只能測 pruning 後 SNP。

## Check 5 — Association exact format 是否已有來源？

### Result
PASS

Slide 9 的 phenotype / covariate format 與完整 command 來自 source-retrieval loop 後新增的 S08。

## Check 6 — Wiki metadata consistency

### Initial result
FAIL

查詢 Wiki 時發現：

`wiki/index.md` 第一行仍寫「由 7 份來源資料生成」，但 source-retrieval loop 後實際已有 **8 份**來源。

### Action
在進入 HTML generation 前，立即把：

```text
7 份來源資料
```

修正為：

```text
8 份來源資料
```

### Recheck
PASS

## Why this matters

這是一個新的實際檢查案例：

```text
Query Wiki
→ Content check
→ Metadata inconsistency found
→ Fix Wiki before HTML generation
→ Recheck = PASS
```

如果檢查放到 HTML 完成後，錯誤的 source count 可能已經被複製到簡報或 README。

因此這再次支持：

> **檢查應盡量放在生成最終成品之前。**

## Decision

Presentation outline **approved for HTML generation**.
