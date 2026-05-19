# 自我介紹簡報 Design Spec

**作者**：邱庭瑋 (Cody Chiu)
**日期**：2026-05-19
**目標應徵**：前端工程師職位（首要目標：Pacston HCI Frontend Engineer）
**簡報長度**：14 分鐘（主簡報 23 張 + 附錄 3 張，Slide 22 有兩個版本可切換）

---

## 1. 設計決策

### 1.1 框架選擇

**Slidev** + 主題 **`@slidev/theme-apple-basic`**

選擇理由：
- Markdown-first 撰寫，整合 PDF 履歷內容效率最高
- Vue 元件可嵌入，需要客製化視覺時不被框架限制
- 一鍵 `slidev export` 產出 PDF，方便面試前寄出
- `apple-basic` 主題：極簡、設計感強、對前端面試官的「設計品味」是直接加分項

### 1.2 敘事策略

**策略 B+：「製作產品的人」主題敘事 + In Medias Res 結構**

核心主題：**「我這 10 年都在做產品，只是換了三個身份。」**

| 三段身份 | 期間 | 學到的事 |
|---|---|---|
| 遊戲企劃 | 2014-2016 | 從玩家視角設計規則 |
| 測試工程師 | 2016-2021（4 年 7 個月） | 品質意識與系統性思考 |
| 前端工程師 | 2021-現在（4 年） | 把想法落地的能力 |

**過去佔總時長 28%、現在的價值佔 72%**，避免線性鋪墊過長的問題。

### 1.3 視覺策略

- **每張投影片至少一個視覺元素**（圖、code、chart、quote、大字）
- **不連續放 3 張以上純文字 bullet list**
- **作品集區塊 50%+ 是截圖**
- 章節分隔頁用旅行照（`divider-*.jpg`）建立視覺呼吸
- 三段身份頁（04-06）採同一模板，建立節奏感
- 配色策略：apple-basic 預設兩色 + 每段落一個 accent 色（避免單調）

### 1.4 彈性設計

- Slide 22「想做的事」做**兩個版本**：通用版（廣投）+ Pacston 客製化版
- 附錄 A2 可做 2-3 個變體（不同技術主題的深度解釋）
- 整份簡報內容通用，可微調投放給其他公司

---

## 2. 完整投影片結構

### 時長配比總表

| Part | Slides | 時長 | 累積 | 佔比 |
|---|---|---|---|---|
| 1 Cold Open | 01-02 | 30s | 0:30 | 4% |
| 2 三段身份 | 03-07 | 4:00 | 4:30 | 28% |
| 3 代表作 | 08-17 | 6:40 | 11:10 | 47% |
| 4 技能總覽 | 18-19 | 1:00 | 12:10 | 7% |
| 5 下一步 | 20-23 | 1:55 | 14:05 | 14% |
| 附錄 | A1-A3 | Q&A 用 | — | — |

**總計：14 分 5 秒**（10-15 分鐘區間中段，留約 1 分鐘 Q&A 銜接）

---

## 3. 投影片詳細設計

### Part 1：Cold Open（2 張 / 30 秒）

#### Slide 01 — 標題卡

```
Self Introduction
自我介紹
2026.05
```

- **功能**：宣告簡報開始，建立 Apple Keynote 開場感
- **視覺**：純文字、大留白、無圖
- **時長**：~10s

#### Slide 02 — 自我介紹

```
[cover-hero.jpg — 旅行照]

邱庭瑋  Cody Chiu
Frontend Engineer

[slogan — 待自填]
```

- **功能**：建立「這是誰」的第一印象
- **視覺**：cover-hero.jpg + 姓名 + 職位 + slogan
- **時長**：~20s
- **TODO**：slogan 由使用者自填，可參考設計階段提供的 7 個候選

---

### Part 2：三段身份回顧（5 張 / 4 分鐘）

#### Slide 03 — 章節標題

```
[divider-roots.jpg 滿版 + 遮罩]

我這 10 年都在做產品
只是換了三個身份
```

- **時長**：~15s

#### Slide 04 — 身份 1：遊戲企劃

```
身份 1 / Game Planner
2014 – 2016 · 卡坦科技 + 遊戲怪獸
──

我學到的事 ─

從玩家視角設計規則

──
→ 後來在 ViewSonic 的 AI 創新小組，
  我用同樣的能力快速做出
  聊天式互動作答系統的 PoC。
```

- **核心訊息**：跨領域 + 玩家視角 = AI 產品 PoC 能力
- **視覺**：三層 hierarchy（標籤 → lesson → bridge）
- **時長**：~60s

#### Slide 05 — 身份 2：測試工程師

```
身份 2 / QA Engineer
2016 – 2021 · 捷思達數位 · 4 年 7 個月
──

我學到的事 ─

品質意識 與 系統性思考

──
→ 後來在 ClassSwift Mac 專案，
  我主動導入 OpenSpec / SDD，
  從制度面降低技術債的累積。
```

- **核心訊息**：4 年 7 個月不是過渡期，是建立品質直覺的關鍵期
- **視覺**：同 Slide 04
- **時長**：~75s（最重要的一張，多 15 秒解釋）

#### Slide 06 — 身份 3：前端工程師

```
身份 3 / Frontend Engineer
2021 – 現在 · 聯合報 + ViewSonic
──

我學到的事 ─

把想法落地的能力

──
→ 最近的個人專案 LARP Nexus，
  從規則設計、品質把關到上線部署，
  三個身份終於合流到一個產品上。
```

- **核心訊息**：終於能親手做產品；預告 Part 3 的 LARP Nexus
- **視覺**：同 Slide 04
- **時長**：~60s

#### Slide 07 — 三身份合流

```
2014  ●━━━━ 遊戲企劃
      │      玩家視角
      │
2016  ●━━━━ 測試工程師
      │      品質意識
      │
2021  ●━━━━ 前端工程師
      │      落地能力
      │
2026  ★━━━━ 邱庭瑋

      ─────────────────
      會做產品的前端工程師
```

- **核心訊息**：三段不是切換，是累積
- **視覺**：Slidev Mermaid / SVG 垂直時間軸，accent 色區分三段
- **時長**：~30s

---

### Part 3：代表作深入（10 張 / 6 分 40 秒）

#### Slide 08 — 章節標題

```
[divider-craft.jpg 滿版 + 遮罩]

代表作
Featured Works

── 三個身份合流的證據
```

- **時長**：~15s

#### Slide 09 — ViewSonic 概覽

```
ViewSonic 優派國際 / Frontend Developer
2024.01 – 2026.02 · 2 年 2 個月
──

[產品縮圖：Quiz Generator + ClassSwift]

三個工作軸線：
●  上線產品開發與維護
    Quiz Generator · ClassSwift (Mac)
●  AI 創新小組：PoC / MVP
    聊天式互動作答 · 學習歷程追蹤
●  OpenSpec 流程導入
```

- **核心訊息**：建立 context、預告三個展開軸線
- **視覺**：產品縮圖（後補，NDA 允許範圍）
- **時長**：~45s

#### Slide 10 — ViewSonic 軸線 1：AI 創新小組 ⭐

```
ViewSonic 軸線 1 / AI 創新小組
──

我做的：

●  聊天式互動作答系統 (PoC → MVP)
●  學習歷程追蹤 · 學生狀態安全警示
●  作答回饋報告整合

──
關鍵能力：
把 LLM / NLP 推論結果
做成即時、可用的互動介面
```

- **核心訊息**：稀缺能力 — 前端整合 AI 推論結果
- **視覺**：可加 LLM → 前端 → 使用者 架構圖（後補）
- **時長**：~50s
- **重要度**：⭐ Pacston JD 最直接命中

#### Slide 11 — ViewSonic 軸線 2：ClassSwift

```
ViewSonic 軸線 2 / ClassSwift
──

[產品截圖：Mac 端 UI]

ViewSonic 主力教育產品 · 課堂即時互動
我負責：Electron Mac 端開發與迭代

──
Stack:
Electron · TypeScript · Redux · Zod
Axios · husky · Vitest · E2E
```

- **核心訊息**：能撐起一個上線中的桌面端產品
- **視覺**：ClassSwift Mac UI 截圖（後補，NDA 允許範圍）
- **時長**：~40s

#### Slide 12 — ViewSonic 軸線 3：OpenSpec

```
ViewSonic 軸線 3 / OpenSpec
──

問題：
既有專案要怎麼跟 AI 開發工具整合？


我的做法：
主動導入 OpenSpec
── 為 AI 而生的 Spec-Driven Development

──
結果：團隊建立能應用於 AI 的開發方式，
      降低技術債、提升程式碼一致性。
```

- **核心訊息**：主動性 + 制度設計能力
- **視覺**：純文字三段式（問題 → 做法 → 結果）
- **時長**：~40s

#### Slide 13 — LARP Nexus 概覽

```
LARP Nexus · 個人專案
github.com/.../larp-nexus
──

[產品截圖 / GIF — GM 桌面端 + 玩家手機端]

即時多人 LARP 劇本管理平台
●  GM 桌面端 + 玩家手機端
●  全程 AI 工具開發
   Claude Code (程式) + Stitch (UI)
```

- **核心訊息**：從零到一獨立打造完整產品
- **視覺**：雙端截圖併排（無 NDA 限制，建議近期準備）
- **時長**：~45s

#### Slide 14 — LARP Nexus 技術核心

```
LARP Nexus / 技術核心
──

關鍵功能：
●  多角色即時狀態同步 (Pusher WebSocket)
●  自動揭露引擎
●  Runtime / Baseline 環境切換
●  原子化知識庫

──
Stack:
Next.js (App Router · Server Actions)
TypeScript · MongoDB · Tailwind · Pusher
```

- **核心訊息**：你自己解了複雜技術問題
- **視覺**：純文字、可選擇加 mini diagram
- **時長**：~55s

#### Slide 15 — LARP Nexus AI 開發實踐

```
LARP Nexus / AI 開發實踐
──

全程 AI 工具開發：

●  程式面：Claude Code
●  UI/UX：Stitch
●  流程：OpenSpec · 原子化知識庫
●  品質：Vitest + E2E

──
→ 「人 + AI」協作可以做出完整產品。
  我已經驗證過了。
```

- **核心訊息**：不只用 AI，是和 AI 一起工作
- **視覺**：四象限工具分配
- **時長**：~50s

#### Slide 16 — 聯合報軸線 1：跨專案共用元件庫

```
聯合報 / 軸線 1
前端工程師 · 2021.10 – 2023.10
──

跨專案共用元件庫

●  NPM 版本控管
●  跨多個專案共用
●  大幅降低重複代碼
●  提升跨專案開發效率

──
→ 我熟悉如何讓一群工程師高效共用程式碼。
```

- **核心訊息**：團隊共用基礎建設能力
- **視覺**：純文字，可選加示意圖
- **時長**：~30s

#### Slide 17 — 聯合報軸線 2：新聞專題 + GTM

```
聯合報 / 軸線 2
──

獨立負責多項前端專案：

●  Vite + SPA — 新聞專題頁面
●  Nuxt + SSR — 需要 SEO 的場合
●  GTM (Google Tag Manager) 數據追蹤

──
→ 從 0 到 1 的環境建置、
  跨產品 / 設計 / 行銷的協作。
```

- **核心訊息**：從零到一的能力 + 跨部門協作
- **視覺**：純文字
- **時長**：~30s

---

### Part 4：技能總覽（2 張 / 1 分鐘）

#### Slide 18 — 技能矩陣

```
技能總覽 / Skill Matrix
──

主力 / Primary
●●●  TypeScript · React · Vue
●●●  Vite · Next.js

熟悉 / Proficient
●●○  Electron · Redux · Pinia
●●○  Tailwind · MongoDB · Pusher

探索 / Exploring
●○○  Svelte

──
Testing: Vitest · E2E · Zod
Tooling: husky · NPM publishing
```

- **核心訊息**：技能分級透明
- **視覺**：點點等級制
- **時長**：~30s

#### Slide 19 — AI 工具熟練度

```
AI 工具熟練度
──

日常使用：
●  Claude Code     程式開發主力
●  Stitch          UI/UX 設計協作
●  OpenSpec       AI-ready 開發流程

──
實戰經驗：
●  ViewSonic AI 創新小組 — LLM 介面整合
●  LARP Nexus — 全程 AI 工具開發
●  ClassSwift — OpenSpec SDD 導入
```

- **核心訊息**：工具熟練度 + 實戰驗證
- **視覺**：兩段式
- **時長**：~30s

---

### Part 5：下一步（4 張 / 1 分 55 秒）

#### Slide 20 — 章節標題

```
[divider-horizon.jpg 滿版 + 遮罩]

為什麼是現在
為什麼是這裡

What's Next
```

- **時長**：~10s

#### Slide 21 — 離職背景

```
2026 年初
ViewSonic Mac team 因公司戰略調整收掉。

──
對我來說，這是個正好的時機點
重新思考下一站要做什麼。
```

- **核心訊息**：裁員一句話帶過，不抱怨、轉成主動契機
- **視覺**：大留白、中央三行字
- **時長**：~25s

#### Slide 22A — 想做的事（通用版）

```
我想找的下一站
──

●  跟得上 AI 浪潮、願意一起進化的團隊

●  能讓我繼續深化「AI + 前端整合」的環境

●  願意接觸更廣的軟體 stack
   不限於前端

──
→ 我能帶來的：
  做產品的視角 · 品質意識 · AI 開發實踐
```

- **時長**：~50s

#### Slide 22B — 想做的事（Pacston 客製化版）

```
為什麼是 Pacston
──

●  AI + LegalTech
   用 AI 賦能專業領域 ─
   正好是我做教育產品兩年來的延續。

●  HCI Frontend 職位
   LLM 推論 → 即時互動介面，
   是我在 ViewSonic 兩年的主軸。

──
我能帶來：
AI 整合經驗 · 元件庫設計 · OpenSpec 流程
```

- **核心訊息**：把整份簡報的價值連回「對方為什麼要錄取你」
- **操作**：22A 和 22B 在 Slidev 用 conditional slides 或兩份 markdown
- **時長**：~50s

#### Slide 23 — Thank You + 聯絡資訊

```
[closing-thanks.jpg + 遮罩]

Thank you
謝謝聆聽

──
邱庭瑋  Cody Chiu

📧  [email]
💼  linkedin.com/in/...
🐙  github.com/...

[QR code for portfolio]
```

- **核心訊息**：感謝 + 拍照記下聯絡方式
- **視覺**：滿版照片 + 中央資訊區 + QR code
- **時長**：~30s
- **TODO**：email、LinkedIn、GitHub URL、QR code 待後補

---

### 附錄（3 張 / Q&A 用）

#### Slide A1 — 詳細工作經歷時間軸

```
附錄 / 詳細經歷時間軸
──

2007 – 2012       成大資源工程學系
2012 – 2014       當兵 + 重考研究所
2014.8 – 10       卡坦科技 / 遊戲企劃
2015.2 – 2016.5   遊戲怪獸 / 遊戲企劃
2016.7 – 2021.2   捷思達數位 / 測試工程師
2021.2 – 2021.10  資策會前端課程
2021.10 – 2023.10 聯合報 / 前端工程師
2024.1 – 2026.2   ViewSonic / Frontend Developer
```

- **用途**：面試官詢問空白期、轉前端動機、測試年資時翻出

#### Slide A2 — 技術深度範例

```
附錄 / 技術深度範例
LARP Nexus — 自動揭露引擎
──

問題：
GM 在劇本進行中，需要根據條件
自動向特定角色揭露線索。


我的設計：
[Mermaid 流程圖 / 狀態機 — 後補]

──
關鍵技術：
Server Actions · WebSocket 廣播
狀態同步策略
```

- **用途**：面試官追問技術深度時翻出
- **建議**：可做 2-3 個變體（自動揭露引擎、Runtime/Baseline、原子化知識庫）

#### Slide A3 — 個人興趣 (LARP)

```
附錄 / 個人興趣
──

[appendix-hobby.jpg]

LARP (Live Action Role-Playing)

這個興趣訓練我：
●  系統思維         (規則設計)
●  使用者同理心     (玩家體驗)
●  即興反應能力     (現場狀況)

──
→ 這也是 LARP Nexus 的起點。
```

- **用途**：面試官想了解「你是怎樣的人」時翻出

---

## 4. 視覺素材清單

### 已備齊的照片

```
g:\codingdata\self-introduce\assets\photos\
  ├─ cover-hero.jpg           Slide 02 自介
  ├─ divider-roots.jpg        Slide 03 章節標題
  ├─ divider-craft.jpg        Slide 08 章節標題
  ├─ divider-horizon.jpg      Slide 20 章節標題
  ├─ appendix-hobby.jpg       Slide A3 個人興趣
  └─ closing-thanks.jpg       Slide 23 Thank You
```

### 待補的素材

| Slide | 素材 | 取得方式 | 優先級 |
|---|---|---|---|
| 02 | slogan 文字 | 使用者自填 | **必要** |
| 09 | Quiz Generator / ClassSwift 縮圖 | NDA 範圍內 | 中 |
| 10 | LLM 整合架構圖 **或** 聊天介面截圖 | Mermaid / NDA 截圖 | **高** |
| 11 | ClassSwift Mac 端 UI 截圖 | NDA 範圍內 | **高** |
| 13 | LARP Nexus 雙端截圖 | 個人專案、無限制 | **高** |
| 14 | 自動揭露引擎 mini diagram | Mermaid 自繪 | 低 |
| 16 | 元件庫使用示意圖 | Mermaid 自繪 | 低 |
| 23 | email / LinkedIn / GitHub URL / portfolio QR | 使用者提供 | **必要** |
| A2 | 技術深度流程圖 | Mermaid 自繪 | 中 |

---

## 5. 技術 Scaffold（待 implementation plan）

### 預期專案結構

```
g:\codingdata\self-introduce\
  ├─ slides.md                  主簡報 (Slidev 入口)
  ├─ slides.pacston.md          Pacston 客製版 (Slide 22B)
  ├─ package.json
  ├─ pnpm-lock.yaml
  ├─ components/                自訂 Vue 元件
  │   ├─ IdentityCard.vue       三段身份模板
  │   ├─ ProjectAxis.vue        代表作軸線模板
  │   ├─ SkillMatrix.vue        技能矩陣
  │   └─ Timeline.vue           時間軸（Slide 07 / A1）
  ├─ assets/
  │   └─ photos/                已存
  ├─ docs/
  │   └─ specs/
  │       └─ 2026-05-19-self-introduce-design.md  (本檔)
  └─ 前端工程師履歷_邱庭瑋.pdf
```

### 預期依賴

- `@slidev/cli`
- `@slidev/theme-apple-basic`
- `@iconify-json/*`（icon 套件）
- 可能需要：`mermaid`（用於圖表）、`@slidev/types`

### Export 流程

```bash
# 開發
pnpm dev

# 匯出 PDF
pnpm export

# 匯出 PPTX（如需要）
pnpm export --format pptx
```

---

## 6. 待使用者最終確認的決策點

1. **Slogan 內容**（Slide 02）
2. **聯絡資訊**（Slide 23 — email / LinkedIn / GitHub / portfolio URL）
3. **是否要在 Slide 10 加架構圖**（或用截圖替代）
4. **是否要做更多 A2 變體**（不同技術主題的深度解釋）
5. **Slidev 主題微調**：是否需要 override apple-basic 的某些樣式（顏色、字體）

---

## 7. 風險與緩解

| 風險 | 緩解 |
|---|---|
| 視覺單調（apple-basic 預設兩色） | 每段落用一個 accent 色 / 旅行照分隔頁 / 作品截圖補色 |
| Part 3 連續 10 張視覺密度過高 | 每張用不同 layout（概覽 / 純文字 / 截圖主 / 技術 spec / 三段式），避免重複 |
| 14 分鐘可能超時 | 預留每段 +/- 10 秒緩衝；附錄不算入主時長 |
| 履歷 PDF 與簡報不同步 | spec 完成後若履歷修改，需同步檢視 |
| 客製化版本管理 | 用兩份 markdown 或 Slidev conditional render |

---

## 附錄：設計過程記錄

### 框架比較（已決定 Slidev）

| 框架 | 評估 |
|---|---|
| Slidev (Vue) ⭐ | 採用 |
| Spectacle (React) | JSX 撰寫慢、預設樣式弱於 Slidev |
| Reveal.js | 樣板需求多 |
| Marp | 客製化能力不足 |

### 敘事策略比較（已決定 B+）

| 策略 | 優點 | 缺點 |
|---|---|---|
| A 時間線 | 清楚 | 鋪墊太長 |
| **B+ 主題敘事 + In Medias Res** ⭐ | 有戲、避免鋪墊 | 每段需設計收束句 |
| C 能力導向 | 對應面試評分 | 故事感弱 |

### 主題比較（已決定 apple-basic）

| 主題 | 評估 |
|---|---|
| apple-basic ⭐ | 採用，極簡、設計感強 |
| the-unnamed | 太個性化，對保守風氣公司有風險 |
| seriph | 文青感較重 |
| geist | 工程師感較重 |
| default | 太安全、無記憶點 |
