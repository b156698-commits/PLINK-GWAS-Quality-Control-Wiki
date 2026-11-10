# Wiki Query Log — Run 01

- **Date:** 2026-11-10
- **Goal:** 從既有 LLM Wiki 產生初學者可理解的教學 HTML 簡報大綱
- **Knowledge source:** `wiki/`
- **Rule:** 簡報內容只能使用 Wiki 已支撐的知識；若查不到，就不能直接由模型記憶補寫。

---

## Query 1 — 初學者在開始 GWAS QC 前，需要先理解什麼？

### Retrieved Wiki
- `wiki/01-plink-basics.md`

### Retrieved points
- PLINK binary fileset 由 `.bed/.bim/.fam` 組成。
- 三個檔案共用 prefix。
- `--bfile study` 代表讀取這一組資料，而不是單一檔案。

### Presentation use
- Slide 2：PLINK 輸入資料與分析起點

---

## Query 2 — Missingness QC 要教哪些核心概念？

### Retrieved Wiki
- `wiki/02-missingness.md`

### Retrieved points
- variant-level missingness → `--geno`
- sample-level missingness → `--mind`
- threshold 必須視為分析設定，不應稱為所有研究的固定標準。

### Presentation use
- Slide 4：Missingness — 先移除品質太差的 variant / sample

---

## Query 3 — MAF 與 HWE 如何向初學者解釋？

### Retrieved Wiki
- `wiki/03-maf-hwe.md`

### Retrieved points
- `--maf` 依 minor allele frequency 篩選 variants。
- `--hwe` 依 HWE exact-test p-value 篩選。
- `0.01`、`1e-6` 等值只能當示範。
- 過於嚴格的 HWE filtering 可能排除 genuine association signals。

### Presentation use
- Slide 5：MAF & HWE

---

## Query 4 — LD pruning 在 workflow 中扮演什麼角色？

### Retrieved Wiki
- `wiki/04-ld-pruning.md`

### Retrieved points
- `--indep-pairwise <window> <step> <r2>`
- `.prune.in` = retained variants
- `.prune.out` = excluded variants
- LD-pruned set 常用於 PCA / relatedness。
- 不應把「LD pruning」誤解成最終 association scan 只能測 pruning 後 SNP。

### Presentation use
- Slide 6：LD Pruning

---

## Query 5 — Relatedness 要教哪些指標？

### Retrieved Wiki
- `wiki/05-relatedness.md`

### Retrieved points
- PLINK `--genome` 可做 pairwise IBD estimation。
- IBD calculation 本身不 LD-aware，因此通常先 pruning。
- `PI_HAT = Z2 + 0.5 × Z1`
- 哪一個 related sample 應移除，仍要由研究規則決定。

### Presentation use
- Slide 7：Relatedness / PI_HAT

---

## Query 6 — PCA 為什麼需要出現在 GWAS 教學中？

### Retrieved Wiki
- `wiki/06-pca.md`

### Retrieved points
- PCA 用來描述 genotype data 中主要 population structure。
- `--pca` 產生 `.eigenvec` / `.eigenval`。
- top PCs 常作為 association regression covariates。
- PLINK 預設輸出 20 PCs，不代表模型一定要使用 20 個 PCs。

### Presentation use
- Slide 8：PCA / Population Structure

---

## Query 7 — Association Analysis 能教到多完整？

### Retrieved Wiki
- `wiki/07-association.md`

### Retrieved points
- case-control phenotype 可用 `--logistic`
- phenotype file：`FID IID STATUS`
- covariate file：`FID IID AGE SEX PC1 PC2 PC3`
- `--pheno-name` / `--covar-name`
- PLINK 1.9 常見 case-control coding：1=control、2=case
- `.assoc.logistic` 可包含 OR / P 等欄位
- LD-pruned SNP set 不應被自動當作完整 genome-wide association set

### Presentation use
- Slide 9：Association Analysis

---

## Query 8 — 結果判讀要讓初學者學會什麼？

### Retrieved Wiki
- `wiki/08-gwas-results.md`

### Retrieved points
- GWAS 有 multiple-testing problem。
- `P < 5 × 10^-8` 可作為常見 genome-wide significance convention 的教學例子。
- Manhattan Plot：x = chromosome / position；y = `-log10(P)`
- QQ Plot：比較 observed 與 null expected distribution。
- QQ deviation 不能單獨證明是哪一種問題。
- association ≠ causality

### Presentation use
- Slide 10：Significance + Manhattan Plot
- Slide 11：QQ Plot + 結果解讀

---

# Query Result

Wiki 足以支撐一份 11 張投影片的初學者教學簡報。

## Content intentionally not added

以下內容本輪不加入簡報，因為目前 Wiki 沒有足夠來源支撐，或會使初學者簡報過度延伸：

- suggestive significance 的固定 threshold
- genomic inflation factor λGC 的完整教學
- imputation workflow
- mixed-model GWAS
- PRS
- fine-mapping

這些內容若之後要加入，必須先補 source，再更新 Wiki。
