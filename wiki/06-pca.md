# 06 PCA / Population Structure

## 為什麼 GWAS 需要 PCA？

不同 ancestral background 的 samples 可能存在 systematic genetic differences。

如果 phenotype 與 population structure 同時相關，就可能產生 confounding。

PCA（Principal Component Analysis）常被用來描述 genotype data 中主要的 population structure。

## PLINK 指令

```bash
plink --bfile ld_pruned --pca --out pca
```

PLINK 1.9 的 `--pca` 預設輸出 top 20 principal components，也可以指定數量，例如：

```bash
plink --bfile ld_pruned --pca 10 --out pca
```

## 主要輸出

```text
pca.eigenvec
pca.eigenval
```

### `.eigenvec`

包含每個 sample 的 principal component scores。

例如：

```text
PC1
PC2
PC3
...
```

### `.eigenval`

包含對應 principal components 的 eigenvalues。

## PCA 在 association analysis 中的用途

PLINK 官方文件指出，top PCs 常被加入 association regression 中作為 covariates，以協助校正 population stratification。

例如概念上：

```text
Disease status ~ SNP + Age + Sex + PC1 + PC2 + PC3
```

## 重要提醒

`--pca` 預設輸出 20 PCs：

> 不代表每個 GWAS 都必須把 20 個 PCs 全部放進 association model。

實際使用多少 PCs 是研究設計與模型選擇問題。

## Sources

- **S05** — PLINK 1.9 Population Stratification
