# 08 GWAS Results

完成 association analysis 後，通常需要回答：

1. 哪些 variants 的 association signal 最強？
2. 整體 p-value distribution 是否合理？
3. 是否有達到 genome-wide significance 的 signals？

---

## 1. 為什麼不能只看 P < 0.05？

GWAS 同時會檢驗大量 genetic variants。

如果每個 test 都單獨以 `P < 0.05` 判定，就會出現嚴重的 multiple-testing problem。

因此 GWAS 需要更嚴格的 significance criterion。

---

## 2. Genome-wide Significance

S07 的 GWAS methods example 使用：

```text
P < 5 × 10^-8
```

作為 genome-wide significance threshold。

這是一個廣泛使用的 GWAS convention，但教學時仍不應把它描述為所有 genetic analysis 都不可更動的數學定律。

---

## 3. Manhattan Plot

Manhattan Plot 常用來呈現整個 genome 的 association results。

### X 軸

Chromosome / genomic position。

### Y 軸

通常為：

```text
-log10(P)
```

因此 p-value 越小，點的位置越高。

### 怎麼看？

如果某個 genomic region 出現一群很高的 points，代表該區域存在較強的 association signals。

但是：

> statistical association ≠ causality

顯著結果仍需要進一步研究與 replication。

---

## 4. QQ Plot

QQ Plot 會比較：

- null hypothesis 下預期的 association statistics
- 實際觀察到的 association statistics

如果大部分 points 接近 null expectation，而只有 strongest signals 在尾端偏離，可能代表存在真正的 association signals。

若大量 points 很早就系統性偏離 expectation，則應進一步檢查是否可能存在：

- population structure
- relatedness
- technical artifacts
- 或其他造成 test statistic distribution 改變的因素

但：

> QQ Plot 的偏離不能單獨證明是哪一種問題造成。

---

## 5. Manhattan Plot 與 QQ Plot 的角色

這兩種圖主要是：

> **GWAS results visualization / interpretation**

而不是 QC command 本身。

它們與前面的 PLINK QC workflow 有關，但應與：

- `--geno`
- `--maf`
- `--hwe`
- `--indep-pairwise`

這些 QC commands 分開理解。

## Sources

- **S07** — Basic statistical analysis in genetic case-control studies
