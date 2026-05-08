# Prose & Novel Layout · 小說、散文的網頁排版技能包

> 把一篇散文或一個連載小說，變成有閱讀節奏的網頁。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

純文字塊是社群最大的閱讀殺手。寫了三千字的散文、寫了五章的故事，貼到 Threads / IG 變成一坨字，讀者三秒鐘內滑走。

這個技能包把你的文章變成有閱讀節奏的網頁——對話用泡泡突顯、金句放大置中、抒情段獨立成信件卡片，背景是溫柔的色系，響應式，手機看也舒服。

---

## 看兩個案例

| 案例 | 主題 | 配色 | 網址 |
|---|---|---|---|
| 🌸 **母親節版本** | 〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉 | 康乃馨淡粉 | [my-mothersday-2026](https://jiang-yude.github.io/my-mothersday-2026/) |
| 🌻 **父親版本** | 〈愛抽菸的爸爸，跟一聞菸味就想吐的孩子〉 | 暖橘金黃 | [my-letter-dad](https://jiang-yude.github.io/my-letter-dad/) |

兩個案例都用同一套技能包做的，只換了配色、SVG 跟標題。證明這個版型的彈性——任何給某人的散文都能套。

---

## 四個核心視覺元件

| 元件 | 用途 |
|---|---|
| **散文段落** | 主敘事，正常文字流 |
| **對話框** | 角色台詞，泡泡造型，左右交錯 |
| **金句** | 重要句子放大、置中、加裝飾線 |
| **信件區塊** | 抒情段獨立成卡片，模擬信紙 |

加上裝飾元素：Hero（封面）／Ornament（・ ・ ・）／Callout（強調句）／Contrast Grid（兩欄對比）／Finale（畫框外結尾）／Signature（署名）。

連載小說多 5 個元件：Chapter Hero ／ Chapter Navigation ／ Reading Progress Bar ／ Table of Contents ／ Series Hero。

---

## 三種輸出模式

### Mode A · 單篇散文

適合：給媽媽的話、給爸爸的話、給某人的書信、心情日記、紀念文、訪談稿、婚禮信。

結構：一個 `index.html` 從頭到尾。

### Mode B · 連載小說

適合：章回體小說、長篇連載、系列散文、多人物對話的故事。

結構：`index.html`（目錄頁）+ `chapter-XX.html`（每章一個）。

### Mode C · 課題分離信件（引導工作流）

跟 A／B 不同——Mode C 不只是排版，是**陪你整理思緒**。

帶著糾結進來（跟父母、伴侶、朋友、同事），AI 陪走三步：

1. **整理想法**（你說，我問）
2. **課題分離**（拆「我的」vs「對方的」課題，阿德勒心理學）
3. **整理成一封信，做成網頁**（含必要的免責聲明）

> 寫信不是為了改變對方。  
> 寫信是為了讓自己想清楚。  
> 對方看不看、接不接受，是對方的課題。

⚠️ 這個 mode 必須附免責聲明：**這是輔助釐清工具，不是心理諮商**。真有強烈心結請找專業心理師。詳見 `references/06-disclaimer.md`。

兩個現成案例（都是用 Mode C 寫出來的真實故事）：

- 🌸 母親節版本 ・[my-mothersday-2026](https://jiang-yude.github.io/my-mothersday-2026/)
- 🌻 父親版本 ・[my-letter-dad](https://jiang-yude.github.io/my-letter-dad/)

---

## 怎麼用

### 方法 A · 給 AI agent

把整個資料夾放到你的 AI agent skill 路徑（Claude Code、Cursor、Codex），跟 agent 說：

> 「用 prose-novel-layout 把這篇文章做成網頁」

然後貼上文章。Agent 會自動：

1. 判斷是單篇還是連載
2. 識別文章裡的對話、金句、信件段
3. 套用四個視覺元件排版
4. 配色、署名、標題自動處理
5. 輸出 HTML 檔，可雙擊開瀏覽器看

詳細 agent workflow 見 `SKILL.md`。

### 方法 B · 手動 copy 範本

從 `examples/` 拿範本，把內容換成自己的：

- `examples/sample-mom.html` — 母親節版本（完整可用範例）
- `examples/sample-dad.html` — 父親版本（完整可用範例）
- `examples/template-essay.html` — 空白單篇範本（含 placeholder）
- `examples/template-novel/` — 空白連載範本（目錄 + 兩章）

雙擊 sample 看效果，再仿著做自己的。

---

## 配色主題

預設康乃馨淡粉（暖白＋粉紅＋葉綠），可換：

| 主題 | 適用 |
|---|---|
| 康乃馨淡粉（預設）| 母親節、感恩、抒情 |
| 暖橘金黃 | 父親節、開朗、向日葵 |
| 抹茶綠 | 治癒、日常、青春 |
| 紫薰衣 | 玄幻、優雅、詩意 |
| 海洋藍 | 懸疑、科幻、冷調 |
| 墨黑（夜色版）| 武俠、正典、嚴肅長篇 |

換主題只改三個 CSS 變數：`--petal` / `--rose` / `--rose-deep`。詳見 `references/01-components.md`。

---

## 部署（三種方法）

| 方法 | 難度 | 適合 |
|---|---|---|
| **Netlify Drop** | ⭐ 30 秒 | 不會 git，拖資料夾 |
| **GitHub Pages** | ⭐⭐ 3 分鐘 | 要更新／版控 |
| **Vercel** | ⭐⭐⭐ 5 分鐘 | 要 SSO 保護、自訂網域 |

最簡單方式：拖資料夾到 [https://app.netlify.com/drop](https://app.netlify.com/drop)，10 秒拿網址。

完整教學見 `references/04-deploy-guide.md`。

---

## 完整檔案結構

```
prose-novel-layout/
├── README.md                        ← 你正在看
├── SKILL.md                         ← 給 AI agent 的指令
├── LICENSE                          ← MIT
├── references/
│   ├── 01-components.md            ← 元件全 CSS
│   ├── 02-chapter-system.md        ← 連載系統（TOC、上下章、進度）
│   ├── 03-article-to-page.md       ← 文章 → 排版的判斷邏輯
│   └── 04-deploy-guide.md          ← 部署
└── examples/
    ├── sample-mom.html              ← 母親案例（完整）
    ├── sample-dad.html              ← 父親案例（完整）
    ├── template-essay.html          ← 單篇散文範本
    └── template-novel/              ← 連載小說範本
        ├── index.html
        ├── chapter-01.html
        └── chapter-02.html
```

---

## 案例集

如果你做出了用這個版型的網頁，歡迎開 issue 分享：

- 🌸 **辣味的比喻**（母親節 2026）— [my-mothersday-2026](https://jiang-yude.github.io/my-mothersday-2026/)
- 🌻 **菸味的比喻**（給爸爸）— [my-letter-dad](https://jiang-yude.github.io/my-letter-dad/)

---

## 許可

MIT License — 自由使用、修改、商用、改作。歡迎 fork 與 PR。

---

## 致謝

源自 2026-05 一篇散文〈辣味的比喻〉的網頁版型。從母親節文章開始，後來抽出排版邏輯做成開源技能包，再擴展到父親節、其他抒情散文、以及連載小說的場景。

希望這個版型能讓更多人寫的東西被讀完。
