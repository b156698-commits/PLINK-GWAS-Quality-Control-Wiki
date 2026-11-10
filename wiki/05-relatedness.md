# 05 Relatedness / PI_HAT

## 核心概念

GWAS sample 中如果存在高度相關或重複個體，可能影響某些統計分析。

PLINK 1.9 可使用：

```bash
--genome
```

進行 pairwise IBS / IBD 計算。

## 為什麼先做 LD pruning？

PLINK 官方文件指出，其 IBD calculation 本身**不是 LD-aware**。

因此進行 relatedness estimation 前，通常會先使用 LD-pruned variants。

## `.genome` 中的重要欄位

### Z0
兩個 samples 分享 0 個 allele IBD 的估計機率。

### Z1
分享 1 個 allele IBD 的估計機率。

### Z2
分享 2 個 allele IBD 的估計機率。

### PI_HAT

PLINK 文件中的關係為：

```text
PI_HAT = Z2 + 0.5 × Z1
```

PI_HAT 可用來描述 pairwise relatedness。

## 基本指令概念

```bash
plink --bfile ld_pruned --genome --out relatedness
```

PLINK 也提供 `--min`、`--max` 等參數，依 PI_HAT 篩選輸出 pair。

## 重要提醒

沒有一個 PI_HAT cutoff 能直接套用到所有研究。

另外：

> `--genome` 會提供 pairwise information，但「兩個相關個體中要移除哪一個」仍需要研究者另外制定規則。

## Sources

- **S04** — PLINK 1.9 Identity-by-Descent
