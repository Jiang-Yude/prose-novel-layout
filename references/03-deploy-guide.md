# 部署指南 · 如何把網頁放到網路上

把寫好的母親節 HTML 變成可以分享的網址。這份是教學＋建議。

---

## 怎麼選？一句話建議

> **沒有特殊需求 → Netlify Drop（30 秒搞定）**
> **想要好記網址、之後會更新 → GitHub Pages**
> **要 SSO 保護不公開 → Vercel**

| 方法 | 難度 | 速度 | 要不要帳號 | 適合 |
|---|---|---|---|---|
| **Netlify Drop** | ⭐ 最簡單 | 30 秒 | 體驗免，永久保留要免費註冊 | 第一次做、不會 git、母親節當天臨時做 |
| **GitHub Pages** | ⭐⭐ | 3 分鐘 | 要 GitHub 帳號 | 想要好記網址、要更新文章、要版控 |
| **Vercel** | ⭐⭐⭐ | 5 分鐘 | 要 Vercel 帳號 | 要 SSO 保護、自訂網域 |

---

## 方法 1 · Netlify Drop（推薦給第一次的人）

> **網址：[https://app.netlify.com/drop](https://app.netlify.com/drop)**

完全免費、免註冊、拖曳就好。**這是最簡單的方式**，30 秒拿到分享網址。

### 教學步驟

**Step 1**：打開瀏覽器，到 [https://app.netlify.com/drop](https://app.netlify.com/drop)

你會看到一個大方框，上面寫「Drag and drop your site folder here」。

**Step 2**：把你的母親節網頁資料夾**整個拖進方框**

- 如果只有 `index.html` 一個檔案 → 直接拖那個檔案進去也可以
- 有多個檔案（`index.html` + `robots.txt` + 圖片）→ 拖整個資料夾，不要只拖一個檔案

**Step 3**：等 5-10 秒上傳

進度條跑完會自動跳到「Site is live」畫面。

**Step 4**：複製分享網址

網址長這樣：`https://random-name-12345.netlify.app/`

點一下複製，就可以貼給媽媽了。

### 注意事項

- **24 小時保留**：免註冊版的網站只會留 24 小時，過期會消失
- **永久保留**：免費註冊一個 Netlify 帳號（Google 登入即可），之後上傳的網站就不會過期
- **想換好記的網址**：在 Netlify 後台 → Site settings → Change site name，可以改成 `https://my-mom-letter-2026.netlify.app/` 之類
- **更新內容**：把整個資料夾再拖一次到同一個網站就會覆蓋

### 適合誰

- ✅ 完全不會 git、不會用 terminal 的人
- ✅ 母親節當天臨時想做一個給媽媽
- ✅ 一次性、不打算之後改的內容
- ✅ 不想創 GitHub 帳號

---

## 方法 2 · GitHub Pages（推薦給會用 git 的人）

免費、可更新、有版本控制、網址好記。

### 前置準備

需要：

1. 一個 [GitHub 帳號](https://github.com/signup)（免費）
2. 安裝 [GitHub CLI](https://cli.github.com/)
   - Mac: `brew install gh`
   - Windows: 從官網下載安裝檔
3. 登入：terminal 跑 `gh auth login` → 照畫面選 GitHub.com → 用瀏覽器授權

### 教學步驟

假設你的母親節網頁資料夾叫 `my-mothersday-2026/`，裡面有 `index.html`。

**Step 1**：進到資料夾，初始化 git

```bash
cd my-mothersday-2026
git init -b main
```

**Step 2**：加 `.gitignore`（避免不該上傳的檔案被推上去）

```bash
cat > .gitignore <<EOF
.DS_Store
node_modules/
.vercel/
.env
*.log
EOF
```

**Step 3**：第一次 commit

```bash
git add .
git commit -m "母親節 2026 首發"
```

**Step 4**：在 GitHub 創 repo 並推上去

```bash
gh repo create my-mothersday-2026 --public --source=. --push
```

`--public` 是公開（GitHub Pages 免費版需要 public repo），但加了 `noindex` meta 和 `robots.txt` 就不會被搜尋引擎找到（見下方「隱蔽分享」）。

**Step 5**：開啟 Pages

```bash
gh api -X POST "repos/<你的帳號>/my-mothersday-2026/pages" \
  -f "source[branch]=main" \
  -f "source[path]=/"
```

把 `<你的帳號>` 換成你的 GitHub username。

**Step 6**：等部署完成（1-3 分鐘）

```bash
URL="https://<你的帳號>.github.io/my-mothersday-2026/"
until [ "$(curl -s -o /dev/null -w '%{http_code}' "$URL")" = "200" ]; do
  echo "等部署中..."
  sleep 5
done
echo "上線了！$URL"
```

完成後網址：`https://<你的帳號>.github.io/my-mothersday-2026/`

### 隱蔽分享（不被搜尋引擎收錄）

母親節文章是私人內容，知道網址才看得到，不希望陌生人 Google 到。三層保護：

**1. HTML 加 noindex meta**

在 `index.html` 的 `<head>` 加：

```html
<meta name="robots" content="noindex, nofollow">
```

**2. robots.txt**

在資料夾根目錄加 `robots.txt`：

```
User-agent: *
Disallow: /
```

**3. Repo 命名不要太好猜**

❌ 不好的命名：`give-mom-a-letter`、`mothers-day-2026`、`for-my-mom`
✅ 好的命名：`my-mothersday-2026`、`my-letter-2026`、`my-2026-may-04`

加完這三層後，網址只有你主動分享給家人的人會看到。

### 更新內容

寫完／改完文章後：

```bash
cd my-mothersday-2026
git add .
git commit -m "更新文章內容"
git push
```

GitHub Pages 自動部署，1-3 分鐘後新版本上線。

### 自訂網域（選用）

如果你有自己的網域（例如 `letter.example.com`）：

1. 在 repo 根目錄加 `CNAME` 檔，內容是你的網域：
   ```
   letter.example.com
   ```
2. 在你的 DNS 服務商加一筆 CNAME 紀錄：
   ```
   letter   CNAME   <你的帳號>.github.io
   ```
3. 等 DNS propagate（5-30 分鐘）

---

## 方法 3 · Vercel（要 SSO 保護才用）

如果你需要：

- **SSO 保護**（家人要登入 Vercel 帳號才能看）
- 自訂域名 + HTTPS
- 動態功能（API、表單、伺服端渲染）

### 教學步驟

**最簡單方式**（拖曳上傳，跟 Netlify Drop 類似）：

1. 打開 [https://vercel.com/new](https://vercel.com/new)
2. 先免費註冊一個帳號（用 GitHub / Google / Email 都可以）
3. 選 **Drop a folder**
4. 把資料夾拖進去
5. 點 Deploy，等 30 秒
6. 拿到 `xxx.vercel.app` 網址

**用 CLI 方式**：

```bash
npm i -g vercel
cd my-mothersday-2026
vercel --prod
```

第一次會問一些設定，按預設選即可。

### 開啟 SSO 保護

進 Vercel dashboard → Settings → **Deployment Protection** → Enable。

設了之後別人要登入自己的 Vercel 帳號才能看你的網頁。適合：

- 只想給特定家人看
- 不希望任何陌生人看到
- 比 GitHub Pages + noindex 更嚴格的隱私

但缺點：每個看的人要先有 Vercel 帳號，技術門檻較高。

---

## 三種方法快速比較

| 情境 | 用哪個 |
|---|---|
| 完全不會技術，想要最快做出網址 | Netlify Drop |
| 母親節當天臨時做一個 | Netlify Drop |
| 之後可能會改文字內容 | GitHub Pages |
| 想要「自己帳號名稱」的網址 | GitHub Pages |
| 想要長期保留、版本控制 | GitHub Pages |
| 不希望任何陌生人看到 | Vercel + SSO |
| 想用自己網域 | GitHub Pages 或 Vercel |
| 第一次做，沒有特殊需求 | **Netlify Drop** |

---

## 常見問題

### Q：404 / Pages 沒上線？

A：等 5 分鐘以上，第一次部署有時較慢。還是 404 的話，檢查 GitHub Pages 狀態：

```bash
gh api "repos/<owner>/<repo>/pages" --jq '.status'
```

`built` 表示成功，`errored` 表示失敗，看 actions log：

```bash
gh run list --repo <owner>/<repo>
```

### Q：改了 HTML 但網站沒更新？

A：瀏覽器快取。網址加 `?v=隨便數字` 強制重抓：

```
https://<owner>.github.io/<repo>/?v=2
```

或用無痕視窗開。

### Q：圖片要上傳？

A：把圖片放進資料夾（建議 `assets/` 子資料夾），HTML 用相對路徑引用：

```html
<img src="assets/mom-photo.jpg" alt="媽媽和我">
```

注意：

- GitHub Pages 是 public，圖片任何人有連結都能看
- 隱私圖建議走 Vercel + SSO，或用浮水印
- 圖片大小建議 < 500KB（可用 [tinypng.com](https://tinypng.com/) 壓縮）

### Q：免費版有流量限制嗎？

| 平台 | 免費額度 |
|---|---|
| GitHub Pages | 每月 100GB 流量 / 1GB 容量 |
| Netlify | 每月 100GB 流量 / 100,000 個 build minutes |
| Vercel | 每月 100GB 流量 / 6,000 個 build minutes |

一般母親節文章遠遠用不到。

### Q：可以放 YouTube 影片嗎？

A：可以，用 iframe 嵌入即可：

```html
<iframe width="560" height="315"
        src="https://www.youtube.com/embed/影片ID"
        frameborder="0" allowfullscreen></iframe>
```

但要記得在母親節網頁裡用，會打斷閱讀節奏，謹慎使用。

---

## 部署完成 checklist

部署完前先確認：

- [ ] HTML 在本地正確顯示（雙擊檔案開瀏覽器測試）
- [ ] 手機看排版正常（Chrome devtools → 切手機尺寸）
- [ ] `<meta name="robots" content="noindex, nofollow">` 已加
- [ ] `robots.txt` 已加（如果要隱蔽）
- [ ] 圖片路徑正確
- [ ] 標題、署名都對

部署完後：

- [ ] 用瀏覽器打開部署網址確認顯示正常
- [ ] 手機開一次確認 RWD
- [ ] 把網址傳給該看的人

---

## 推薦給長輩看的方法

如果是要傳給媽媽自己看：

1. 用 Netlify Drop 或 GitHub Pages 上線
2. 拷貝網址
3. **建議用 LINE 或訊息傳給媽媽**，不要只貼裸網址
4. 訊息範本：

```
媽媽，
我寫了一篇東西給妳，
寫得不夠好但是真心，
看完就好，不用回我。

[網址]

母親節快樂 🌸
```

5. 如果媽媽不會用網頁、只用 LINE：可以用瀏覽器開好網址後，截圖長截圖傳給她，或者直接傳網頁所有內容貼到 LINE
