# 教學 HTML 簡報大綱

## 題目

**從 Genotype Data 到 GWAS Results：初學者的 PLINK / GWAS QC 流程**

## 目標受眾

原本不熟悉 PLINK / GWAS QC 的初學者。

## 教學目標

看完簡報後，學習者應能：

1. 說明 PLINK `.bed/.bim/.fam` 的基本角色。
2. 理解 Missingness、MAF、HWE、LD pruning、Relatedness、PCA 的用途。
3. 知道 case-control association analysis 的基本資料與模型概念。
4. 初步看懂 Manhattan Plot 與 QQ Plot。
5. 知道 QC threshold 與 covariate 設定不是所有研究都固定相同。

---

# Slide 1 — Title

## 標題
從 Genotype Data 到 GWAS Results

## 副標題
初學者的 PLINK / GWAS Quality Control 流程

## 畫面
- DNA / chromosome 簡潔插圖
- 一條從 genotype → QC → association → results 的流程線

## 教學目的
先建立完整地圖，讓初學者知道後面每一步在整個流程中的位置。

## Wiki
- `wiki/index.md`

---

# Slide 2 — PLINK 從什麼資料開始？

## 核心訊息
PLINK binary fileset 通常由三個共用 prefix 的檔案構成：

```text
study.bed
study.bim
study.fam
```

指令：

```bash
plink --bfile study
```

## 教學重點
- `.bed`：genotype data
- `.bim`：variant information
- `.fam`：sample / family information
- `--bfile study` 不是指單一檔案

## Wiki / Sources
- `wiki/01-plink-basics.md`
- S01

---

# Slide 3 — 為什麼 GWAS 要先做 QC？

## 核心訊息
在測試 SNP 與 phenotype 的 association 前，要先降低資料品質、相關樣本、population structure 等問題造成的影響。

## 視覺流程

```text
Genotype Data
↓
Missingness
↓
MAF & HWE
↓
LD Pruning
↓
Relatedness
↓
PCA
↓
Association
↓
GWAS Results
```

## 特別提醒
這是一條「教學流程」，不是宣稱所有研究只能使用完全相同的順序或 threshold。

## Wiki
- `wiki/index.md`
- `wiki/02-missingness.md` ～ `wiki/08-gwas-results.md`

---

# Slide 4 — Missingness：先找缺失過多的資料

## 左側
### Variant-level
`--geno`

移除 missing call rate 太高的 variants。

## 右側
### Sample-level
`--mind`

移除 missing genotype rate 太高的 samples。

## Example
```bash
plink --bfile study --geno 0.02 --make-bed --out qc_geno
```

## 必須顯示的提醒
**0.02 是教學範例，不是 universal threshold。**

## Wiki / Sources
- `wiki/02-missingness.md`
- S02

---

# Slide 5 — MAF & HWE：檢查 variant 品質

## MAF
```bash
--maf <threshold>
```

低頻 variants 的處理要依研究設計決定。

## HWE
```bash
--hwe <p-value>
```

HWE deviation 可以是 QC 警訊，但 overly strict filtering 也可能造成不必要排除。

## Example
```bash
--maf 0.01
--hwe 1e-6
```

## 提醒
兩個數值皆為示範。

## Wiki / Sources
- `wiki/03-maf-hwe.md`
- S02

---

# Slide 6 — LD Pruning：建立較獨立的 SNP subset

## 指令
```bash
--indep-pairwise <window> <step> <r2>
```

## Example
```bash
--indep-pairwise 50 5 0.2
```

## Output
```text
.prune.in
.prune.out
```

## 教學重點
LD-pruned set 常用於：
- PCA
- Relatedness

但：
**不要直接推論 final GWAS 只能測 pruning 後 SNP。**

## Wiki / Sources
- `wiki/04-ld-pruning.md`
- S03

---

# Slide 7 — Relatedness：樣本之間是不是太相似？

## 核心公式
```text
PI_HAT = Z2 + 0.5 × Z1
```

## PLINK
```bash
--genome
```

## 教學重點
- relatedness estimation 前通常先做 LD pruning
- PI_HAT 描述 pairwise relatedness
- cutoff 及「要刪哪一個 sample」不是 PLINK 自動替研究者決定

## Wiki / Sources
- `wiki/05-relatedness.md`
- S04

---

# Slide 8 — PCA：處理 Population Structure

## 問題
不同 ancestry 的 systematic genetic differences 可能造成 confounding。

## PLINK
```bash
--pca
```

## Output
```text
.eigenvec
.eigenval
```

## Association model 概念
```text
Disease ~ SNP + Age + Sex + PC1 + PC2 + PC3
```

## 提醒
PLINK 預設輸出 20 PCs，不代表一定要使用 20 PCs。

## Wiki / Sources
- `wiki/06-pca.md`
- S05

---

# Slide 9 — Association Analysis：SNP 與疾病有沒有關聯？

## Phenotype
```text
FID IID STATUS
```

PLINK 1.9 常見 case/control：
- 1 = control
- 2 = case

## Covariates
```text
FID IID AGE SEX PC1 PC2 PC3
```

## Example command
```bash
plink   --bfile qc_final   --pheno phenotype.txt   --pheno-name STATUS   --covar covariates.txt   --covar-name AGE,SEX,PC1-PC3   --logistic hide-covar   --out gwas_logistic
```

## 教學重點
- `OR > 1` / `OR < 1` 必須配合 effect allele 解讀
- covariates 依研究設計決定
- association ≠ causality

## Wiki / Sources
- `wiki/07-association.md`
- S05, S06, S08

---

# Slide 10 — Manhattan Plot：全基因組哪裡有強訊號？

## Multiple Testing
GWAS 同時檢驗大量 variants，所以不能只用一般的 `P < 0.05` 思考。

## 常見 convention
```text
P < 5 × 10^-8
```

## Manhattan Plot
- X：chromosome / genomic position
- Y：`-log10(P)`
- 點越高 → p-value 越小

## 提醒
Genome-wide significance 不等於 causality。

## Wiki / Sources
- `wiki/08-gwas-results.md`
- S07

---

# Slide 11 — QQ Plot 與整體結果判讀

## QQ Plot
比較：
- null 下 expected association statistics
- observed association statistics

## 如何讀？
- 多數 points 接近 expectation：整體較合理
- strongest tail departure：可能有 association signal
- 大量 points 很早偏離：需要檢查 population structure、relatedness、technical artifacts 等

## 關鍵提醒
QQ deviation **不能單獨證明**是哪一個問題造成。

## Closing summary
```text
Input
→ QC
→ Population / Relatedness checks
→ Association
→ Results interpretation
```

## Wiki / Sources
- `wiki/08-gwas-results.md`
- S07
