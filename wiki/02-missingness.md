# 02 Missingness QC

## 核心概念

GWAS genotype data 中可能會有 missing genotype。

Missingness 可以從兩個方向檢查：

1. **Variant-level missingness**
2. **Sample-level missingness**

PLINK 分別提供：

```bash
--geno
--mind
```

## Variant-level：`--geno`

`--geno` 用來移除 missing call rate 超過指定門檻的 variants。

概念上可寫成：

```bash
plink --bfile study --geno <threshold> --make-bed --out qc_geno
```

## Sample-level：`--mind`

`--mind` 用來移除 missing genotype rate 過高的 samples。

概念上可寫成：

```bash
plink --bfile qc_geno --mind <threshold> --make-bed --out qc_mind
```

## 為什麼要檢查 missingness？

如果某些 variants 或 samples 有大量缺失資料，後續分析的可靠性可能受到影響，因此通常會先進行 missingness QC。

## Threshold 注意事項

PLINK 文件包含預設參數值，但：

> **PLINK default ≠ 所有 GWAS 研究都適用的固定 QC 標準。**

例如課堂或分析流程中看到的：

```bash
--geno 0.02
--mind 0.02
```

應視為分析設定範例；實際門檻需依研究設計與資料品質決定。

## Sources

- **S02** — PLINK 1.9 Input Filtering
