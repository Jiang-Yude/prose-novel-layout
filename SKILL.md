---
name: mothers-day-tribute
version: v1.0
license: MIT
repo: https://github.com/Jiang-Yude/mothers-day-tribute
description: Mother's Day tribute page generator. User drops in an article (memoir, letter to mom, story, reflection); AI agent restructures it into a single-page HTML with editorial typography (prose / dialogue bubbles / pull quotes / letter sections), prefixed by a "Mother's Day YYYY" hero and optionally signed.
trigger: 母親節網頁, 母親節版型, 母親節感恩, mothers day page, 致媽媽網頁, 給媽媽的網頁, 母親節文章排版, mothers-day-tribute, 把這篇給媽媽的文章做成網頁
---

# Mother's Day Tribute · 母親節感恩網頁產生器 v1.0

把使用者寫給媽媽的文章，變成有閱讀節奏的母親節感恩網頁。

---

## 設計意圖

每年母親節，很多人想寫點什麼給媽媽——一段回憶、一個比喻、一封信。但寫出來貼在社群，常常變成一大段純文字，讀者很快就滑走了。

這個 skill 解決的問題：

1. **長文一頁式滾動容易疲勞** — 把純文字塊拆成不同視覺密度的區塊
2. **段落要有層次** — 不只空一行，要視覺上明確的轉換點
3. **關鍵對話與金句要被看見** — 對話用泡泡、金句用裝飾線
4. **給媽媽的告白要有儀式感** — 信件區塊獨立成卡片，讓讀的人感受到那是「給媽媽的話」

---

## 觸發詞

「母親節網頁」「母親節版型」「母親節感恩」「致媽媽網頁」「給媽媽的網頁」「母親節文章排版」「把這篇給媽媽的文章做成網頁」

英文：`mothers day page`, `mom tribute page`, `mothers-day-tribute`

---

## Agent 工作流程

當使用者觸發 skill 並貼上文章時，按以下步驟做：

### Step 1 · 確認基本資訊（一次問完）

```
我會把這篇文章排版成母親節感恩網頁。先確認幾件事：

1. 標題你想用「__________」（從文章猜一個給使用者）還是另外的？
2. 副標要不要？（建議：「假的故事，真的感受」之類的 italic 短句）
3. 結尾署名什麼？（可填：你的名字 / 暱稱 / 「致媽媽 — 你的孩子」/ 不署名）
4. 配色：預設康乃馨淡粉，其他選：暖橘 / 抹茶綠 / 紫薰衣 / 深玫瑰
5. 部署：要 Netlify Drop（最簡單，30 秒）/ GitHub Pages（要更新／版控）/ Vercel（要 SSO 保護）/ 先本地預覽就好？

回答後我就開始排版。
```

### Step 2 · 讀文章，識別四類內容

掃描整篇，標記：

- **散文段落**（Scene） — 一般敘述、回憶、描寫，最大宗
- **對話**（Dialogue） — 用引號標出的角色台詞。識別說話者（媽媽 / 我 / 孩子 / etc）
- **金句**（Pull Quote 候選）— 整篇最有重量的 1-3 句
- **信件**（Letter） — 「親愛的媽媽⋯」「媽媽，⋯」開頭的告白段

### Step 3 · 文章潤稿（可選，先問使用者）

潤稿前先問：「要我順便潤稿嗎？我會做這幾件事：」

- 拿掉破折號 `——`（換成句號或逗號）
- 拿掉「不是 X，而是 Y」對立句型（換成肯定句）
- 全形標點統一（`，。：？！` 取代半形）
- 抓出冗長重複句、建議精簡

使用者同意才動，不同意就只排版不改文字。

### Step 4 · 套用排版

按照「寫作節奏指南」配置元件：

| 位置 | 元件 |
|---|---|
| 最頂 | Hero（「YYYY 年母親節快樂」+ 文章標題 + 副標 + 康乃馨 SVG）|
| 1-2 段散文進場 | Scene |
| 角色互動 | Dialogue × 2-3（左右交錯）|
| 場景轉換 | Ornament `・ ・ ・` |
| 中段 | Pull Quote（1-2 個，最動人的句子）|
| 後段對話／衝突 | Dialogue × 2-3 |
| 章末抒情 | Letter Section（給媽媽的話獨立成信卡）|
| 章末收束 | Finale（畫框外金句）|
| 最底 | Signature（「— 署名」）|

節奏鐵律：

- 兩個 dialogue 之間至少夾一段 scene 或一個 ornament
- pull quote 和 callout 不要連續用
- letter section 全篇至多 1 次
- 對話框集中在「衝突場景」，反思段落用 pull quote

### Step 5 · 輸出 HTML

單一 HTML 檔，內嵌 CSS（不依賴外部框架，只連 Google Fonts）。

完整 HTML 範本見 `examples/template.html`。元件 CSS 全集見 `references/01-components.md`。

### Step 6 · 部署（看使用者選哪種）

三種方法，照 `references/03-deploy-guide.md`：

| 方法 | 對象 | 流程 |
|---|---|---|
| **Netlify Drop** | 不會 git，最快 | 打開 https://app.netlify.com/drop → 拖資料夾 → 30 秒拿網址 |
| **GitHub Pages** | 會 git，要更新／版控 | `git init` + `gh repo create` + `gh api pages` |
| **Vercel** | 要 SSO 保護或自訂域名 | https://vercel.com/new → 拖資料夾 |

**預設推薦 Netlify Drop**——最簡單，30 秒搞定。除非使用者明確說「我要 GitHub Pages」「我要 SSO 保護」才走另外兩種。

**內容隱蔽性處理**：不論哪種方法，HTML 都要加 `<meta name="robots" content="noindex, nofollow">`，並在資料夾放 `robots.txt`：

```
User-agent: *
Disallow: /
```

這是私人內容，知道網址才看得到，不希望陌生人 Google 到。

---

## 標題自動化

Hero 區開頭的標籤格式：

```
YYYY 年 ・ 母親節快樂
```

YYYY 自動取執行當下的年份（用 `TZ=Asia/Taipei date +%Y` 或讀系統年份）。如果使用者明確說別的年份，照他的。

---

## 配色

預設康乃馨淡色：

```css
:root {
  --bg:        #FBF6F0;
  --paper:     #FFFCF7;
  --petal:     #F5DCDC;
  --rose:      #C28A85;
  --rose-deep: #9E5F5A;
  --leaf:      #B8C2A8;
  --ink:       #3D332E;
  --ink-soft:  #7A6B62;
  --rule:      #E8D9D2;
}
```

換主題只改 `--petal / --rose / --rose-deep`：

| 主題 | --petal | --rose | --rose-deep | 適用 |
|---|---|---|---|---|
| 康乃馨淡色（預設）| #F5DCDC | #C28A85 | #9E5F5A | 溫柔、感恩、給媽媽 |
| 暖橘 | #F4D8C4 | #C9876A | #9E5F4A | 給很開朗的媽媽 |
| 抹茶綠 | #DDE5D2 | #8FA77E | #5E7B52 | 給愛大自然的媽媽 |
| 紫薰衣 | #DDD5E8 | #8F7BA3 | #5F507A | 給優雅的媽媽 |
| 深玫瑰 | #E8B8B8 | #A66258 | #7A4540 | 給很有威嚴的媽媽 |

---

## References 路由

| 任務 | 讀 |
|---|---|
| 元件 CSS / HTML 範本 | `references/01-components.md` |
| 文章 → 排版的判斷邏輯 | `references/02-article-to-page.md` |
| 部署到 Netlify / GitHub Pages / Vercel | `references/03-deploy-guide.md` |

---

## 工作流程禁忌

不要：

- ❌ 沒問使用者就直接排版（先問五個問題確認方向）
- ❌ 整篇純 Scene 段落（疲勞）
- ❌ 一篇用 5 個 pull quote（金句要稀有才有力）
- ❌ 把媽媽的多句憤怒分成 5 個 dialogue（合併成一個長 bubble 更有衝擊力）
- ❌ 動文字內容卻不問使用者（潤稿要先取得同意）
- ❌ 署名亂編（如果使用者沒給就不署名，不要編一個名字上去）

---

## 案例

第一個觸發 skill 的真實案例：

- **辣味的比喻**（2026-05-04，江昱德給媽媽的散文）
- 標題：〈喜歡煮麻辣火鍋的媽媽，跟一吃辣就拉肚子的孩子〉
- Repo: `Jiang-Yude/my-mothersday-2026`
- URL: https://jiang-yude.github.io/my-mothersday-2026/
- 配色：康乃馨淡色
- 結構：13 段散文 + 6 個對話框 + 2 個金句 + 1 個兩欄對比 + 1 封信件 + Finale 金句
- 完整檔案見 `examples/sample.html`
