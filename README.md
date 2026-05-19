# 自我介紹簡報

邱庭瑋 (Wayne Chiu) 的面試自介簡報,使用 Slidev + apple-basic 主題,14 分鐘長度 (23 主簡報 + 3 附錄)。

## 開發

```bash
pnpm install
pnpm dev               # 通用版 (slides.md)
pnpm dev:pacston       # Pacston 客製版 (slides.pacston.md)
```

## 匯出 PDF

首次匯出需先安裝 chromium:

```bash
pnpm exec playwright install chromium
```

然後:

```bash
pnpm export            # 匯出通用版 → slides-export.pdf
pnpm export:pacston    # 匯出 Pacston 客製版
```

## 投影片結構

| Part | Slides | 時長 |
|---|---|---|
| 1 Cold Open | 01-02 | 30s |
| 2 三段身份 | 03-07 | 4:00 |
| 3 代表作 | 08-17 | 6:40 |
| 4 技能總覽 | 18-19 | 1:00 |
| 5 下一步 | 20-23 | 1:55 |
| 附錄 (Q&A) | A1-A3 | — |

**總計**: 14 分 05 秒

## 自訂元件

- `IdentityCard.vue` — 三段身份模板 (Slides 04-06)
- `JourneyTimeline.vue` — 時間軸 (Slide 07 三身份合流 + Slide A1 詳細經歷)
- `ProjectAxis.vue` — 代表作軸線模板 (Slide 10 等)
- `SkillMatrix.vue` — 技能矩陣 (Slide 18)

## 文件

- [Design Spec](./docs/specs/2026-05-19-self-introduce-design.md)
- [Implementation Plan](./docs/plans/2026-05-19-self-introduce-implementation.md)

## 待補的內容 (TODO)

開始用之前記得補上:

1. **Slide 02** — 個人 slogan
2. **Slide 09** — Quiz Generator / ClassSwift 縮圖
3. **Slide 10** — LLM 整合架構圖 **或** 聊天介面截圖
4. **Slide 11** — ClassSwift Mac 端 UI 截圖
5. **Slide 13** — LARP Nexus 雙端截圖 + 替換 GitHub URL placeholder
6. **Slide 23** — email / LinkedIn / GitHub URL + portfolio QR code
7. **Slide A2** — 自動揭露引擎流程圖 (Mermaid)

## 客製化新公司

要為另一家公司製作客製版:

1. 複製 `slides.md` 為 `slides.<company>.md`
2. 修改 Slide 22 內容對應該公司
3. 加 npm script 到 `package.json`:
   ```json
   "dev:<company>": "slidev slides.<company>.md --open",
   "export:<company>": "slidev export slides.<company>.md"
   ```
