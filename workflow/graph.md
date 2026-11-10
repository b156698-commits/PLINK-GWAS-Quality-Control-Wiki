# Loop / Graph Design

## Current Workflow

```text
[取得資料]
     ↓
[Ingest 到 raw/]
     ↓
[建立 / 更新 Wiki]
     ↓
[Source Coverage Check]
     │
     ├── FAIL ──→ [補找來源]
     │                ↓
     │           [重新 ingest]
     │                ↓
     └────────── [重新生成 Wiki]
                      ↓
                    PASS
                      ↓
               [查詢 Wiki]
                      ↓
             [整理教學重點]
                      ↓
             [Content Check]
     │
     ├── FAIL ──→ 回到「查詢 Wiki」
     ↓ PASS
          [產生 HTML 簡報]
                 ↓
        [Presentation Check]
     │
     ├── FAIL ──→ 回到「整理教學重點」
     ↓ PASS
               [完成]
```

## 已實際執行的 loop

第一次 Wiki generation 時，Association Analysis 的 exact phenotype/covariate format 沒有足夠來源支撐。

因此實際走過：

```text
Wiki generation
→ Source Coverage Check = FAIL
→ 補找 PLINK 官方來源
→ ingest S08
→ validate
→ regenerate Association Wiki
→ Source Coverage Check = PASS
```

## 為什麼把 Source Coverage Check 放在簡報前？

因為 Wiki 是簡報的知識來源。

如果 Wiki 中已經有 unsupported content，之後生成 HTML 簡報時會把錯誤一起放大。

因此先在 Wiki 層檢查，可以降低後續重做整份簡報的成本。
