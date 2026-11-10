# 07 Association Analysis

## 核心概念

完成基本 QC 與 population structure 處理後，可以進一步檢驗 genetic variants 與 phenotype 之間是否存在 association。

對 case-control phenotype，PLINK 1.9 可使用：

```bash
--logistic
```

執行 logistic regression，並可加入 covariates。

---

## 1. Phenotype file

PLINK 1.9 可用：

```bash
--pheno phenotype.txt
```

從外部檔案讀入 phenotype。

基本格式的前兩欄必須是：

```text
FID IID
```

預設情況下，PLINK 從第 3 欄讀取 phenotype。

例如：

```text
FID IID STATUS
F001 I001 1
F001 I002 2
F002 I003 2
```

如果檔案有 header，可以用：

```bash
--pheno-name STATUS
```

指定 phenotype 欄位。

使用 `--pheno-name` 時，header 的前兩個欄位必須是 `FID`、`IID`。

### Case/control coding

PLINK 1.9 一般 case/control coding 為：

- `1` = control
- `2` = case
- `0` = 可作為 missing value
- missing phenotype 通常以 `-9` 表示

如果使用：

```bash
--1
```

則改為：

- `0` = control
- `1` = case

因此在 association analysis 前，一定要確認 phenotype coding。

---

## 2. Covariate file

Covariates 可用：

```bash
--covar covariates.txt
```

載入。

基本格式同樣以：

```text
FID IID
```

作為前兩欄，後面的欄位則是 covariates。

例如：

```text
FID IID AGE SEX PC1 PC2 PC3
F001 I001 70 1 -0.012 0.031 -0.004
F001 I002 66 2  0.008 0.022  0.011
F002 I003 74 1 -0.020 0.015  0.006
```

如果有 header，可以使用：

```bash
--covar-name AGE,SEX,PC1-PC3
```

指定要放入模型的 covariates。

這裡的：

```text
AGE、SEX、PC1–PC3
```

只是教學範例。

實際 covariate 選擇必須依研究設計決定。

### Missing covariates

PLINK 預設情況下，如果 sample 的任一 covariate 缺失，該 sample 的主要 phenotype 會被視為 missing 而無法進入該次 regression。

因此執行 GWAS 前應檢查 phenotype、covariates 與 genotype sample IDs 是否一致且完整。

---

## 3. Logistic regression

概念模型可以表示為：

```text
Disease status
    ~ SNP
    + Age
    + Sex
    + PC1
    + PC2
    + PC3
```

其中 PCs 常被用來協助校正 population stratification。

一個完整的 PLINK 教學範例為：

```bash
plink   --bfile qc_final   --pheno phenotype.txt   --pheno-name STATUS   --covar covariates.txt   --covar-name AGE,SEX,PC1-PC3   --logistic hide-covar   --out gwas_logistic
```

`hide-covar` 會讓主要 association report 不額外列出每個 covariate 的 test rows。

如果使用：

```bash
--logistic beta
```

則 logistic regression report 會輸出 regression coefficient，而不是 odds ratio。

---

## 4. `.assoc.logistic` output

`--logistic` 會產生：

```text
gwas_logistic.assoc.logistic
```

常見欄位包括：

| 欄位 | 意義 |
|---|---|
| `CHR` | chromosome |
| `SNP` | variant ID |
| `BP` | base-pair position |
| `A1` | allele 1 |
| `TEST` | test identifier |
| `NMISS` | genotype、phenotype、covariates 都非 missing 的 observations |
| `OR` | odds ratio；若使用 `--logistic beta` 則為 `BETA` |
| `STAT` | test statistic |
| `P` | asymptotic p-value |

---

## 5. Odds Ratio 基本解讀

在 logistic regression 下：

- OR > 1：A1 與較高 disease odds 相關
- OR < 1：A1 與較低 disease odds 相關
- OR = 1：沒有 odds difference

但實際解讀前，一定要確認：

- A1 是哪一個 allele
- phenotype coding
- covariates
- analysis model

association 不等於 causality。

---

## 6. 關於 LD-pruned dataset

LD-pruned variants 常被用於：

- PCA
- relatedness estimation

但是最終 GWAS association scan：

> 不應在沒有研究設計理由的情況下，只對 LD-pruned SNP subset 進行完整 genome-wide testing。

最終測試的 variant set 應由完整 QC workflow 與研究目的決定。

---

## Source-retrieval loop note

Wiki Generation 01 原本發現 phenotype / covariate 的精確格式缺乏來源支撐，因此沒有直接生成。

之後回到 source retrieval，新增 **S08** 官方文件後，本章才補上：

- phenotype file format
- covariate file format
- `--pheno-name`
- `--covar-name`
- case/control coding
- `.assoc.logistic` fields

這是本專案第一次實際執行的 retrieval → validate → regenerate loop。

## Sources

- **S05** — PLINK 1.9 Population Stratification
- **S06** — PLINK 1.9 Association Analysis
- **S08** — PLINK 1.9 Phenotype and Covariate Input / File Format Reference
