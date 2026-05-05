# 元件全集 · CSS + HTML 範本

所有元件的完整 CSS 和 HTML 範例。直接 copy 到你的專案使用。

---

## CSS 變數（放 `<style>` 開頭）

```css
:root {
  /* 康乃馨淡色（預設）*/
  --bg:        #FBF6F0;    /* 暖奶白底 */
  --paper:     #FFFCF7;    /* 卡片底 */
  --petal:     #F5DCDC;    /* 主色：花瓣淡粉 */
  --petal-soft:#FAEAEA;    /* 次粉 */
  --petal-warm:#F4E1D8;    /* 暖橘粉 */
  --rose:      #C28A85;    /* accent 玫瑰 */
  --rose-deep: #9E5F5A;    /* 標題深玫瑰 */
  --leaf:      #B8C2A8;    /* 葉綠點綴 */
  --ink:       #3D332E;    /* 主文字 */
  --ink-soft:  #7A6B62;    /* 次文字 */
  --rule:      #E8D9D2;    /* 分隔線 */
}
```

換主題只改 `--petal / --rose / --rose-deep` 三個值。

---

## Base styles

```css
* { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  font-family: 'Noto Serif TC', 'Songti TC', 'PingFang TC', serif;
  color: var(--ink);
  background: var(--bg);
  background-image:
    radial-gradient(ellipse at 10% 0%, rgba(245,220,220,0.4) 0%, transparent 50%),
    radial-gradient(ellipse at 90% 100%, rgba(184,194,168,0.15) 0%, transparent 60%);
  line-height: 1.95;
  -webkit-font-smoothing: antialiased;
  overflow-x: hidden;
}

.container { max-width: 720px; margin: 0 auto; padding: 0 28px; }
```

字體載入：

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+TC:wght@300;400;500;600;700&family=Cormorant+Garamond:ital,wght@0,400;0,500;1,400&display=swap" rel="stylesheet">
```

---

## 1. Hero（封面區）

```html
<section class="hero">
  <svg class="hero-flower" viewBox="0 0 96 96" xmlns="http://www.w3.org/2000/svg">
    <path d="M48 70 Q36 62 32 50" stroke="#B8C2A8" stroke-width="2" fill="none" stroke-linecap="round"/>
    <ellipse cx="32" cy="56" rx="9" ry="3.5" fill="#B8C2A8" opacity="0.6" transform="rotate(-30 32 56)"/>
    <ellipse cx="56" cy="62" rx="7" ry="3" fill="#B8C2A8" opacity="0.5" transform="rotate(35 56 62)"/>
    <g opacity="0.9">
      <path d="M48 18 Q32 24 32 36 Q32 44 48 44 Q64 44 64 36 Q64 24 48 18 Z" fill="#F5DCDC"/>
      <path d="M48 22 Q36 28 36 36 Q36 42 48 42 Q60 42 60 36 Q60 28 48 22 Z" fill="#F0CECE"/>
      <path d="M48 26 Q40 30 40 36 Q40 40 48 40 Q56 40 56 36 Q56 30 48 26 Z" fill="#E8B8B8"/>
      <path d="M32 30 L34 28 L36 30 L38 27 L40 30 L42 26 L44 30 L46 26 L48 30 L50 26 L52 30 L54 27 L56 30 L58 28 L60 30 L62 28"
            stroke="#E8B8B8" stroke-width="1" fill="none" opacity="0.7"/>
    </g>
    <circle cx="48" cy="34" r="2.5" fill="#C28A85"/>
    <path d="M48 44 L48 84" stroke="#B8C2A8" stroke-width="2"/>
  </svg>
  <div class="hero-meta">2026 年 ・ 母親節快樂</div>
  <h1>
    <span class="line">主標第一行</span>
    <span class="line">主標第二行</span>
  </h1>
  <div class="hero-sub">副標 italic</div>
  <div class="hero-divider"></div>
</section>
```

```css
.hero { text-align: center; padding: 100px 28px 80px; }
.hero-flower { width: 88px; height: 88px; margin: 0 auto 32px; display: block; }
.hero-meta {
  font-size: 14px; letter-spacing: 0.4em; color: var(--rose);
  text-transform: uppercase; margin-bottom: 24px; font-weight: 500;
}
.hero h1 {
  font-size: 42px; font-weight: 600; color: var(--rose-deep);
  letter-spacing: 0.06em; line-height: 1.5; margin-bottom: 28px;
}
.hero h1 .line { display: block; }
.hero h1 .line + .line { margin-top: 8px; }
.hero-sub {
  font-family: 'Cormorant Garamond', 'Noto Serif TC', serif;
  font-style: italic; font-size: 20px; color: var(--ink-soft);
  letter-spacing: 0.05em;
}
.hero-divider { width: 50px; height: 1px; background: var(--rose); opacity: 0.5; margin: 40px auto 0; }
```

短標題（≤6 字）：`font-size: 64-72px`，單行，可拿掉 `.line` span。

---

## 2. Scene（散文段落）

```html
<section class="scene">
  <p>第一段...</p>
  <p>第二段...</p>
</section>
```

```css
.scene { padding: 36px 0; }
.scene p {
  font-size: 19px; line-height: 2.05; margin-bottom: 1.4em;
  color: var(--ink); text-align: justify; text-wrap: pretty;
}
.scene p:last-child { margin-bottom: 0; }
```

---

## 3. Dialogue（對話框）

```html
<div class="dialogue left">
  <div class="speaker">孩 子</div>
  <div class="bubble child">「對白內容」</div>
</div>

<div class="dialogue right">
  <div class="speaker">媽媽</div>
  <div class="bubble mom">「對白內容」</div>
</div>
```

```css
.dialogue { margin: 36px 0; max-width: 580px; }
.dialogue.right { margin-left: auto; }
.dialogue.left  { margin-right: auto; }
.speaker {
  font-size: 12px; letter-spacing: 0.3em; color: var(--rose-deep);
  margin-bottom: 10px; font-weight: 500;
}
.dialogue.right .speaker { text-align: right; }

.bubble {
  background: var(--paper); border: 1px solid var(--petal);
  padding: 24px 28px; border-radius: 12px; font-size: 18px; line-height: 1.95;
  position: relative; box-shadow: 0 4px 16px rgba(194,138,133,0.08);
}
.bubble.child {
  background: linear-gradient(135deg, var(--paper) 0%, #FBF1EE 100%);
  border-color: var(--petal-warm);
}
.bubble.mom {
  background: linear-gradient(135deg, var(--petal-soft) 0%, var(--paper) 100%);
  border-color: var(--petal);
}

.bubble::after {
  content: ''; position: absolute; bottom: -8px; width: 14px; height: 14px;
  transform: rotate(45deg); background: inherit;
  border-right: 1px solid; border-bottom: 1px solid; border-color: inherit;
}
.dialogue.left  .bubble::after { left: 32px;  border-color: var(--petal-warm); background: #FBF1EE; }
.dialogue.right .bubble::after { right: 32px; border-color: var(--petal); background: var(--petal-soft); }
```

---

## 4. Pull Quote（金句框）

```html
<div class="pullquote">
  <div class="quote-text">金句內容。</div>
</div>
```

```css
.pullquote {
  text-align: center; margin: 64px auto; padding: 0 24px; max-width: 640px;
}
.pullquote::before, .pullquote::after {
  content: ''; display: block; width: 40px; height: 1px;
  background: var(--rose); margin: 0 auto; opacity: 0.4;
}
.pullquote::before { margin-bottom: 28px; }
.pullquote::after  { margin-top: 28px; }
.pullquote .quote-text {
  font-size: 28px; line-height: 1.7; color: var(--rose-deep);
  font-weight: 500; letter-spacing: 0.06em;
}
```

---

## 5. Callout（強調句）

```html
<div class="callout">強調的話<br>分兩行。</div>
```

```css
.callout {
  text-align: center; margin: 48px 0;
  font-size: 24px; line-height: 1.7; color: var(--rose-deep);
  font-weight: 500; letter-spacing: 0.05em;
}
```

---

## 6. Contrast Grid（兩欄對比）

```html
<section class="scene">
  <div class="contrast">
    <div class="contrast-col">
      <h3>標 題 一</h3>
      <p>內容一</p>
    </div>
    <div class="contrast-divider"></div>
    <div class="contrast-col">
      <h3>標 題 二</h3>
      <p>內容二</p>
    </div>
  </div>
</section>
```

```css
.contrast { display: grid; grid-template-columns: 1fr 1px 1fr; gap: 32px; align-items: start; margin: 56px 0; }
.contrast-col { text-align: center; }
.contrast-col h3 { font-size: 18px; color: var(--rose-deep); font-weight: 600; margin-bottom: 18px; letter-spacing: 0.15em; }
.contrast-col p  { font-size: 17px; line-height: 1.95; color: var(--ink); text-align: center !important; }
.contrast-divider { width: 1px; background: var(--rule); }
```

行動版要在 `@media (max-width: 640px)` 改成單欄並讓 divider 變橫線。

---

## 7. Letter Section（信件區塊）

```html
<div class="letter-section">
  <p>信件內容...</p>
  <p class="letter-keyline">中段金句</p>
  <p>更多內容...</p>
</div>
```

```css
.letter-section {
  margin: 80px 0 60px; padding: 56px 48px 48px;
  background: var(--paper); border: 1px solid var(--petal);
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(194,138,133,0.06), 0 16px 48px rgba(194,138,133,0.08);
  position: relative;
}
.letter-section::before {
  content: '致 媽 媽'; position: absolute; top: -12px; left: 50%;
  transform: translateX(-50%); background: var(--bg); color: var(--rose-deep);
  font-size: 13px; letter-spacing: 0.4em; padding: 0 16px; font-weight: 500;
}
.letter-section::after {
  content: ''; position: absolute; top: 24px; left: 24px; right: 24px; bottom: 24px;
  border: 1px solid var(--petal-soft); border-radius: 2px; pointer-events: none;
}
.letter-section p { font-size: 18px; line-height: 2.05; margin-bottom: 1.4em; text-align: justify; position: relative; z-index: 1; }
.letter-keyline {
  text-align: center !important; font-size: 22px !important; color: var(--rose-deep) !important;
  font-weight: 500; letter-spacing: 0.05em; margin: 24px 0 !important; line-height: 1.7 !important;
}
```

`::before` 內容可改：「致 媽 媽」「給 母 親」「親 愛 的 媽 媽」等。

---

## 8. Ornament（場景分隔）

```html
<div class="ornament">・ ・ ・</div>
```

```css
.ornament {
  text-align: center; margin: 48px 0;
  color: var(--rose); opacity: 0.5; letter-spacing: 0.6em; font-size: 14px;
}
```

---

## 9. Scene Label（場景小標）

```html
<section class="scene">
  <div class="scene-label">場 景 一</div>
  <p>...</p>
</section>
```

```css
.scene-label {
  text-align: center; font-size: 12px; letter-spacing: 0.5em;
  color: var(--rose); opacity: 0.6; margin-bottom: 24px;
  text-transform: uppercase; font-weight: 500;
}
```

---

## 10. Finale（畫框外結尾）

```html
<section class="finale">
  <svg class="finale-flower" viewBox="0 0 64 64" xmlns="http://www.w3.org/2000/svg">
    <g opacity="0.9">
      <path d="M32 14 Q22 18 22 26 Q22 32 32 32 Q42 32 42 26 Q42 18 32 14 Z" fill="#F5DCDC"/>
      <path d="M32 16 Q24 20 24 26 Q24 30 32 30 Q40 30 40 26 Q40 20 32 16 Z" fill="#F0CECE"/>
      <path d="M32 18 Q26 22 26 26 Q26 28 32 28 Q38 28 38 26 Q38 22 32 18 Z" fill="#E8B8B8"/>
    </g>
    <circle cx="32" cy="25" r="2" fill="#C28A85"/>
    <path d="M32 32 L32 56" stroke="#B8C2A8" stroke-width="1.5"/>
  </svg>
  <p class="closing-line">
    結尾金句第一行，
    <span class="second">第二行收束。</span>
  </p>
</section>
```

```css
.finale { text-align: center; padding: 120px 28px 80px; }
.finale-flower { width: 56px; margin: 0 auto 56px; display: block; opacity: 0.85; }
.finale .closing-line {
  font-size: 38px; line-height: 1.7; color: var(--rose-deep);
  letter-spacing: 0.1em; font-weight: 500;
}
.finale .closing-line .second { display: block; margin-top: 1.6em; }
```

---

## 11. Signature（署名）

```html
<footer class="signature">
  — 你 的 名 字
</footer>
```

```css
.signature {
  text-align: center; padding: 0 28px 100px;
  font-size: 14px; letter-spacing: 0.3em;
  color: var(--ink-soft); font-weight: 500;
}
```

不署名時整段省略（不要留空 footer）。

---

## 行動版適配

```css
@media (max-width: 640px) {
  .container { padding: 0 20px; }

  .hero { padding: 64px 20px 56px; }
  .hero h1 { font-size: 30px; line-height: 1.5; letter-spacing: 0.04em; }
  .hero h1 .line + .line { margin-top: 6px; }
  .hero-sub { font-size: 16px; }
  .hero-flower { width: 72px; height: 72px; }

  .scene { padding: 28px 0; }
  .scene p { font-size: 17px; line-height: 2; }

  .dialogue { margin: 28px 0; max-width: 100%; }
  .bubble { padding: 20px 22px; font-size: 16px; }

  .pullquote { margin: 48px auto; }
  .pullquote .quote-text { font-size: 22px; }
  .callout { font-size: 20px; }

  .contrast { grid-template-columns: 1fr; gap: 24px; }
  .contrast-divider { width: 40px; height: 1px; margin: 0 auto; }
  .contrast-col h3 { font-size: 16px; }
  .contrast-col p  { font-size: 16px; }

  .letter-section { padding: 44px 28px 32px; margin: 56px -8px 48px; }
  .letter-section::after { top: 16px; left: 16px; right: 16px; bottom: 16px; }
  .letter-section p { font-size: 16px; }
  .letter-keyline { font-size: 18px !important; }

  .finale { padding: 80px 20px 60px; }
  .finale .closing-line { font-size: 26px; line-height: 1.85; }
}
```

---

## 排版節奏

每篇文章建議的元件分佈：

| 位置 | 元件 |
|---|---|
| 開場 | Hero |
| 1-2 段後 | 第一個對話（如有對話）|
| 3-4 段後 | Ornament `・ ・ ・` |
| 段落中 | 偶爾插入 callout |
| 中段 | Contrast Grid（如有 A vs B 對比結構）|
| 中後段 | Pull Quote（情緒高點，1-2 個）|
| 結尾前 | Letter Section（給媽媽的告白）|
| 收束 | Finale（畫框外）|
| 最底 | Signature |

節奏鐵律：

- 兩個 dialogue 之間至少夾一段 scene 或一個 ornament
- pull quote 和 callout 不要連續用
- letter section 全篇至多 1 次
- 對話框集中在「衝突場景」，反思段落用 pull quote
