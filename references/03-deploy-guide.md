# 部署指南

把母親節網頁上線。三種方法，從最簡單排到最進階：

| 方法 | 難度 | 速度 | 適合 |
|---|---|---|---|
| **Netlify Drop** | ⭐ 最簡單 | 30 秒 | 完全不會 git，只想要一個分享網址 |
| **GitHub Pages** | ⭐⭐ | 3 分鐘 | 想要好記網址、要更新內容、要版本控制 |
| **Vercel** | ⭐⭐⭐ | 5 分鐘 | 要 SSO 保護、自訂網域、進階功能 |

---

## 方法 1 · Netlify Drop（最簡單，不用帳號）

完全免費、免註冊、拖曳就好。**這是最簡單的方式**。

### 步驟

1. 打開 [https://app.netlify.com/drop](https://app.netlify.com/drop)
2. 把你的 HTML 檔案（或整個資料夾）**拖進網頁中央的方框**
3. 等 5-10 秒，網址出現

完成。網址會像 `https://random-name-12345.netlify.app/`。

### 注意

- 免註冊版的網站會在 24 小時後過期。要永久保留就免費註冊一個帳號（Google 登入即可）
- 註冊後回到 Drop 頁面，拖一次就會永久保留
- 想換網址：在 Netlify 後台 → Site settings → Change site name

### 適合誰

- 完全不會 git、不會用 terminal 的人
- 母親節當天臨時想做一個給媽媽
- 一次性、不打算之後改的內容

---

## 方法 2 · GitHub Pages（推薦給會用 git 的人）

免費、可更新、有版本控制、網址好記。

### 前置

- 一個 GitHub 帳號
- 安裝 [GitHub CLI](https://cli.github.com/)（`brew install gh` on Mac，或從官網下載）
- `gh auth login` 登入帳號

---

### 標準流程

假設你的母親節網頁資料夾叫 `my-mothersday-2026/`，裡面有 `index.html`。

```bash
cd my-mothersday-2026

# 1. 初始化 git
git init -b main

# 2. 加 .gitignore
cat > .gitignore <<EOF
.DS_Store
node_modules/
.vercel/
.env
*.log
EOF

# 3. 第一次 commit
git add .
git commit -m "母親節 2026 首發"

# 4. 創 GitHub repo（public）並推上去
gh repo create my-mothersday-2026 --public --source=. --push

# 5. 開啟 Pages
gh api -X POST "repos/<你的帳號>/my-mothersday-2026/pages" \
  -f "source[branch]=main" \
  -f "source[path]=/"

# 6. 等部署完成（1-3 分鐘）
URL="https://<你的帳號>.github.io/my-mothersday-2026/"
until [ "$(curl -s -o /dev/null -w '%{http_code}' "$URL")" = "200" ]; do
  echo "等部署中..."
  sleep 5
done
echo "上線了！$URL"
```

把 `<你的帳號>` 換成你的 GitHub username。

---

### 隱蔽分享（不被搜尋引擎收錄）

母親節文章是私人內容，知道網址才看得到，不希望陌生人 Google 到。三層保護：

**1. HTML 加 noindex meta**：在 `index.html` 的 `<head>` 加：

```html
<meta name="robots" content="noindex, nofollow">
```

**2. robots.txt**：在資料夾根目錄加 `robots.txt`：

```
User-agent: *
Disallow: /
```

**3. Repo 命名不要太好猜**

不要叫 `give-mom-a-letter` 這種搜尋會中的名字。叫 `my-mothersday-2026`、`my-letter-2026`、或加流水號 `my-2026-may-04`。

加完這三層後，網址只有你主動分享給家人的人會看到，搜尋引擎不會收錄。

---

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

如果你有自己的網域（例如 `letter.example.com`），可以指向 GitHub Pages：

1. 在 repo 根目錄加 `CNAME` 檔，內容是你的網域：
   ```
   letter.example.com
   ```
2. 在你的 DNS 服務商加一筆 CNAME 紀錄：
   ```
   letter   CNAME   <你的帳號>.github.io
   ```
3. 等 DNS propagate（通常 5-30 分鐘）

---

---

## 方法 3 · Vercel

如果你需要：

- SSO 保護（只給特定人看，需要帳號才能進）
- 自訂域名 + HTTPS
- 動態功能（API、表單、伺服端渲染）

最簡單方式：

1. 打開 [https://vercel.com/new](https://vercel.com/new)（先免費註冊一個帳號）
2. 選 **Drop a folder**，把資料夾拖進去
3. 點 Deploy，等 30 秒

或用 CLI：

```bash
npm i -g vercel
cd my-mothersday-2026
vercel --prod
```

第一次會問一些設定，按預設選即可。完成後拿到 `xxx.vercel.app` 網址。

**SSO 保護**：進 Vercel dashboard → Settings → Deployment Protection → Enable。設了之後別人要登入 Vercel 帳號才能看，適合家庭群組看不想公開的內容。

---

## 常見問題

### Q：404 / Pages 沒上線？

A：等 5 分鐘以上，第一次部署有時較慢。還是 404 的話：

```bash
gh api "repos/<owner>/<repo>/pages" --jq '.status'
```

看狀態。`built` 表示成功，`errored` 表示失敗，看 actions log：

```bash
gh run list --repo <owner>/<repo>
```

### Q：改了 HTML 但網站沒更新？

A：瀏覽器快取。網址加 `?v=隨便數字` 強制重抓：

```
https://<owner>.github.io/<repo>/?v=2
```

或在無痕視窗開。

### Q：圖片上傳？

A：把圖片放進 repo（建議 `assets/` 資料夾），HTML 用相對路徑引用：

```html
<img src="assets/mom-photo.jpg" alt="媽媽和我">
```

注意：repo 是 public 的，圖片任何人有連結都能看。隱私圖建議走 Vercel + SSO。

### Q：免費版 GitHub Pages 有流量限制嗎？

A：免費版每月 100GB 流量、每月 10 次 build、每個 site 1GB 大小。一般母親節文章遠遠用不到。

---

## 部署完成 checklist

- [ ] HTML 正確顯示（雙擊本地檔案測試）
- [ ] 手機看排版正常（Chrome devtools → 切手機尺寸）
- [ ] `<meta name="robots" content="noindex, nofollow">` 已加
- [ ] `robots.txt` 已加
- [ ] Repo 是 public（GitHub Pages 免費版需要 public）
- [ ] Repo 名稱不會被輕易搜尋到
- [ ] 部署成功（curl 200）
- [ ] 把網址傳給該看的人
