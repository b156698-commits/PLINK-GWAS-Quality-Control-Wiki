# HTML Generation Log — Run 01

- **Date:** 2026-11-10
- **Input:** `presentation/outline.md`
- **Output:** `presentation/index.html`, `presentation/style.css`

## Design decisions

1. 使用單一 HTML 檔搭配單一 CSS 檔，方便直接上傳 GitHub Pages。
2. 每一頁簡報使用一個 `<section class="slide">`。
3. 提供：
   - 左右切換按鈕
   - 側邊 slide navigation
   - 鍵盤左右方向鍵切換
4. 視覺風格延續前一週網站的柔和風格：
   - 奶油白背景
   - 淡藍 / 淡綠卡片
   - 簡潔的 DNA / plot 示意圖
5. 所有內容都從 `presentation/outline.md` 轉入，不額外加入未經 Wiki 支撐的新知識。

## Slide count

- Total slides: 11

## Traceability

- Slide 2 ← `wiki/01-plink-basics.md`
- Slide 4 ← `wiki/02-missingness.md`
- Slide 5 ← `wiki/03-maf-hwe.md`
- Slide 6 ← `wiki/04-ld-pruning.md`
- Slide 7 ← `wiki/05-relatedness.md`
- Slide 8 ← `wiki/06-pca.md`
- Slide 9 ← `wiki/07-association.md`
- Slide 10–11 ← `wiki/08-gwas-results.md`
