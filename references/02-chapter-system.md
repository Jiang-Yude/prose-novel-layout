# 連載系統 · 多章節擴充元件

只有 Mode B（連載小說）才用。單篇散文略過這份。

---

## 目錄結構

```
我的小說/
├── index.html              ← 目錄頁（書系封面 + TOC）
├── chapter-01.html         ← 第一章
├── chapter-02.html
├── chapter-03.html
├── ...
└── assets/
    └── shared.css          ← 共用樣式（選用）
```

每章獨立一個 HTML，這是真實小說網站（晉江、起點、AO3）的做法。每章獨立 URL 好分享、好搜尋、好版控。

---

## 1. Series Hero（書系封面 / 目錄頁封面）

`index.html` 頂部，整本書的封面。

```html
<section class="series-hero">
  <div class="series-meta">完結 ・ 全 12 章</div>
  <h1 class="series-title">小說書名</h1>
  <div class="series-sub">副標 italic</div>
  <p class="series-blurb">兩三句話的劇情簡介。給讀者進入故事前的一個 hook。不要寫劇透，留懸念。</p>
  <div class="hero-divider"></div>
</section>
```

```css
.series-hero {
  text-align: center; padding: 100px 28px 60px;
}
.series-meta {
  font-size: 14px; letter-spacing: 0.4em; color: var(--rose);
  text-transform: uppercase; margin-bottom: 24px; font-weight: 500;
}
.series-title {
  font-size: 56px; font-weight: 600; color: var(--rose-deep);
  letter-spacing: 0.08em; line-height: 1.3; margin-bottom: 20px;
}
.series-sub {
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  font-size: 22px; color: var(--ink-soft); letter-spacing: 0.05em;
  margin-bottom: 36px;
}
.series-blurb {
  max-width: 520px; margin: 0 auto;
  font-size: 17px; line-height: 2; color: var(--ink-soft);
}
```

---

## 2. Table of Contents（目錄）

`index.html` 的章節列表。

```html
<section class="toc">
  <h2 class="toc-title">目 錄</h2>
  <ol class="chapter-list">
    <li>
      <a href="chapter-01.html">
        <span class="ch-num">第 一 章</span>
        <span class="ch-name">章節標題</span>
        <span class="ch-meta">3,200 字</span>
      </a>
    </li>
    <li>
      <a href="chapter-02.html">
        <span class="ch-num">第 二 章</span>
        <span class="ch-name">章節標題</span>
        <span class="ch-meta">2,800 字</span>
      </a>
    </li>
  </ol>
</section>
```

```css
.toc { max-width: 720px; margin: 0 auto; padding: 80px 28px; }
.toc-title {
  text-align: center; font-size: 24px; font-weight: 500;
  color: var(--rose-deep); letter-spacing: 0.4em; margin-bottom: 56px;
}
.chapter-list { list-style: none; padding: 0; margin: 0; }
.chapter-list li { border-bottom: 1px solid var(--rule); }
.chapter-list li:first-child { border-top: 1px solid var(--rule); }
.chapter-list a {
  display: grid; grid-template-columns: 100px 1fr auto;
  gap: 24px; align-items: center;
  padding: 24px 16px;
  color: var(--ink); text-decoration: none;
  transition: background 0.2s;
}
.chapter-list a:hover { background: var(--paper); }
.ch-num { font-size: 13px; letter-spacing: 0.2em; color: var(--rose); font-weight: 500; }
.ch-name { font-size: 18px; color: var(--ink); font-weight: 500; }
.ch-meta { font-size: 13px; color: var(--ink-soft); letter-spacing: 0.1em; }

@media (max-width: 640px) {
  .chapter-list a { grid-template-columns: 1fr; gap: 6px; padding: 20px 8px; }
  .ch-num, .ch-meta { font-size: 12px; }
  .ch-name { font-size: 16px; }
}
```

---

## 3. Chapter Hero（章節封面）

每章開頭的儀式感封面。

```html
<section class="chapter-hero">
  <div class="chapter-num">第 一 章</div>
  <h1 class="chapter-title">章節標題</h1>
  <div class="chapter-sub">章節副標 italic</div>
  <div class="hero-divider"></div>
</section>
```

```css
.chapter-hero {
  text-align: center; padding: 120px 28px 80px;
}
.chapter-num {
  font-size: 14px; letter-spacing: 0.5em; color: var(--rose);
  margin-bottom: 32px; font-weight: 500;
}
.chapter-title {
  font-size: 48px; font-weight: 600; color: var(--rose-deep);
  letter-spacing: 0.06em; line-height: 1.5; margin-bottom: 24px;
}
.chapter-sub {
  font-family: 'Cormorant Garamond', serif; font-style: italic;
  font-size: 20px; color: var(--ink-soft); letter-spacing: 0.05em;
}
```

---

## 4. Chapter Navigation（上下章導航）

每章底部的固定導航條。

```html
<nav class="chapter-nav">
  <a href="chapter-01.html" class="nav-prev">‹ 上一章 · 第一章</a>
  <a href="index.html" class="nav-toc">目錄</a>
  <a href="chapter-03.html" class="nav-next">下一章 · 第三章 ›</a>
</nav>
```

```css
.chapter-nav {
  max-width: 720px; margin: 80px auto 60px; padding: 32px 28px;
  display: grid; grid-template-columns: 1fr auto 1fr;
  gap: 24px; align-items: center;
  border-top: 1px solid var(--rule); border-bottom: 1px solid var(--rule);
}
.chapter-nav a {
  color: var(--rose-deep); text-decoration: none;
  font-size: 15px; letter-spacing: 0.1em;
  transition: opacity 0.2s;
}
.chapter-nav a:hover { opacity: 0.6; }
.chapter-nav .nav-prev { text-align: left; }
.chapter-nav .nav-toc { text-align: center; color: var(--ink-soft); }
.chapter-nav .nav-next { text-align: right; }

@media (max-width: 640px) {
  .chapter-nav { grid-template-columns: 1fr; gap: 12px; text-align: center; }
  .chapter-nav .nav-prev, .chapter-nav .nav-next { text-align: center; }
}
```

第一章 `nav-prev` 隱藏（用 `<span class="nav-prev"></span>` 佔位），最後一章 `nav-next` 改成「全文完」。

---

## 5. Reading Progress Bar（閱讀進度條）

頂部固定的細線進度條，隨滾動延伸。

```html
<div class="progress-bar"><div class="progress-fill" id="progress"></div></div>

<script>
window.addEventListener('scroll', () => {
  const scrolled = window.scrollY;
  const total = document.documentElement.scrollHeight - window.innerHeight;
  const pct = (scrolled / total) * 100;
  document.getElementById('progress').style.width = pct + '%';
});
</script>
```

```css
.progress-bar {
  position: fixed; top: 0; left: 0; right: 0; height: 3px;
  background: transparent; z-index: 1000;
}
.progress-fill {
  height: 100%; width: 0; background: var(--rose);
  transition: width 0.1s ease-out;
}
```

---

## 章節頁範本

`chapter-01.html`：

```html
<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="robots" content="noindex, nofollow">
  <title>第一章 ｜ 小說名</title>
  <!-- Google Fonts + 完整 CSS（從 references/01-components.md 複製過來） -->
  <style>
    /* :root 變數、所有元件 CSS、連載擴充 CSS */
  </style>
</head>
<body>

  <!-- 進度條 -->
  <div class="progress-bar"><div class="progress-fill" id="progress"></div></div>

  <!-- 章節封面 -->
  <section class="chapter-hero">
    <div class="chapter-num">第 一 章</div>
    <h1 class="chapter-title">章節標題</h1>
    <div class="chapter-sub">副標</div>
    <div class="hero-divider"></div>
  </section>

  <!-- 章節內文 -->
  <div class="container">
    <section class="scene"><p>...</p></section>
    <div class="dialogue left">
      <div class="speaker">角色</div>
      <div class="bubble">「對白」</div>
    </div>
    <!-- 各種元件交錯（散文/對話/金句/信件）-->
  </div>

  <!-- 章節底部導航 -->
  <nav class="chapter-nav">
    <span class="nav-prev"></span>     <!-- 第一章沒有上一章 -->
    <a href="index.html" class="nav-toc">目錄</a>
    <a href="chapter-02.html" class="nav-next">下一章 · 第二章 ›</a>
  </nav>

  <script>
    window.addEventListener('scroll', () => {
      const pct = (window.scrollY / (document.documentElement.scrollHeight - window.innerHeight)) * 100;
      document.getElementById('progress').style.width = pct + '%';
    });
  </script>

</body>
</html>
```

---

## 寫作節奏建議（每章排版）

| 位置 | 元件 |
|---|---|
| 章節最頂 | Chapter Hero |
| 1-2 段散文進場 | Scene |
| 角色互動 | Dialogue × 2-3 |
| 場景轉換 | Ornament `・ ・ ・` |
| 中段 | Pull Quote 或 Callout（章節主旨）|
| 後段對話／衝突 | Dialogue × 2-3 |
| 章末抒情 | Letter Section（如有書信／心聲）|
| 章末收束 | Finale 或 直接 Chapter Nav |
| 章節最底 | Chapter Nav |

每章字數參考：

- 短章：1,500-2,500 字（速食小說、輕小說）
- 中章：2,500-4,000 字（一般網路小說）
- 長章：4,000-6,000 字（傳統長篇）

每章內部 **至少 3 個視覺斷點**（場景分隔／金句／對話框），不要整章純文字塊。

---

## v2 擴充想法（待實作）

- 章節間轉場動畫（fade / slide）
- 書籤系統（localStorage 記住讀到第幾段）
- 字級調整（讀者調 18px / 21px / 24px）
- 夜間模式切換
- 章節閱讀計時器
- 章節評論（Disqus / Giscus）
- 多人協作章節（不同作者寫不同章）
