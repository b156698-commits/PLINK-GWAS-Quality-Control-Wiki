# 03 MAF & HWE

## 1. Minor Allele Frequency（MAF）

MAF 是 minor allele 在資料中的頻率。

PLINK 可用：

```bash
--maf <threshold>
```

移除 MAF 低於指定門檻的 variants。

例如：

```bash
plink --bfile qc_mind --maf 0.01 --make-bed --out qc_maf
```

這裡的 `0.01` 應視為**範例值**，不是每個 GWAS 都必須使用的固定標準。

---

## 2. Hardy-Weinberg Equilibrium（HWE）

PLINK 可以用：

```bash
--hwe <p-value>
```

根據 HWE exact test 的 p-value 篩選 variants。

概念範例：

```bash
plink --bfile qc_maf --hwe 1e-6 --make-bed --out qc_hwe
```

同樣地，`1e-6` 是一個分析範例，不應寫成所有研究都必須使用的固定門檻。

## 為什麼 HWE threshold 不能隨便設得很嚴？

PLINK 官方文件提醒，真正與 phenotype 有關的 variants 也可能出現 HWE deviation，因此使用過於嚴格的 HWE filtering 可能造成不必要的排除。

PLINK 也提供如：

- `midp`
- `include-nonctrl`

等 modifier。

## 重點

MAF 與 HWE 都是常見 QC 概念，但門檻設定要依研究設計與資料特性決定。

## Sources

- **S02** — PLINK 1.9 Input Filtering
