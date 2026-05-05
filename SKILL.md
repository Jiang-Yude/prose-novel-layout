---
name: web-novel-layout
version: v1.0
license: MIT
repo: https://github.com/Jiang-Yude/web-novel-layout
description: Open-source web novel layout skill pack. Single-page editorial typography (prose / dialogue bubbles / pull quotes / letter sections) extended with serial fiction system (chapter cover, prev/next nav, reading progress, table of contents). Self-contained, no external dependencies beyond Google Fonts.
trigger: web novel layout, 網路小說版型, 做網路小說, 做連載, 章回體, 做小說網頁, 長篇連載, 章節網頁, 做故事網頁, 把小說放網路上
---

# Web Novel Layout · 網路小說版型 v1.0

把連載小說、章回體故事、長篇敘事做成可分享的網頁。

---

## 設計意圖

要解決的問題：

1. **長文一頁式滾動容易疲勞** — 純文字塊讀者會放棄。但翻頁版（信紙翻書）又太重、不適合長散文。
2. **段落要清楚** — 不只是空一行，要有視覺層次的轉換點（場景分隔／配色／字級）讓讀者眼睛知道「這是新段」。
3. **排版要多元** — 不能整篇都同一個密度。要有正常段落、有放大金句、有泡泡對話、有獨立卡片，交錯出節奏。
4. **關鍵對話與金句要被看見** — 重點不能埋在段落裡。對話用泡泡突顯角色互動，金句用裝飾線放大置中。
5. **連載故事要有章節系統** — 章節索引、上下章導航、閱讀進度，讓讀者可以慢慢讀、回頭看、追進度。

這個版型是為「給朋友看／在社群分享／放部落格／開連載」設計的。它的核心是：**讓長篇閱讀有節奏感**。

---

## 觸發詞

「網路小說版型」「做網路小說」「做連載」「章回體」「做小說網頁」「長篇連載」「章節網頁」「做故事網頁」「把小說放網路上」「故事第一章 第二章」「連載故事網頁」

英文：`web novel layout`, `serial fiction website`, `chapter-based story website`, `novel hosting page`

---

## 快速開始

### 給 AI agent

把整個 `web-novel-layout/` 資料夾放進你的 skill 路徑，要做小說網頁時讀取本 SKILL.md。

### 給 Human

直接看 `examples/` 的範本：
- `examples/index.html` 是目錄頁
- `examples/chapter-01.html` 是章節頁

或讀 `references/01-components.md` copy 需要的元件。

---

## 核心元件

四個視覺元件（從散文編輯版型繼承）：

1. **散文段落**（Scene）
2. **對話框**（Dialogue Bubble）
3. **金句**（Pull Quote / Callout）
4. **信件區塊**（Letter Section）

連載系統擴充五個元件：

5. **Chapter Hero**（章節封面）
6. **Chapter Navigation**（上下章導航）
7. **Reading Progress Bar**（閱讀進度條）
8. **Table of Contents**（目錄頁）
9. **Series Hero**（書系封面）

加裝飾元素：

10. **Ornament**（・ ・ ・ 場景分隔）
11. **Scene Label**（場景小標）
12. **Contrast Grid**（兩欄對比）
13. **Finale**（畫框外結尾）

完整 CSS 與 HTML 範本見 `references/01-components.md`。

---

## 架構

### 兩種選擇

| 場景 | 架構 | 優點 | 缺點 |
|---|---|---|---|
| 章數少（≤5）| 單頁 SPA + JS 切章 | 一個檔案、好 deploy | JS 切換、難分享單章 |
| 章數多（>5）或要 SEO | **多 HTML 檔（推薦）** | 每章獨立 URL、好分享、好搜尋 | 需要管多檔案 |

預設走多 HTML 檔（每章一個 URL），這也是真實小說網站（晉江、起點、AO3）的做法。

### 目錄結構

```
我的小說/
├── index.html              ← 目錄頁（封面 + TOC + 章節列表）
├── chapter-01.html         ← 第一章
├── chapter-02.html
├── chapter-03.html
├── ...
└── assets/
    └── shared.css          ← 共用樣式
```

---

## 配色

預設「康乃馨淡色系」（CSS 變數定義），可一鍵切換主題：

```css
:root {
  --bg:        #FBF6F0;    /* 暖奶白底 */
  --paper:     #FFFCF7;    /* 卡片底 */
  --petal:     #F5DCDC;    /* 主色：花瓣淡粉 */
  --rose:      #C28A85;    /* accent 玫瑰 */
  --rose-deep: #9E5F5A;    /* 標題深玫瑰 */
  --leaf:      #B8C2A8;    /* 葉綠點綴 */
  --ink:       #3D332E;    /* 主文字 */
  --ink-soft:  #7A6B62;    /* 次文字 */
  --rule:      #E8D9D2;    /* 分隔線 */
}
```

換主題只改 `--petal / --rose / --rose-deep` 三個值。內建主題：

| 主題 | --petal | --rose | --rose-deep | 適用 |
|---|---|---|---|---|
| 康乃馨淡色（預設）| #F5DCDC | #C28A85 | #9E5F5A | 溫柔、親情、散文 |
| 海洋藍 | #D4E2EA | #6B8FAD | #4A6884 | 懸疑、科幻、冷調 |
| 抹茶綠 | #DDE5D2 | #8FA77E | #5E7B52 | 治癒、日常、青春 |
| 暖橘 | #F4D8C4 | #C9876A | #9E5F4A | 熱血、冒險、仲夏 |
| 紫薰衣 | #DDD5E8 | #8F7BA3 | #5F507A | 玄幻、詩意、古風 |
| 墨黑（夜色版）| 全套變數要重寫 | | | 武俠、正典、嚴肅 |

長篇小說建議**全書統一配色**，章節間切換主題會讓讀者混亂。

---

## 字體

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;500;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
```

- 中文：Noto Serif TC（思源宋體繁中）
- 西文／斜體副標：Cormorant Garamond italic
- Body fallback: `'Songti TC', 'PingFang TC', serif`

簡體場景可換 Noto Serif SC。日文場景可換 Noto Serif JP。

---

## 寫作節奏指南

### 每章建議的元件分佈

| 位置 | 元件 |
|---|---|
| 章節最頂 | Chapter Hero |
| 1-2 段散文進場 | Scene |
| 角色互動 | Dialogue × 2-3 |
| 場景轉換 | Ornament `・ ・ ・` |
| 中段 | Pull Quote 或 Callout（章節主旨）|
| 後段對話／衝突 | Dialogue × 2-3 |
| 章末抒情 | Letter Section（如有書信／心聲）|
| 章末收束 | Finale 或直接 Chapter Nav |
| 章節最底 | Chapter Nav（上一章 / 目錄 / 下一章）|

### 字數參考

- 短章：1,500-2,500 字（速食小說、輕小說）
- 中章：2,500-4,000 字（一般網路小說）
- 長章：4,000-6,000 字（傳統長篇）

### 節奏鐵律

- 兩個 dialogue 之間至少夾一段 scene 或一個 ornament
- pull quote 和 callout 不要連續用
- 一章用 letter-section 至多 1 次
- 對話框集中在「衝突場景」，反思段落用 pull quote / callout
- 每章至少 3 個視覺斷點，不要整章純文字塊

---

## 部署

預設 GitHub Pages（免費、簡單）：

```bash
cd 我的小說
git init -b main
git add .
git commit -m "首發"
gh repo create my-novel-name --public --source=. --push
gh api -X POST "repos/<owner>/my-novel-name/pages" -f "source[branch]=main" -f "source[path]=/"
```

詳細步驟與隱蔽技巧（noindex、robots.txt）見 `references/03-deploy-guide.md`。

---

## References 路由

| 任務 | 讀 |
|---|---|
| 元件 CSS / HTML 範本 | `references/01-components.md` |
| 章節系統實作（TOC / 上下章 / 進度條）| `references/02-chapter-system.md` |
| 部署到 GitHub Pages / Vercel | `references/03-deploy-guide.md` |

---

## 工作流程（給 AI agent）

1. **問清楚**：章數？預期字數？讀者群？要公開還是隱蔽分享？
2. **先做 1 個章節 demo**，確認排版風格與配色，再批量做其他章
3. **每章手動排版**：依寫作節奏指南配元件，不要每章用同一套模板
4. **目錄頁最後做**：有所有章節後再寫 index.html 才能準確列字數
5. **本地預覽**：直接雙擊 HTML 開瀏覽器看
6. **部署**：照 `references/03-deploy-guide.md` 走

不要：
- ❌ 每章都同一套排版（讀起來無聊）
- ❌ 整章只有 Scene 段落（疲勞）
- ❌ 章節間切換配色主題（混亂）
- ❌ 把所有章節塞進一個 HTML（除非確定章數 ≤5）

---

## 改作（Forking）

歡迎 fork 改自己的版本：

- 換配色 → 改 CSS 變數即可
- 換字體 → 改 Google Fonts 連結 + body font-family
- 加新元件 → 在 references/01-components.md 加，提 PR
- 加 v2 想法（書籤、夜間模式、多語）→ 提 issue 討論

---

## 案例集

歡迎在 issue 分享你做出的小說網站，列在這裡：

- 範例 1：（待加入）
- 範例 2：（待加入）

---

## 致謝

源自 2026-05-04 一篇散文〈辣味的比喻〉的網頁版型，作者覺得這個排版邏輯適合做連載故事，就獨立出來開源。

四個核心視覺元件（散文／對話框／金句／信件）的設計理念來自編輯雜誌與紙本書的視覺語言，做成 web 友善的形式。

許可：MIT License。請隨意使用、改作、商用。
