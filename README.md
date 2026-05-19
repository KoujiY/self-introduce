# 自我介紹簡報

邱庭瑋 (Wayne Chiu) 的面試自介簡報，使用 [Slidev](https://sli.dev/) + apple-basic 主題。

- **主簡報**: 21 張 (`slides.md`)
- **附錄** (Q&A 備用): 3 張
- **長度**: 約 14 分鐘

## 🌐 線上瀏覽

部署完成後，可在以下網址瀏覽：

<https://koujiy.github.io/self-introduce/>

## 🛠 本地開發

```bash
pnpm install
pnpm dev               # 啟動 dev server，自動開瀏覽器到 localhost:3030
```

## 📄 匯出 PDF

首次匯出需先安裝 chromium：

```bash
pnpm exec playwright install chromium
```

然後：

```bash
pnpm export            # 匯出 → slides-export.pdf
```

## 🚀 部署到 GitHub Pages

### 自動部署（推薦）

repo 已包含 [`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml)。
每次 push 到 `main` branch,workflow 會自動 build 並部署。

**首次部署設定（只需做一次）**：

1. 在 GitHub 建立新 repo `self-introduce`，把本地專案 push 上去
   ```bash
   git remote add origin https://github.com/KoujiY/self-introduce.git
   git push -u origin main
   ```
2. 進入 repo 的 **Settings → Pages**
3. **Source** 選擇 **GitHub Actions**
4. push 一次到 `main` branch,workflow 會自動執行
5. 完成後在 <https://koujiy.github.io/self-introduce/> 即可瀏覽

workflow 會用 `github.event.repository.name` 自動帶入 base path，不需手動改任何東西。

### 手動 build

如果想手動 build 並自己 deploy（例如部署到別處）：

```bash
pnpm slidev build --base /<your-base-path>/
# 輸出在 dist/
```

## 🧱 投影片結構

| Part | Slides | 內容 |
|---|---|---|
| 1 Cold Open | 01-02 | 標題卡 + 自我介紹 |
| 2 三段身份 | 03-06 | 遊戲企劃 → 測試 → 前端的職涯線 |
| 3 作品集 | 07-17 | ViewSonic / LARP Nexus / 聯合報 三個專案 |
| 4 下一步 | 18-21 | 離職背景 + 想做的事 + Thank You |
| 附錄 | A1-A3 | 詳細經歷時間軸 / 技術範例 / 個人興趣 |

## 🧩 自訂元件

- [`components/IdentityCard.vue`](./components/IdentityCard.vue) — 三段身份模板 (Slides 04-06)
- [`components/ProductThumb.vue`](./components/ProductThumb.vue) — 產品縮圖 + 點圖看原圖 (Slide 08 ViewSonic 概覽)
- [`components/ProjectAxis.vue`](./components/ProjectAxis.vue) — 作品集軸線模板 (Slides 09-11, 13-14, 16-17)

`ProductThumb` 與 `ProjectAxis` 都支援 `fallback` / `imageFallback` prop:當 `:src` 載入 404 時，會由 `@error` + `onMounted` 雙保險換成 fallback 圖。Slide 08 / 09 的 `mvp-chat.png` 就是用這個機制 —— 原圖因 NDA 不上 git，在 GitHub Pages 上會自動降級顯示 `mvp-chat-mock.svg`。

## 📚 文件

- [`CLAUDE.md`](./CLAUDE.md) — 給 AI agents 的專案指引與 gotchas

### 歷史紀錄（已封存）

設計階段的 spec / plan 已收斂為實作，封存於 [`docs/archive/`](./docs/archive/):

- [Design Spec](./docs/archive/2026-05-19-self-introduce-design.md)
- [Implementation Plan](./docs/archive/2026-05-19-self-introduce-implementation.md)

> 內容可能與目前實作有出入，僅供回溯。
