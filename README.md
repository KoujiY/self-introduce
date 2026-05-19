# 自我介紹簡報

邱庭瑋 (Wayne Chiu) 的面試自介簡報,使用 Slidev + apple-basic 主題。

- **主簡報**：21 張 (`slides.md`)
- **附錄** (Q&A 備用)：3 張
- **長度**：約 14 分鐘

## 開發

```bash
pnpm install
pnpm dev               # 啟動 dev server (自動開瀏覽器)
```

## 匯出 PDF

首次匯出需先安裝 chromium：

```bash
pnpm exec playwright install chromium
```

然後：

```bash
pnpm export            # 匯出 → slides-export.pdf
```

## 投影片結構

| Part | Slides | 內容 |
|---|---|---|
| 1 Cold Open | 01-02 | 標題卡 + 自我介紹 |
| 2 三段身份 | 03-06 | 遊戲企劃 → 測試 → 前端的職涯線 |
| 3 作品集 | 07-17 | ViewSonic / LARP Nexus / 聯合報 三個專案 |
| 4 下一步 | 18-21 | 離職背景 + 想做的事 + Thank You |
| 附錄 | A1-A3 | 詳細經歷時間軸 / 技術範例 / 個人興趣 |

## 自訂元件

- `components/IdentityCard.vue` — 三段身份模板 (Slides 04-06)
- `components/ProjectAxis.vue` — 作品集軸線模板 (Slides 09-11, 13-14, 16-17)

## 文件

- [Design Spec](./docs/specs/2026-05-19-self-introduce-design.md)
- [Implementation Plan](./docs/plans/2026-05-19-self-introduce-implementation.md)

> 註：spec 與 plan 是設計階段的歷史紀錄,可能與目前實作有出入。

## 待補的內容 (TODO)

- **Slide 21 (Thank You)** — 實際的 email / LinkedIn URL / GitHub URL / portfolio QR code
