# PICT 前端統一樣式標準（記錄）

此文件整理目前已執行並約定的「統一標準」，方便後續維護、擴充與審查一致性。

---
## 1. 色彩系統（CSS 變數）
:root 定義（各頁若缺請補）：
- --primary: #0f766e  （主品牌色 / 漸層起點）
- --secondary: #e0f7f6 （淺底/重點背景）
- --background: #f8fafc （全站頁面底色）
- --text: #1f2937 （主文字）
- --highlight: #fef3c7 （提示 / 輔助強調）

使用原則：
- 需要高反差 CTA / Hero：漸層 linear-gradient(135deg,#0f766e,#0d9488)
- 區塊輕度強調：--secondary 背景 + 左側主色邊框

---
## 2. 字體與排版層級（Global Typography）
全站（style.css 已設）：
- Base font-family: 'Noto Sans TC', 'Segoe UI', system-ui, -apple-system, 'Microsoft JhengHei', sans-serif
- h1–h6：font-weight:700；letter-spacing:.5px；line-height:1.25
- html 基礎字級：16px（≥1280px 時 17px）

標題縮放（clamp）：
- h1: clamp(2rem, 1.4rem + 2.1vw, 3rem)
- h2: clamp(1.55rem, 1.2rem + 1.2vw, 2.3rem)
- h3: clamp(1.15rem, 1rem + .6vw, 1.55rem)
- .section-title.small: clamp(1.3rem,1.05rem + .9vw,1.8rem)
- 輔助標題 .section-sub: clamp(1rem,.9rem + .4vw,1.2rem) / font-weight:600

Hero（統一）
- .header h1: clamp(1.9rem,1.3rem + 1.9vw,2.6rem); line-height:1.18; letter-spacing:.8px; font-weight:700
- .header p: clamp(1.05rem,.95rem + .5vw,1.35rem); line-height:1.5; letter-spacing:.5px; margin:0

語意特例：section-5-5 使用 h2 但視覺需等同 .header h1，採用同一組 clamp；副標使用同一組 .header p clamp。

行距：一般段落 line-height 約 1.7–1.8；Hero 副標 1.5；表格內容 1.55。

---
## 3. Hero 區塊（Header）
結構：
```
<div class="header">
  <h1>主要標題</h1>
  <p>副標簡述</p>
</div>
```
樣式要點：
- 背景漸層：linear-gradient(135deg,#0f766e,#0d9488)
- 內距：桌機常用 48–60px Y；手機可縮至 ~36px
- 文字顏色固定白色；避免再個別設定 font-size（交由全域）

---
## 4. 區塊標題（Section Title）
```
<h2 class="section-title">標題</h2>
```
- 左側 6px 寬主色邊框 + 漸層淡背景（style.css 已含）
- 嚴禁覆寫 font-size；若需較小版本用 .section-title.small

---
## 5. 按鈕 & CTA（Buttons / CTA）
基礎按鈕（白底深綠字）：
```
<a class="btn" ...>文字</a>
```
- 背景：#fff；字色 var(--primary)；font-weight:700；圓角 12px；padding:14px 26px
- Hover：上移 -3px + 陰影增強

Outline 變體：.btn.outline
- 半透明白背景 + 2px 半透明白框 + backdrop-filter: blur(4px)

LINE 變體：.btn.line
- 背景 #06c755；白字；加強陰影 hover

CTA 區容器：.cta
- 漸層背景（同 Hero）、text-align:center、padding: (桌機) 42px 24px / (手機) 36px 18px
- 內部主標題 h2 font-size:30px（手機 24px）除非改用全域 clamp（未來可考慮統一）

事件追蹤（GA Data 屬性）：
- data-ga-category="CTA"
- data-ga-action="click" 或 "download"
- data-ga-label="語意識別字串"

ARIA：
- 需開新分頁 target="_blank" 時加 rel="noopener noreferrer" & aria-label 描述動作

---
## 6. 規格 / 資料表格（.spec-table）
結構：table + caption（若需要標題說明）
統一樣式重點：
- border-collapse: separate + border-spacing:0
- 字級：clamp(.9rem,.84rem + .25vw,1rem)
- th：線性漸層背景 linear-gradient(135deg,var(--secondary),#f0fffd)
- th, td：padding 約 11px 18px（手機改 10px 12px）
- 第一欄 (td:first-child) font-weight:600, color:#0f5c55
- 偶數列淡底 (#f9fafb)，hover 行底色 #f1f5f9
- 四角圓角：首列首欄 / 首列末欄 / 末列首欄 / 末列末欄
- 手機：縮小字級與 padding，保持可讀性，允許橫向滾動（外層 .table-wrap overflow-x:auto）

---
## 7. 卡片與資訊盒
- .card：2px 邊框 #e2e8f0，hover 變主色；圓角 12px；padding:18px
- .highlight / .highlight-box：主色左邊框 5px + 次色背景；字體 font-weight:600 或 bold
- .success：綠色背景 #f0fdf4 + 左側 #22c55e 邊框

---
## 8. 圖片 Gallery
- 外層 .image-gallery：白底、圓角 12px、陰影、內距 12px 0（手機縮小）
- 圖片預設 width:92%（超寬螢幕再縮至 85%）；手機寬度 100%
- 圖片間距 margin-bottom:26px（手機 20px）

---
## 9. 無障礙與 ALT 文案規則
ALT 撰寫原則：
1. 具體：描述圖像功能或呈現的關鍵資訊（例如「技術流程圖：展示光離子催化從 UV 到自由基生成過程」）。
2. 避免贅述：不寫「圖片：」開頭。
3. 若為純裝飾且無資訊價值，可用空 alt=""。
4. 統一語言：繁體中文；專有名詞保留英文（例如 VOCs, PICT）。
5. 場景圖：提及用途/情境與重點裝置。

圖片錯誤後備：onerror 切換替代 src 並更新 alt（如 section-5-5 主圖）。

隱藏描述：.sr-only 用於 SEO / 描述補充但不佔版面。

---
## 10. RWD 斷點（目前用法）
- 1200px：Gallery 寬度縮至 85%
- 992px：舊版某些頁調整（可逐步淘汰，改用 clamp 全流動）
- 768px：CTA、Button、Section padding 縮小 / Buttons 改 block
- 640px：表格縮字 + padding、Gallery 寬 100%、Hero padding 縮
- 600px：部分舊 Hero 字級（逐步由 clamp 取代）

策略：新頁面盡量只保留 768px / 640px 兩個核心斷點 + clamp 做流體排版。

---
## 11. Spacing 建議（未全面硬編碼）
- Section 外距（底部）：40px（手機可 30px）
- Section 內距：40px 30px（手機 30px 20px）
- Hero 與下一區塊間距：≥ 32px (已用 margin-bottom:40px)
- 卡片網格 gap：18px

---
## 12. 清理與技術債（TODO）
- 移除尚未刪除的每頁 .header h1 / p 固定 px 定義，完全依賴全域 .header h1/p
- 將 CTA 區塊的 h2 固定 30px 改成 clamp（可共用 h2 或自訂 .cta h2 clamp）
- 統一 992px / 600px 舊媒體查詢，逐步以 clamp + 768px / 640px 主斷點整合
- 建立 /docs 或 components snippet 方便複製標準結構

---
## 13. 範例片段（複製用）
Hero：
```
<div class="header">
  <h1>主標題關鍵價值陳述</h1>
  <p>補充一句具體情境 / 益處描述</p>
</div>
```

CTA：
```
<section class="cta" aria-labelledby="cta-title" aria-describedby="cta-desc">
  <h2 id="cta-title">行動呼籲標題</h2>
  <p id="cta-desc" class="sr-only">簡述用途與互動選項</p>
  <a class="btn" data-ga-category="CTA" data-ga-action="click" data-ga-label="buy_xxx">立即購買</a>
  <a class="btn line" data-ga-category="CTA" data-ga-action="click" data-ga-label="line_consult_xxx">LINE 諮詢</a>
  <a class="btn outline" data-ga-category="CTA" data-ga-action="download" data-ga-label="download_manual_xxx">下載手冊</a>
</section>
```

表格：
```
<div class="table-wrap">
  <table class="spec-table">
    <caption>產品規格</caption>
    <thead>
      <tr><th>項目</th><th>資料</th></tr>
    </thead>
    <tbody>
      <tr><td>尺寸</td><td>...</td></tr>
    </tbody>
  </table>
</div>
```

---
## 14. 版本管理說明
此文件由 2025-08-12 統整。後續如有新增元件 / 調整 clamp 值，請：
1. 先改 style.css
2. 測試 375 / 768 / 1440 寬度視覺
3. 更新本文件對應段落

---
如需補充其他標準（動畫、表單、Lazy-load 策略等），可在下一版新增章節。
