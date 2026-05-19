---
theme: apple-basic
title: 邱庭瑋 - 自我介紹
download: true
lineNumbers: false
layout: none
class: 'h-full flex flex-col justify-between p-16'
---

<div class="text-sm opacity-50 tracking-widest">2026.05</div>

<div>

<div class="text-7xl font-light leading-tight">Self Introduction</div>

<div class="mt-4 w-12 border-t border-gray-400"></div>

<div class="mt-6 text-lg opacity-70">邱庭瑋  ·  Wayne Chiu</div>

</div>

<div></div>

<!--
Slide 01 — 標題卡（🅱️ 不對稱角落定錨）
時長：~10s
-->


---
layout: intro-image
image: /photos/cover-hero.jpg
---

<div class="absolute inset-0 bg-gradient-to-t from-black/80 via-black/40 to-transparent"></div>

<div class="absolute bottom-12 left-12 text-white">

# 邱庭瑋  Wayne Chiu

Frontend Engineer

<div class="mt-4 text-xl opacity-90">
在不斷變化的軟體環境中摸索前行
</div>

</div>

<!--
Slide 02 — 自我介紹
時長：~20s
記得：補上 slogan
-->

---
layout: intro-image
image: /photos/divider-roots.jpg
---

<div class="absolute inset-0 bg-black/50"></div>

<div class="absolute inset-0 flex flex-col justify-center items-center text-white text-center">

# 從企劃、測試、再到前端

## 跨越十年的軌跡

</div>

<!--
Slide 03 — Part 2 章節標題
時長：~15s
-->

---

<IdentityCard
  number="1"
  role="Game Planner"
  period="2014 – 2016"
  company="卡坦科技 + 遊戲怪獸"
  lesson="從玩家視角設計規則"
  bridge="後來在 ViewSonic 的 AI 創新小組,我用同樣的能力快速做出聊天式互動作答系統的 PoC。"
  accent="var(--accent-game)"
/>

<!--
Slide 04 — 身份 1：遊戲企劃
時長：~60s
-->

---

<IdentityCard
  number="2"
  role="QA Engineer"
  period="2016 – 2021"
  company="捷思達數位 · 4 年 7 個月"
  lesson="品質意識 與 系統性思考"
  bridge="後來在 ClassSwift Mac 專案,我主動導入 OpenSpec / SDD,從制度面降低技術債的累積。"
  accent="var(--accent-test)"
/>

<!--
Slide 05 — 身份 2：測試工程師
時長：~75s
-->

---

<IdentityCard
  number="3"
  role="Frontend Engineer"
  period="2021 – 現在"
  company="聯合報 + ViewSonic"
  lesson="把想法落地的能力"
  bridge="最近的個人專案 LARP Nexus,從規則設計、品質把關到上線部署,三個身份終於合流到一個產品上。"
  accent="var(--accent-front)"
/>

<!--
Slide 06 — 身份 3：前端工程師
時長：~60s
-->

---

<JourneyTimeline
  :nodes="[
    { year: '2014', title: '遊戲企劃', subtitle: '玩家視角', accent: 'var(--accent-game)' },
    { year: '2016', title: '測試工程師', subtitle: '品質意識', accent: 'var(--accent-test)' },
    { year: '2021', title: '前端工程師', subtitle: '落地能力', accent: 'var(--accent-front)' },
    { year: '2026', title: '邱庭瑋', accent: 'var(--accent-now)', isCurrent: true }
  ]"
  conclusion="會做產品的前端工程師"
/>

<!--
Slide 07 — 三身份合流
時長：~30s
-->

---
layout: intro-image
image: /photos/divider-craft.jpg
---

<div class="absolute inset-0 bg-black/50"></div>

<div class="absolute inset-0 flex flex-col justify-center items-center text-white text-center">

# 代表作

## Featured Works

<div class="mt-4 opacity-80">── 三個身份合流的證據</div>

</div>

<!--
Slide 08 — Part 3 章節標題
時長：~15s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# ViewSonic 優派國際

## Frontend Developer · 2024.01 – 2026.02 · 2 年 2 個月

<div class="mt-4 text-sm text-gray-500">
TODO: Quiz Generator + ClassSwift 縮圖待補
</div>

### 三個工作軸線：

- **上線產品開發與維護**
  Quiz Generator · ClassSwift (Mac)
- **AI 創新小組：PoC / MVP**
  聊天式互動作答 · 學習歷程追蹤
- **OpenSpec 流程導入**

</div>

<!--
Slide 09 — ViewSonic 概覽
時長：~45s
-->

---

<ProjectAxis
  company="ViewSonic"
  axisLabel="軸線 1 / AI 創新小組"
  heading="我做的："
  :bullets="[
    '聊天式互動作答系統 (PoC → MVP)',
    '學習歷程追蹤 · 學生狀態安全警示',
    '作答回饋報告整合'
  ]"
  footerLabel="關鍵能力："
  footerText="把 LLM / NLP 推論結果做成即時、可用的互動介面。"
/>

<!--
Slide 10 — ViewSonic 軸線 1：AI 創新小組 ⭐
時長：~50s
TODO：可選擇加入 LLM 整合架構圖
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# ViewSonic 軸線 2 / ClassSwift

<div class="mt-4 text-sm text-gray-500">
TODO: ClassSwift Mac 端 UI 截圖待補
</div>

ViewSonic 主力教育產品 · 課堂即時互動

我負責：Electron Mac 端開發與迭代

<hr class="my-6" />

**Stack:**

Electron · TypeScript · Redux · Zod · Axios · husky · Vitest · E2E

</div>

<!--
Slide 11 — ViewSonic 軸線 2：ClassSwift
時長：~40s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# ViewSonic 軸線 3 / OpenSpec

**問題：**
既有專案要怎麼跟 AI 開發工具整合？

<hr class="my-6" />

**我的做法：**
主動導入 OpenSpec
── 為 AI 而生的 Spec-Driven Development

<hr class="my-6" />

**結果：** 團隊建立能應用於 AI 的開發方式,降低技術債、提升程式碼一致性。

</div>

<!--
Slide 12 — ViewSonic 軸線 3：OpenSpec
時長：~40s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# LARP Nexus · 個人專案

<div class="mt-2 text-sm text-blue-600">
github.com/.../larp-nexus  TODO: 替換為真實 URL
</div>

<div class="mt-4 text-sm text-gray-500">
TODO: GM 桌面端 + 玩家手機端雙截圖待補
</div>

即時多人 LARP 劇本管理平台

- GM 桌面端 + 玩家手機端
- 全程 AI 工具開發
  Claude Code (程式) + Stitch (UI)

</div>

<!--
Slide 13 — LARP Nexus 概覽
時長：~45s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# LARP Nexus / 技術核心

### 關鍵功能：

- **多角色即時狀態同步** (Pusher WebSocket)
- **自動揭露引擎**
- **Runtime / Baseline 環境切換**
- **原子化知識庫**

<hr class="my-6" />

**Stack:**

Next.js (App Router · Server Actions) · TypeScript · MongoDB · Tailwind · Pusher

</div>

<!--
Slide 14 — LARP Nexus 技術核心
時長：~55s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# LARP Nexus / AI 開發實踐

### 全程 AI 工具開發：

- **程式面**：Claude Code
- **UI/UX**：Stitch
- **流程**：OpenSpec · 原子化知識庫
- **品質**：Vitest + E2E

<hr class="my-6" />

→ 「人 + AI」協作可以做出完整產品。
&nbsp;&nbsp;&nbsp;我已經驗證過了。

</div>

<!--
Slide 15 — LARP Nexus AI 開發實踐
時長：~50s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# 聯合報 / 軸線 1

## 前端工程師 · 2021.10 – 2023.10

### 跨專案共用元件庫

- NPM 版本控管
- 跨多個專案共用
- 大幅降低重複代碼
- 提升跨專案開發效率

<hr class="my-6" />

→ 我熟悉如何讓一群工程師高效共用程式碼。

</div>

<!--
Slide 16 — 聯合報軸線 1：跨專案共用元件庫
時長：~30s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# 聯合報 / 軸線 2

### 獨立負責多項前端專案：

- **Vite + SPA** — 新聞專題頁面
- **Nuxt + SSR** — 需要 SEO 的場合
- **GTM (Google Tag Manager)** 數據追蹤

<hr class="my-6" />

→ 從 0 到 1 的環境建置、
&nbsp;&nbsp;&nbsp;跨產品 / 設計 / 行銷的協作。

</div>

<!--
Slide 17 — 聯合報軸線 2：新聞專題 + GTM
時長：~30s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto text-center">

# 技能總覽

## Skill Matrix

</div>

<SkillMatrix
  :groups="[
    { level: '主力 / Primary', dots: 3, items: ['TypeScript · React · Vue', 'Vite · Next.js'] },
    { level: '熟悉 / Proficient', dots: 2, items: ['Electron · Redux · Pinia', 'Tailwind · MongoDB · Pusher'] },
    { level: '探索 / Exploring', dots: 1, items: ['Svelte'] }
  ]"
  :footnotes="[
    { label: 'Testing', text: 'Vitest · E2E · Zod' },
    { label: 'Tooling', text: 'husky · NPM publishing' }
  ]"
/>

<!--
Slide 18 — 技能矩陣
時長：~30s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# AI 工具熟練度

### 日常使用：

- **Claude Code**　　　程式開發主力
- **Stitch**　　　　　 UI/UX 設計協作
- **OpenSpec**　　　　 AI-ready 開發流程

<hr class="my-6" />

### 實戰經驗：

- **ViewSonic AI 創新小組** — LLM 介面整合
- **LARP Nexus** — 全程 AI 工具開發
- **ClassSwift** — OpenSpec SDD 導入

</div>

<!--
Slide 19 — AI 工具熟練度
時長：~30s
-->

---
layout: intro-image
image: /photos/divider-horizon.jpg
---

<div class="absolute inset-0 bg-black/50"></div>

<div class="absolute inset-0 flex flex-col justify-center items-center text-white text-center">

# 為什麼是現在

## 為什麼是這裡

<div class="mt-4 opacity-80">What's Next</div>

</div>

<!--
Slide 20 — Part 5 章節標題
時長：~10s
-->

---
layout: center
class: text-center
---

<div class="max-w-3xl mx-auto">

### 2026 年初

ViewSonic Mac team 因公司戰略調整收掉。

<hr class="my-8 mx-auto w-1/3" />

對我來說,這是個正好的時機點

重新思考下一站要做什麼。

</div>

<!--
Slide 21 — 離職背景
時長：~25s
-->

---
layout: center
---

<div class="max-w-4xl mx-auto">

# 我想找的下一站

- 跟得上 AI 浪潮、願意一起進化的團隊
- 能讓我繼續深化「AI + 前端整合」的環境
- 願意接觸更廣的軟體 stack,不限於前端

<hr class="my-6" />

→ 我能帶來的：
&nbsp;&nbsp;&nbsp;做產品的視角 · 品質意識 · AI 開發實踐

</div>

<!--
Slide 22A — 想做的事（通用版）
時長：~50s
注意：Pacston 客製版在 slides.pacston.md
-->

---
layout: intro-image
image: /photos/closing-thanks.jpg
---

<div class="absolute inset-0 bg-black/50"></div>

<div class="absolute inset-0 flex flex-col justify-center items-center text-white text-center">

# Thank you

## 謝謝聆聽

<div class="mt-8 text-lg">
邱庭瑋  Wayne Chiu
</div>

<div class="mt-2 text-sm opacity-80">
📧  TODO: email　·　💼  TODO: linkedin　·　🐙  TODO: github
</div>

<div class="mt-8 text-sm opacity-70">
TODO: QR code for portfolio
</div>

</div>

<!--
Slide 23 — Thank You + 聯絡資訊
時長：~30s
-->

---
hideInToc: true
layout: center
---

# 附錄 / 詳細經歷時間軸

<JourneyTimeline
  :nodes="[
    { year: '2007–2012', title: '成大資源工程學系' },
    { year: '2012–2014', title: '當兵 + 重考研究所' },
    { year: '2014.8–10', title: '卡坦科技 / 遊戲企劃' },
    { year: '2015.2–2016.5', title: '遊戲怪獸 / 遊戲企劃' },
    { year: '2016.7–2021.2', title: '捷思達數位 / 測試工程師' },
    { year: '2021.2–10', title: '資策會前端課程' },
    { year: '2021.10–2023.10', title: '聯合報 / 前端工程師' },
    { year: '2024.1–2026.2', title: 'ViewSonic / Frontend Developer' }
  ]"
/>

<!--
Slide A1 — 詳細工作經歷時間軸（Q&A 備用）
-->

---
hideInToc: true
layout: center
---

<div class="max-w-4xl mx-auto">

# 附錄 / 技術深度範例

## LARP Nexus — 自動揭露引擎

**問題：**
GM 在劇本進行中,需要根據條件
自動向特定角色揭露線索。

<hr class="my-6" />

**我的設計：**

<div class="mt-4 text-sm text-gray-500">
TODO: Mermaid 流程圖 / 狀態機示意
</div>

<hr class="my-6" />

**關鍵技術：**
Server Actions · WebSocket 廣播
狀態同步策略

</div>

<!--
Slide A2 — 技術深度範例（Q&A 備用）
-->

---
hideInToc: true
layout: image-right
image: /photos/appendix-hobby.jpg
---

# 附錄 / 個人興趣

## LARP (Live Action Role-Playing)

這個興趣訓練我：

- **系統思維**　　　(規則設計)
- **使用者同理心**　(玩家體驗)
- **即興反應能力**　(現場狀況)

<hr class="my-6" />

→ 這也是 LARP Nexus 的起點。

<!--
Slide A3 — 個人興趣（Q&A 備用）
-->
