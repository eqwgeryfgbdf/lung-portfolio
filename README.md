# 龍禹丞的未來資訊履歷（靜態網站方案）

面向初中生：我們用一份 `task.json` 讓電腦自動幫你生成整個網站。大部分頁面是純靜態 HTML（超快），只有需要互動的部分才載入少量 JavaScript（更快）。

## 技術選擇（快且可互動）
- Astro（SSG + Islands）：預設輸出靜態 HTML，互動用「島嶼」逐步啟用。
- Tailwind CSS：快速做出一致風格，方便套用 `theme.color` 和 cute/techy/mystic。
- Preact 或 Alpine.js：小巧互動庫，僅在需要的組件上載入。
- 部署：Cloudflare Pages（或 Netlify/GitHub Pages），全球 CDN，延遲低、免伺服器。

## 資料來源與映射
- 單一來源：根目錄 `task.json`。
- 路由：`pages[*].id` 對應網址，例如 `home → /`、`about → /about`、`resume → /resume`。
- 標題：`pages[*].title` 用於 `<title>` 與頁面主標題。
- 元件：`components[*].type` 對應 Astro 元件（如 `intro-banner`、`quick-nav`、`bio` 等）。
- 主題：`theme.color` 對應 Tailwind 自訂色盤；`theme.style/notes` 控制霓虹、圓角、陰影等變體。

## 頁面與元件（預計）
- `src/pages/index.astro`（home）與 `src/pages/[page].astro`（about/resume/portfolio/blog/contact）。
- 元件清單：
  - `IntroBanner.astro`（intro-banner）
  - `QuickNav.astro`（quick-nav）
  - `Bio.astro`（bio）
  - `Vision.astro`（vision）
  - `Education.astro`（education）
  - `Skills.astro`（skills）
  - `Certificates.astro`（certificates）
  - `Honors.astro`（honors）
  - `ProjectList.astro`（project-list）
  - `BlogList.astro`（blog-list）
  - `ContactInfo.astro`（contact-info）

## 互動與效能
- 僅在需要處載入 JS：快速導覽、展開/收合、滑動動畫等。
- Lazy load 圖片，使用 `loading="lazy"`、`decoding="async"`。
- Purge 未用 CSS、壓縮資源、產生 sitemap 與 meta。

## 專案結構（示意）
/（repo root）
- task.json                    # 內容來源
- src/pages/index.astro        # home
- src/pages/[page].astro       # 其他頁
- src/components/*.astro       # 組件
- public/                      # 圖片資源
- astro.config.mjs, tailwind.config.cjs, package.json

## 建置步驟（指令）
1) 初始化
- npm create astro@latest roylung-site -- --template minimal
- cd roylung-site
- npx astro add tailwind

2) 複製 `task.json` 至專案根目錄，建立路由與元件，從 `task.json` 讀取 pages。

3) 部署到 Cloudflare Pages（或 Netlify）：綁定 GitHub，推送即自動部署。

## 使用方式（非工程背景也能改）
- 只改 `task.json`：新增作品、調整技能等級、換顏色，都能自動更新網站。

## 驗收標準（可量測）
- 首屏可互動時間（TTI）< 2 秒（一般 4G）。
- 首包 JS < 50 KB（不含字型/第三方）。
- `task.json` 變更 1 分鐘內可上線（CI/CD）。
- 關鍵內容在關閉 JS 時仍可讀。

## 相關文件
- 專案規劃：`PLAN.md`
- 前端規範：`frontend-guidelines.md`
- 資產放置：`ASSETS.md`
