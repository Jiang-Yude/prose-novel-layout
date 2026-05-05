# Mother's Day Tribute · 母親節感恩網頁產生器

> 把一篇給媽媽的文章，變成漂亮的母親節網頁。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

把你寫給媽媽的文章丟進來，AI 會自動排版成有層次的網頁——段落、對話、金句、信件區塊交錯呈現。開頭是「母親節快樂」標題，結尾可以署名。

## 解決什麼問題

每年母親節，很多人想寫點什麼給媽媽——一段回憶、一個比喻、一封信。但寫出來貼在 Threads 或社群，常常變成一大段純文字，讀起來很累。

這個版型把你的文章變成有閱讀節奏的網頁：

- 對話用泡泡突顯
- 金句放大置中
- 給媽媽的話獨立成信件卡片
- 背景是康乃馨淡色系
- 響應式，手機看也舒服

---

## 怎麼用

### 方法 A · 給 AI agent

如果你用 Claude Code、Cursor、Codex，把整個資料夾放進 skill 路徑，跟 agent 說：

> 「用 mothers-day-tribute 把這篇文章做成網頁」

然後貼上你的文章。Agent 會自動：

1. 讀文章找出對話、金句、給媽媽的告白段
2. 套用四個視覺元件排版
3. 開頭加上「YYYY 年母親節快樂」標題
4. 結尾加上署名（會問你要不要署名、署什麼）
5. 輸出單一 HTML 檔，可雙擊開來看

詳細 agent workflow 見 `SKILL.md`。

### 方法 B · 手動 copy 範本

直接複製 `examples/template.html`，把 placeholder 換成自己的內容：

- `{{TITLE_LINE_1}}` / `{{TITLE_LINE_2}}` → 標題（兩行排版）
- `{{SUBTITLE}}` → 副標
- `{{YEAR}}` → 年份（自動填）
- `{{SCENE_*}}` → 散文段落
- `{{DIALOGUE_*}}` → 對話框
- `{{PULLQUOTE}}` → 金句
- `{{LETTER}}` → 給媽媽的信
- `{{SIGNATURE}}` → 署名

### 方法 C · 直接看範例

`examples/sample.html` 是真實案例（〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉）。雙擊開瀏覽器看效果。

---

## 四個核心元件

| 元件 | 用途 | 你的文章裡長什麼樣 |
|---|---|---|
| **散文段落** | 主敘事 | 一般敘述、回憶、描寫 |
| **對話框** | 角色台詞 | 有引號的對話：媽媽說「⋯」、我說「⋯」 |
| **金句** | 重要句 | 整篇最動人的一句 |
| **信件區塊** | 抒情段 | 「親愛的媽媽⋯」開頭的長段告白 |

加上裝飾：

- **Hero**（封面）— 「2026 年母親節快樂」+ 你的標題 + 康乃馨 SVG
- **Ornament**（・ ・ ・）— 場景轉換時的小分隔
- **Finale**（結尾）— 最後一句金句獨立漂在背景上
- **Signature**（署名）— 「— 你的名字」

---

## 配色主題

預設康乃馨淡色（粉紅＋暖白＋葉綠），可換：

| 主題 | 適用 |
|---|---|
| 康乃馨淡色（預設）| 溫柔、感恩、給媽媽 |
| 暖橘 | 給很開朗的媽媽 |
| 抹茶綠 | 給愛大自然的媽媽 |
| 紫薰衣 | 給優雅的媽媽 |
| 深玫瑰 | 給很有威嚴的媽媽 |

換主題只要改三個 CSS 變數。詳見 `references/01-components.md`。

---

## 部署（三種方法）

| 方法 | 難度 | 適合 |
|---|---|---|
| **Netlify Drop** | ⭐ 30 秒 | 不會 git，拖資料夾就好 |
| **GitHub Pages** | ⭐⭐ 3 分鐘 | 想要好記網址、要更新內容 |
| **Vercel** | ⭐⭐⭐ 5 分鐘 | 要 SSO 保護、自訂網域 |

### 最簡單的方法：Netlify Drop

打開 [https://app.netlify.com/drop](https://app.netlify.com/drop)，把你的 HTML 資料夾拖進去，等 10 秒拿到分享網址。完全免費、免註冊即可體驗，註冊後可以永久保留。

### 推薦給開發者：GitHub Pages

```bash
cd 你的母親節網頁資料夾
git init -b main
git add .
git commit -m "母親節 2026"
gh repo create my-mothersday-2026 --public --source=. --push
gh api -X POST "repos/<你的帳號>/my-mothersday-2026/pages" -f "source[branch]=main" -f "source[path]=/"
```

等 1-3 分鐘，網址會是 `https://<你的帳號>.github.io/my-mothersday-2026/`。

完整流程（含隱蔽分享、Vercel SSO、不被 Google 收錄）見 `references/03-deploy-guide.md`。

---

## 完整檔案結構

```
mothers-day-tribute/
├── README.md                       ← 你正在看
├── SKILL.md                        ← 給 AI agent 的指令
├── LICENSE                         ← MIT
├── references/
│   ├── 01-components.md           ← 元件全 CSS
│   ├── 02-article-to-page.md      ← AI 排版工作流
│   └── 03-deploy-guide.md         ← 部署
└── examples/
    ├── template.html               ← 空白範本（含 placeholder）
    └── sample.html                 ← 真實範例（辣味的比喻）
```

---

## 案例

如果你做出了用這個版型的母親節網頁，歡迎開 issue 分享，列在這裡：

- **辣味的比喻**（2026-05-04）— 第一個用這個版型做的網頁，作者寫給媽媽的散文。網址：[my-mothersday-2026](https://jiang-yude.github.io/my-mothersday-2026/)

---

## 許可

MIT License — 自由使用、修改、商用、改作。歡迎 fork 與 PR。

---

## 致謝

源自 2026-05 一篇散文〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉的網頁版型。原本只是一篇給媽媽的文章，後來把排版邏輯抽出來開源，希望今年母親節大家都能寫一篇給自己的媽媽，貼成漂亮的網頁送出去。
