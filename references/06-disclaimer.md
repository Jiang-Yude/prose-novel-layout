# 免責聲明區塊（Disclaimer Block）

當使用 Mode C 課題分離信件模式生成網頁時，**必須**在頁面底部附上免責聲明。

---

## 為什麼一定要加

這個 skill 處理的是人際關係、心理糾結、情緒整理——這些是**心理諮商的領域**。

我們提供的是**排版工具**，不是專業治療。讀者可能：

- 有更深的心結（PTSD、家暴、長期壓抑）→ 需要專業協助
- 把「寫信」當成解決問題的捷徑 → 過度依賴工具
- 寄信後對方反應很糟 → 二次傷害
- 把這個 skill 的邏輯誤解為心理治療標準

加上免責聲明可以：

- 設定使用者期望（這是輔助，不是治療）
- 鼓勵使用者真有需要時找專業
- 保護自己（工具作者）不被誤解為心理師
- 給讀者邊界感（這是別人的故事，不是普世真理）

---

## 標準免責聲明 HTML

```html
<!-- ====== 免責聲明（網頁底部） ====== -->
<section class="disclaimer">
  <div class="container">
    <h3>關於這封信</h3>
    <p>這封信是用 <a href="https://github.com/Jiang-Yude/prose-novel-layout" target="_blank">prose-novel-layout</a> 的「課題分離信件模式」寫的。</p>
    <p><strong>這不是心理諮商工具</strong>，只是一個幫人把感受寫得更清楚的輔助。如果你也有類似的糾結，這個工具可以陪你走一遍——但真的有強烈心結，請找專業心理師。</p>
    <p>信寫了不一定要寄。對方接不接受，是對方的課題；自己有沒有想清楚，是自己的課題。</p>
    <p class="disclaimer-resource">需要專業協助：<a href="https://www.tsh.org.tw/" target="_blank">台灣自殺防治學會</a> ・ <a href="https://www.lifeline.org.tw/" target="_blank">張老師 1980</a> ・ <a href="https://1925.mohw.gov.tw/" target="_blank">安心專線 1925</a></p>
  </div>
</section>
```

## 對應 CSS

```css
.disclaimer {
  background: var(--paper);
  border-top: 1px solid var(--rule);
  padding: 60px 28px 80px;
  margin-top: 80px;
}
.disclaimer h3 {
  font-size: 16px;
  letter-spacing: 0.3em;
  color: var(--rose-deep);
  margin-bottom: 24px;
  text-align: center;
  font-weight: 500;
}
.disclaimer p {
  font-size: 15px;
  line-height: 2;
  color: var(--ink-soft);
  margin-bottom: 1em;
  max-width: 600px;
  margin-left: auto;
  margin-right: auto;
}
.disclaimer p:last-child { margin-bottom: 0; }
.disclaimer a {
  color: var(--rose-deep);
  text-decoration: underline;
  text-underline-offset: 3px;
}
.disclaimer .disclaimer-resource {
  font-size: 13px;
  color: var(--ink-soft);
  text-align: center;
  margin-top: 24px;
  letter-spacing: 0.05em;
}

@media (max-width: 640px) {
  .disclaimer { padding: 40px 20px 60px; }
  .disclaimer p { font-size: 14px; }
  .disclaimer .disclaimer-resource { font-size: 12px; }
}
```

---

## 在地化資源

不同國家／地區的專業協助資源不同。範本內建台灣資源，使用者可以自己換：

### 台灣（預設）

- 台灣自殺防治學會：https://www.tsh.org.tw/
- 張老師專線：1980
- 安心專線：1925
- 衛福部諮商心理師查詢：https://dep.mohw.gov.tw/DOMHW/cp-4691-78174-107.html

### 中國大陸

- 北京心理危機研究與干預中心：010-82951332
- 全國心理援助熱線：400-161-9995

### 香港

- 香港撒瑪利亞防止自殺會：23892222
- 生命熱線：23820000

### 其他

替換時要注意：

- 連結要可用（不要放失效網址）
- 電話要正確
- 不要放廣告型 / 商業諮商機構（保持中立）

---

## 簡易版（適合單篇文章）

如果不想佔太多版面，最低標版本：

```html
<section class="disclaimer-mini">
  <p>※ 這是一封用「課題分離」的角度整理出來的信，不是心理諮商。<br>
  真的有強烈心結，建議找專業心理師。</p>
  <p>用 <a href="https://github.com/Jiang-Yude/prose-novel-layout" target="_blank">prose-novel-layout</a> 排版。</p>
</section>
```

```css
.disclaimer-mini {
  text-align: center;
  font-size: 13px;
  color: var(--ink-soft);
  padding: 40px 28px 60px;
  border-top: 1px solid var(--rule);
  margin-top: 60px;
  line-height: 1.85;
}
.disclaimer-mini p { margin-bottom: 1em; }
.disclaimer-mini a { color: var(--rose-deep); }
```

---

## 工作流程禁忌

不要：

- ❌ 跳過免責聲明（不論完整版還是簡易版，至少要有一個）
- ❌ 把免責聲明寫得很正式像條款（讓人有壓力，也沒人讀）
- ❌ 替使用者選擇要不要寄信（永遠是「不一定要寄」）
- ❌ 暗示這個工具能解決所有問題
- ❌ 不附專業資源連結
