# 網路小說版型 · Web Novel Layout

> 把連載小說、章回體故事、長篇敘事做成可分享網頁的開源版型。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

一頁式滾動閱讀，但不是純文字流。把長文拆成不同視覺密度的區塊交錯，讓讀者眼睛有節奏感、不會疲勞。

## 為什麼有這個版型

要解決的問題：

1. **長文一頁式滾動容易疲勞** — 純文字塊讀者會放棄
2. **段落要清楚** — 不只是空一行，要有視覺層次的轉換點
3. **排版要多元** — 不能整篇同一個密度，要交錯出節奏
4. **關鍵對話與金句要被看見** — 重點不能埋在段落裡

## 四個核心視覺元件

| 元件 | 用途 |
|---|---|
| **散文段落**（Scene）| 主敘事，正常文字流 |
| **對話框**（Dialogue Bubble）| 角色台詞，泡泡造型＋說話者標籤，左右交錯 |
| **金句**（Pull Quote / Callout）| 重要句子放大、置中、加裝飾線 |
| **信件區塊**（Letter Section）| 抒情段落獨立成卡片，模擬信紙質感 |

## 連載系統擴充

| 元件 | 用途 |
|---|---|
| Chapter Hero | 每章開頭的儀式感封面 |
| Chapter Navigation | 上一章 / 目錄 / 下一章 |
| Reading Progress Bar | 頂部固定進度條 |
| Table of Contents | 目錄頁的章節列表 |
| Series Hero | 整本書的封面 |

## 怎麼用

### 方法一：手動 copy CSS

直接讀 `references/01-components.md`，把需要的元件 CSS 複製到你的 HTML。

### 方法二：用 AI agent

如果你用 Claude Code、Cursor、Codex 等 AI agent，這是一個 Anthropic-style skill pack。把整個資料夾放進你的 skill 路徑，跟 agent 說「用網路小說版型做」就會啟動。

```
your-skill-folder/
└── web-novel-layout/
    ├── SKILL.md
    ├── README.md
    └── references/
        ├── 01-components.md
        ├── 02-chapter-system.md
        └── 03-deploy-guide.md
```

### 方法三：直接看範例

`examples/` 資料夾有完整可用的 demo：

- `examples/index.html` — 目錄頁範例
- `examples/chapter-01.html` — 章節頁範例
- `examples/shared.css` — 所有元件的共用樣式

雙擊開啟就能看到完整效果。

## 配色預設

預設康乃馨淡色系，可換主題：

| 主題 | 適用 |
|---|---|
| 康乃馨淡色（預設）| 溫柔、親情、散文 |
| 海洋藍 | 懸疑、科幻、冷調 |
| 抹茶綠 | 治癒、日常、青春 |
| 暖橘 | 熱血、冒險、仲夏 |
| 紫薰衣 | 玄幻、詩意、古風 |
| 墨黑 | 武俠、正典、嚴肅 |

換主題只要改三個 CSS 變數：`--petal` / `--rose` / `--rose-deep`。詳見 `references/01-components.md`。

## 部署

預設 GitHub Pages 流程，免費。詳見 `references/03-deploy-guide.md`。

## 字數參考

| 章長 | 字數 | 適用 |
|---|---|---|
| 短章 | 1,500 - 2,500 字 | 速食小說、輕小說 |
| 中章 | 2,500 - 4,000 字 | 一般網路小說 |
| 長章 | 4,000 - 6,000 字 | 傳統長篇 |

每章內部建議 **至少 3 個視覺斷點**（場景分隔／金句／對話框），避免整章純文字塊。

## 許可

MIT License - 自由使用、修改、商用、改作。歡迎 fork 與 PR。

## 相關

源自 2026-05 一篇散文網頁的延伸思考。第一個應用案例是「辣味的比喻」母親節文章。

如果你做出了用這個版型的小說，歡迎開 issue 分享！
