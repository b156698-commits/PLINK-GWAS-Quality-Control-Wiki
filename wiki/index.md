# PLINK / GWAS Quality Control Wiki

這份 Wiki 目前由 8 份來源資料支撐，主要提供後續教學 HTML 簡報使用。

## Learning Path

```text
PLINK Basics
    ↓
Missingness
    ↓
MAF & HWE
    ↓
LD Pruning
    ↓
Relatedness
    ↓
PCA / Population Structure
    ↓
Association Analysis
    ↓
GWAS Results
```

## Chapters

1. [PLINK Basics](01-plink-basics.md)
2. [Missingness QC](02-missingness.md)
3. [MAF & HWE](03-maf-hwe.md)
4. [LD Pruning](04-ld-pruning.md)
5. [Relatedness / PI_HAT](05-relatedness.md)
6. [PCA / Population Structure](06-pca.md)
7. [Association Analysis](07-association.md)
8. [GWAS Results](08-gwas-results.md)

## Source Mapping

| Wiki chapter | Source IDs |
|---|---|
| PLINK Basics | S01 |
| Missingness | S02 |
| MAF & HWE | S02 |
| LD Pruning | S03 |
| Relatedness / PI_HAT | S04 |
| PCA / Population Structure | S05 |
| Association Analysis | S05, S06, S08 |
| GWAS Results | S07 |

## Generation Rule

Wiki 內容只能使用 raw sources 能支撐的資訊。

如果某個教學內容尚未獲得來源支撐，應直接標記「尚待驗證」，而不是由模型自行補完。

## Important QC Principle

範例 threshold、PLINK default 與研究中的實際 QC threshold 必須分開。

例如：

```text
--geno 0.02
--maf 0.01
--hwe 1e-6
--indep-pairwise 50 5 0.2
```

可以作為教學範例，但不得自動稱為所有 GWAS 都必須使用的固定標準。
