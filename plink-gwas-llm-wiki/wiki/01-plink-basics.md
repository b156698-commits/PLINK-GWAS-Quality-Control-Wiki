# 01 PLINK Basics

## 核心概念

PLINK 1.9 常使用一組三個檔案組成的 binary fileset：

- `.bed`：binary genotype data
- `.bim`：variant information
- `.fam`：sample / family information

三個檔案會共用相同的 prefix。例如：

```text
study.bed
study.bim
study.fam
```

在 PLINK 中可用：

```bash
plink --bfile study
```

一次指定這組資料。

## 為什麼這一步重要？

GWAS 分析需要同時掌握：

- 個體（sample）
- 遺傳變異（variant）
- genotype data

因此，在正式進入 QC 前，要先確認輸入檔案是否正確，以及 PLINK 能否成功讀取資料。

## 初學者應先理解

`--bfile study` 的意思不是指定單一檔案，而是指定：

```text
study.bed
study.bim
study.fam
```

這三個具有相同 prefix 的檔案。

## 注意事項

這一章只介紹基本資料輸入，不討論 QC threshold。

## Sources

- **S01** — PLINK 1.9 Standard Data Input
