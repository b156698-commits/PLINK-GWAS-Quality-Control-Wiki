# 04 LD Pruning

## 核心概念

鄰近 genetic variants 之間可能存在 linkage disequilibrium（LD）。

某些分析，例如 PCA 或 relatedness analysis，通常希望使用較接近 linkage equilibrium 的 variant subset，因此可以先進行 LD pruning。

PLINK 提供：

```bash
--indep-pairwise
```

## 基本語法

```bash
plink --bfile qc_data --indep-pairwise <window> <step> <r2> --out ld
```

三個核心參數為：

1. **window size**
2. **step size**
3. **pairwise r² threshold**

例如：

```bash
plink --bfile qc_data --indep-pairwise 50 5 0.2 --out ld
```

`50 5 0.2` 應視為一組常見的示範設定，不是所有資料都應固定使用。

## 輸出檔案

主要會得到：

```text
ld.prune.in
ld.prune.out
```

其中：

- `.prune.in`：保留下來的 variants
- `.prune.out`：被 pruning 排除的 variants

後續可以搭配：

```bash
--extract ld.prune.in
```

建立 LD-pruned dataset。

## 重要提醒

LD-pruned variants 常用於：

- PCA
- relatedness / IBD

但這不代表最後 GWAS association testing 一定只能使用 pruning 後的 SNP subset。

正式 association scan 通常仍需依研究設計決定要使用哪些 post-QC variants。

## Sources

- **S03** — PLINK 1.9 Linkage Disequilibrium
