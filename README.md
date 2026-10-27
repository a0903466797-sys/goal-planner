# 目標理財規劃器

用 FV（終值）、PV（現值）、PMT（每期存款）依理財目標試算所需存款，並提供調整建議的純靜態網站。無需建置，所有計算都在瀏覽器內完成。

## 專案結構

```
goal-planner/
├── public/
│   ├── index.html      # 網站本體（HTML + CSS + JS 單一檔案）
│   └── _headers        # Cloudflare 安全標頭
├── wrangler.jsonc      # Cloudflare Workers 靜態資源設定（選用）
├── .gitignore
└── README.md
```

## 本機預覽

```bash
npx serve public
```

或直接用瀏覽器開啟 `public/index.html`。

## 上傳到 GitHub

```bash
cd goal-planner
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/<你的帳號>/goal-planner.git
git push -u origin main
```

## 部署到 Cloudflare Pages（連接 GitHub）

1. Cloudflare 後台 → Workers & Pages → Create → Pages → Connect to Git
2. 選擇 `goal-planner` 儲存庫
3. 設定：
   - Framework preset：None
   - Build command：留空
   - Build output directory：`public`
4. Save and Deploy，完成後會得到 `*.pages.dev` 網址
5. 之後每次 push 到 `main` 都會自動重新部署

## 改用 Wrangler 部署（選用）

```bash
npx wrangler deploy
```

## 公式

月利率 `r = 年化報酬率 / 12`，期數 `n = 年數 × 12`

- `FV = PV·(1+r)^n + PMT·((1+r)^n − 1) / r`
- `PMT = (FV − PV·(1+r)^n)·r / ((1+r)^n − 1)`
- 目標金額依通膨換算：`FV = 今日金額 × (1+通膨率)^年數`

存款假設在每月月底投入。

## 免責聲明

本工具僅供試算參考，報酬率為假設值而非保證，不構成投資建議。
