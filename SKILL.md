---
name: prose-novel-layout
version: v2.0
license: MIT
repo: https://github.com/Jiang-Yude/prose-novel-layout
description: Chinese prose & novel web layout skill pack. Drop in a single article (essay, letter, memoir) or a multi-chapter novel; AI agent restructures it into editorial-typography HTML pages. Four core components — prose paragraphs, dialogue bubbles, pull quotes, letter sections — plus chapter system (cover, prev/next, TOC, progress) for serial fiction.
trigger: 散文版型, 小說版型, 散文網頁, 小說網頁, 散文排版, 小說排版, 連載小說, 母親節網頁, 父親節網頁, 給媽媽的網頁, 給爸爸的網頁, 章回體, 寫信給, 文章排版, 課題分離, 想對父母說, 跟父母和解, 整理我的想法, 寫信給父母, 我糾結很久, prose layout, novel layout, task separation letter
---

# Prose & Novel Web Layout · 小說、散文的網頁排版技能包 v2.0

把一篇散文或一個連載小說，變成有閱讀節奏的網頁。

---

## 設計意圖

純文字塊是社群最大的閱讀殺手。寫了三千字的散文、寫了五章的故事，貼到 Threads / IG 變成一整坨字，讀者三秒鐘內就滑走。

這個技能包解決的問題：

1. **長文一頁式滾動容易疲勞** — 把純文字塊拆成不同視覺密度的區塊
2. **段落要有層次** — 不只空一行，要視覺上明確的轉換點
3. **關鍵對話與金句要被看見** — 對話用泡泡、金句用裝飾線
4. **抒情段落要有儀式感** — 給某人的告白、書信、獨白獨立成卡片
5. **連載故事要有導航** — 章節索引、上下章、閱讀進度，讓讀者可以慢慢讀

---

## 四個核心視覺元件

不論單篇還是連載，都靠這四個元件交錯排版：

> **散文段落**（Scene）・主敘事，正常文字流  
> **對話框**（Dialogue Bubble）・角色台詞，泡泡造型，左右交錯  
> **金句**（Pull Quote）・重要句子放大、置中、加裝飾線  
> **信件區塊**（Letter Section）・抒情段獨立成卡片，模擬信紙

加上裝飾元素：

- **Hero**（封面）— 標題 + 副標 + 主題 SVG（康乃馨／向日葵／自訂）
- **Ornament**（・ ・ ・）— 場景轉換時的小分隔
- **Callout** — 中等強調句，比金句輕、比散文重
- **Contrast Grid** — 兩欄對比（A 有錯嗎？B 有錯嗎？）
- **Finale** — 結尾畫框外金句
- **Signature** — 「— 你的名字」

---

## 兩種輸出模式

### Mode A · 單篇散文（一頁式）

適合：

- 給媽媽的話（母親節）
- 給爸爸的話（父親節）
- 給某人的書信、紀念文
- 心情日記要正式發表
- 訪談稿（對話為主）
- 婚禮信、追悼文

結構：一個 `index.html` 從頭到尾。

```
my-letter-2026/
├── index.html        ← 整篇文章
├── robots.txt        ← 隱私 (Disallow: /)
└── assets/           ← 圖片（選用）
```

### Mode B · 連載小說（多章節）

適合：

- 章回體小說（≥2 章）
- 長篇連載
- 系列散文（一週一篇）
- 多人物對話的故事

結構：每章獨立 HTML + 目錄頁。

```
my-novel/
├── index.html        ← 目錄頁（書系封面 + 章節列表）
├── chapter-01.html   ← 第一章
├── chapter-02.html
├── chapter-03.html
└── assets/
    └── shared.css    ← 共用樣式（選用）
```

連載專屬擴充元件：

- **Chapter Hero** — 每章開頭的儀式感封面
- **Chapter Navigation** — 章末「上一章 / 目錄 / 下一章」
- **Reading Progress Bar** — 頂部固定的閱讀進度條
- **Table of Contents** — 目錄頁的章節列表
- **Series Hero** — 整本書的封面

詳見 `references/02-chapter-system.md`。

### Mode C · 課題分離信件（Task Separation Letter）

跟 Mode A／B 不同——Mode C 是**引導工作流**，不只是排版。

使用者帶著「跟某人的糾結」進來，AI 陪走三步：

1. **整理想法** ・你說，我問（五個引導問題）
2. **課題分離** ・拆「我的課題」vs「對方的課題」（阿德勒心理學）
3. **整理成一封信，做成網頁** ・用四元件排版 + 必要的免責聲明

適合：

- 想對父母說但說不出口
- 跟某人有未解的糾結（伴侶／朋友／同事）
- 不期待對方理解，但想自己想清楚
- 母親節／父親節想送孩子們一份「整理思緒」的禮物

**核心理念**：

> 寫信不是為了改變對方。<br>
> 寫信是為了讓自己想清楚。<br>
> 對方看不看、接不接受，是對方的課題。

⚠️ **必須附上免責聲明**：這是輔助釐清工具，不是心理諮商。詳見 `references/06-disclaimer.md`。

完整工作流見 `references/05-task-separation-letter.md`。

兩個現成案例（都是用 Mode C 寫出來的）：

- 🌸 〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉
- 🌻 〈愛抽菸的爸爸，跟一聞菸味就想吐的孩子〉

兩篇都來自江昱德 2026-05 的真實困境——學會尊重彼此、放過自己，再寫成信。

---

## 觸發詞

**單篇散文**：「散文版型」「文章排版」「散文網頁」「給媽媽的網頁」「給爸爸的網頁」「給某人的信」「母親節網頁」「父親節網頁」「致媽媽」「致爸爸」「把這篇文章做成網頁」

**連載小說**：「小說版型」「網路小說版型」「做連載」「章回體」「做小說網頁」「長篇連載」「章節網頁」「故事網頁」「把小說放網路上」

英文：`prose layout`, `novel layout`, `essay web layout`, `serial fiction layout`, `editorial typography`

---

## Agent 工作流程

當使用者觸發 skill 並貼上文章時：

### Step 1 · 判斷模式

問使用者：

```
這是單篇文章還是連載？
- 一篇散文 / 給某人的話 / 心情日記 → Mode A 單篇
- 兩章以上 / 連載故事 / 章回體 → Mode B 連載

或者直接貼來，我從內容判斷。
```

判斷規則：

- 文章只有一個主題、一個場景、3,000-5,000 字以內 → Mode A
- 有「第一章」「第二章」標記、超過 5,000 字、多場景切換 → Mode B
- 不確定就問使用者「會有第二章嗎？」

### Step 2 · 確認基本資訊（一次問完）

```
我會把這篇排版成網頁。先確認幾件事：

1. 標題你想用「__________」（從文章猜一個給使用者）還是另外的？
2. 副標要不要？（建議：italic 短句點題）
3. 主題場合：母親節 / 父親節 / 給某人的話 / 紀念 / 連載小說 / 其他
4. 結尾署名什麼？（可填：你的名字 / 暱稱 / 不署名）
5. 配色：康乃馨淡粉 / 暖橘金黃 / 抹茶綠 / 紫薰衣 / 海洋藍 / 墨黑 / 自訂
6. 部署：Netlify Drop（最簡單，30 秒）/ GitHub Pages（要更新／版控）/ Vercel（要 SSO）/ 先本地預覽就好？

回答後我就開始排版。
```

### Step 3 · 識別內容類型

掃文章標記：

- **Scene**（散文段落）— 一般敘述、回憶、描寫，最大宗
- **Dialogue**（對話）— 引號標出的角色台詞，識別說話者
- **Pull Quote**（金句候選）— 整篇最有重量的 1-3 句
- **Letter**（信件）— 「親愛的⋯」「媽媽，⋯」「爸爸，⋯」開頭的告白段

識別邏輯詳見 `references/03-article-to-page.md`。

### Step 4 · 文章潤稿（可選，先問使用者）

潤稿前先問。同意才動：

- 拿掉破折號 `——`（換成句號或逗號）
- 拿掉「不是 X，而是 Y」對立句型（換成肯定句）
- 全形標點統一
- 抓出冗長重複句

不同意 → 只排版，不改文字。

### Step 5 · 套用排版

按節奏指南配置元件（詳見 `references/01-components.md`）。

**節奏鐵律**：

- 兩個 dialogue 之間至少夾一段 scene 或 ornament
- pull quote 和 callout 不要連續用
- letter section 全篇至多 1 次（單篇 mode）
- 對話框集中在「衝突場景」，反思段落用 pull quote

### Step 6 · 輸出 HTML

單一 HTML（Mode A）或多 HTML（Mode B），內嵌 CSS（不依賴外部框架，只連 Google Fonts）。

範本：

- `examples/template-essay.html` — 單篇散文範本
- `examples/template-novel/` — 連載小說範本（index.html + chapter-01.html + chapter-02.html）

### Step 7 · 部署

三種方法（詳見 `references/04-deploy-guide.md`）：

| 方法 | 對象 | 流程 |
|---|---|---|
| **Netlify Drop** | 不會 git，最快 | 拖資料夾到 [app.netlify.com/drop](https://app.netlify.com/drop) → 30 秒 |
| **GitHub Pages** | 會 git，要更新／版控 | `gh repo create` + `gh api pages` |
| **Vercel** | 要 SSO 保護 | 拖到 [vercel.com/new](https://vercel.com/new) |

**預設推薦 Netlify Drop**。

**隱蔽性處理**：HTML 加 `<meta name="robots" content="noindex, nofollow">`，資料夾加 `robots.txt: Disallow: /`，repo 命名不要太好猜。

---

## 配色主題

預設「康乃馨淡粉」（暖白＋粉紅＋葉綠），適合大部分抒情主題。

| 主題 | --petal | --rose | --rose-deep | 適用場景 |
|---|---|---|---|---|
| 康乃馨淡粉（預設）| #F5DCDC | #C28A85 | #9E5F5A | 母親節、感恩、給媽媽 |
| 暖橘金黃 | #F4D8C4 | #C9876A | #9E5F4A | 父親節、開朗、向日葵 |
| 抹茶綠 | #DDE5D2 | #8FA77E | #5E7B52 | 治癒、日常、青春 |
| 紫薰衣 | #DDD5E8 | #8F7BA3 | #5F507A | 玄幻、優雅、詩意 |
| 海洋藍 | #D4E2EA | #6B8FAD | #4A6884 | 懸疑、科幻、冷調 |
| 墨黑（夜色版）| 全套變數重寫 | | | 武俠、正典、嚴肅 |

換主題只改 `--petal / --rose / --rose-deep` 三個變數。詳見 `references/01-components.md`。

長篇小說建議**全書統一一個配色**，章節間切換主題會讓讀者混亂。

---

## References 路由

| 任務 | 讀 |
|---|---|
| 元件 CSS / HTML 範本 | `references/01-components.md` |
| 連載系統（章節導航、TOC、進度條）| `references/02-chapter-system.md` |
| 文章 → 排版的判斷邏輯 | `references/03-article-to-page.md` |
| 部署到 Netlify / GitHub Pages / Vercel | `references/04-deploy-guide.md` |
| **課題分離信件模式（引導工作流）** | `references/05-task-separation-letter.md` |
| **免責聲明 HTML 模板（Mode C 必附）** | `references/06-disclaimer.md` |

---

## 案例

### Case 1 · 母親節版本

- **主題**：〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉
- **配色**：康乃馨淡粉
- **網址**：[https://jiang-yude.github.io/my-mothersday-2026/](https://jiang-yude.github.io/my-mothersday-2026/)
- **檔案**：`examples/sample-mom.html`

### Case 2 · 父親版本（給爸爸的話）

- **主題**：〈愛抽菸的爸爸，跟一聞菸味就想吐的孩子〉
- **配色**：暖橘金黃
- **網址**：[https://jiang-yude.github.io/my-letter-dad/](https://jiang-yude.github.io/my-letter-dad/)
- **檔案**：`examples/sample-dad.html`

兩個案例同一套技能包做的，只換配色、SVG 與標題，證明這個版型的彈性：**任何給某人的散文都能套**。

---

## 工作流程禁忌

不要：

- ❌ 沒問使用者就直接排版（先問模式 + 五個基本問題）
- ❌ 整篇純 Scene 段落（疲勞）
- ❌ 一篇用 5 個 pull quote（金句要稀有才有力）
- ❌ 動文字內容卻不問使用者（潤稿要先取得同意）
- ❌ 署名亂編（沒給就不署名）
- ❌ 連載小說每章換主題配色（讀者會混亂）
- ❌ 把所有章節塞進一個 HTML（除非確定章數 ≤5）

---

## 改作（Forking）

歡迎 fork：

- 換配色 → 改 CSS 變數
- 換字體 → 改 Google Fonts 連結 + body font-family
- 換主題 SVG → 改 hero-flower 的 svg 內容
- 加新元件 → 在 `references/01-components.md` 加，提 PR
- 加 v3 想法（書籤、夜間模式、多語、字級調整）→ 提 issue 討論

---

## 致謝

源自 2026-05 一篇散文〈辣味的比喻〉的網頁版型。從母親節文章開始，後來抽出排版邏輯做成開源技能包，再擴展到父親節、其他抒情散文、以及連載小說的場景。

希望這個版型能讓更多人寫的東西被讀完。

License: MIT。自由使用、改作、商用。
