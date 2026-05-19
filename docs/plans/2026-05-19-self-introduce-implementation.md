# 自我介紹簡報 Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 建置一個 14 分鐘的 Slidev 簡報專案，含 23 張主簡報 + 3 張附錄，用於前端工程師面試自介，可一鍵匯出 PDF。

**Architecture:** Slidev (Vue 3) + apple-basic 主題；單一 `slides.md` 為主入口，搭配 4 個自訂 Vue 元件處理重複版型（IdentityCard、ProjectAxis、JourneyTimeline、SkillMatrix）。Slide 22 用兩個變體（22A 通用 / 22B Pacston）支援多公司彈性使用。

**Tech Stack:** Slidev · @slidev/theme-apple-basic · Vue 3 · TypeScript · Tailwind（內建）· UnoCSS（內建）

**Spec 來源:** [docs/specs/2026-05-19-self-introduce-design.md](../specs/2026-05-19-self-introduce-design.md)

---

## File Structure

### 將會建立的檔案

| 路徑 | 用途 |
|---|---|
| `package.json` | 專案設定、Slidev 依賴 |
| `.gitignore` | 排除 node_modules、dist、.slidev |
| `slides.md` | 主簡報入口（23 張主簡報 + 3 張附錄，使用 22A 通用版） |
| `slides.pacston.md` | Pacston 客製版（22A 換成 22B） |
| `components/IdentityCard.vue` | Slide 04-06 三段身份模板 |
| `components/ProjectAxis.vue` | ViewSonic / 聯合報軸線投影片模板 |
| `components/JourneyTimeline.vue` | Slide 07 三身份合流圖、Slide A1 詳細時間軸 |
| `components/SkillMatrix.vue` | Slide 18 技能矩陣 |
| `style.css` | 自訂全域樣式（accent 色、Slidev 自動載入） |

### 既有的檔案（不會修改）

- `前端工程師履歷_邱庭瑋.pdf` — 履歷來源
- `assets/photos/*.jpg` — 6 張旅行照已備齊
- `docs/specs/2026-05-19-self-introduce-design.md` — Design spec

---

## 設計原則

1. **內容驅動的元件化**：每個重複的版型抽成 Vue 元件，slides.md 只放資料（props）
2. **單一 `slides.md` 入口**：所有投影片在同一個檔案，用 `---` 分隔。Pacston 版另存一份僅換 Slide 22
3. **視覺驗證為主**：每個 task 完成後在 dev server 開瀏覽器確認，不寫單元測試（YAGNI — 簡報無業務邏輯）
4. **段落級 commit**：以 Phase 為 commit 邊界，每完成一個 Phase 統一 commit 一次（見下方 Commit 策略）

## Commit 策略

每個 **Phase** 完成後 commit 一次，而非每個 Task 都 commit。這樣 git history 對應到簡報的結構單位（scaffold / 元件 / 主簡報 / 雙版本 / 附錄），閱讀 history 比逐 task 更有意義。

| Phase | 包含 Tasks | Commit 訊息 |
|---|---|---|
| 1 Scaffold | Task 1-2 | `chore: scaffold Slidev project with apple-basic theme` + `feat: add global accent colors and shared styles`（已執行，保留兩個 commit） |
| 2 元件 | Task 3-6 | `feat: add reusable Vue components for slides` |
| 3 主簡報內容 | Task 7-11 | `feat: implement main presentation content (Cold Open through Skills)` |
| 4 下一步 + 雙版本 | Task 12-13 | `feat: add next-step section and Pacston-customized variant` |
| 5 附錄 + Polish | Task 14-16 | `feat: add appendix slides, PDF export config, and README` |

**Task 內步驟保留**（不變動 task 的拆解粒度），只是 commit 動作合併到 Phase 結束時統一執行。各 task 內若仍寫有「Commit」步驟，視為「Phase 結束的 commit」的一部分。

---

## Phase 1：專案 Scaffold（Task 1-2）

### Task 1：初始化 Slidev 專案

**Files:**
- Create: `package.json`
- Create: `.gitignore`
- Create: `slides.md`（先放佔位內容）

- [ ] **Step 1：建立 `package.json`**

```json
{
  "name": "self-introduce",
  "type": "module",
  "private": true,
  "scripts": {
    "dev": "slidev --open",
    "dev:pacston": "slidev slides.pacston.md --open",
    "build": "slidev build",
    "export": "slidev export",
    "export:pacston": "slidev export slides.pacston.md"
  },
  "dependencies": {
    "@slidev/cli": "^0.49.0",
    "@slidev/theme-apple-basic": "latest",
    "vue": "^3.4.0"
  },
  "devDependencies": {
    "@slidev/types": "^0.49.0",
    "playwright-chromium": "^1.40.0"
  }
}
```

- [ ] **Step 2：建立 `.gitignore`**

```
node_modules/
dist/
.slidev/
*.local
.DS_Store
Thumbs.db
```

- [ ] **Step 3：建立最簡 `slides.md`（驗證能跑）**

```markdown
---
theme: apple-basic
title: 邱庭瑋 - 自我介紹
download: true
lineNumbers: false
---

# Self Introduction

自我介紹

2026.05

---

# Hello World

驗證能跑
```

- [ ] **Step 4：安裝依賴**

Run: `pnpm install`
Expected: 套件安裝成功、無 error

- [ ] **Step 5：啟動 dev server 驗證**

Run: `pnpm dev`
Expected: 自動開啟瀏覽器 `http://localhost:3030`，看到兩張簡單的投影片
按 `Ctrl+C` 關閉 dev server

- [ ] **Step 6：Commit**

```bash
git init
git add package.json .gitignore slides.md
git commit -m "chore: scaffold Slidev project with apple-basic theme"
```

---

### Task 2：建立全域樣式

Slidev 會自動載入專案根目錄的 `style.css`（標準慣例），所有元件與投影片都能使用其中定義的變數與 class。

**Files:**
- Create: `style.css`（**根目錄**，Slidev 自動載入）

- [ ] **Step 1：建立根目錄 `style.css`**

```css
/* 自訂 accent 色 — 三段身份對應 */
:root {
  --accent-game: #d97706;     /* 暖橘 — 遊戲企劃 */
  --accent-test: #2563eb;     /* 藍 — 測試工程師 */
  --accent-front: #059669;    /* 綠 — 前端工程師 */
  --accent-now: #1e293b;      /* 深灰 — 現在的我 */
}

/* 通用：項目分隔線 */
hr.section-divider {
  border: none;
  border-top: 1px solid #cbd5e1;
  margin: 1rem 0;
  width: 60%;
}
```

- [ ] **Step 2：啟動驗證樣式可載入**

Run: `pnpm dev`
Expected: 開啟 DevTools，於 `:root` 元素檢查 `--accent-game` 等 CSS 變數已套用

- [ ] **Step 3：Commit**

```bash
git add style.css
git commit -m "feat: add global accent colors and shared styles"
```

---

## Phase 2：自訂 Vue 元件（Task 3-6）

### Task 3：建立 IdentityCard 元件（給 Slide 04-06 使用）

**Files:**
- Create: `components/IdentityCard.vue`

- [ ] **Step 1：建立元件**

```vue
<!-- components/IdentityCard.vue -->
<script setup lang="ts">
defineProps<{
  number: string
  role: string
  period: string
  company: string
  lesson: string
  bridge: string
  accent?: string  // CSS color, defaults to var(--accent-now)
}>()
</script>

<template>
  <div class="identity-card" :style="{ '--card-accent': accent || 'var(--accent-now)' }">
    <div class="header">
      <span class="number">身份 {{ number }} / {{ role }}</span>
    </div>
    <div class="meta">{{ period }} · {{ company }}</div>
    <hr class="section-divider" />

    <div class="lesson-block">
      <div class="lesson-label">我學到的事 ─</div>
      <div class="lesson-emphasis" :style="{ color: 'var(--card-accent)' }">
        {{ lesson }}
      </div>
    </div>

    <hr class="section-divider" />
    <div class="bridge">→ {{ bridge }}</div>
  </div>
</template>

<style scoped>
.identity-card {
  display: flex;
  flex-direction: column;
  padding: 2rem 3rem;
  height: 100%;
}

.header {
  font-size: 0.95em;
  letter-spacing: 0.05em;
  color: #1e293b;
}

.meta {
  font-size: 0.85em;
  color: #64748b;
  margin-top: 0.25rem;
}

.lesson-block {
  margin: 2rem 0;
  text-align: center;
}

.lesson-label {
  font-size: 1em;
  color: #475569;
  margin-bottom: 1rem;
}
</style>
```

- [ ] **Step 2：在 `slides.md` 末尾加一張暫時測試頁**

```markdown
---

<IdentityCard
  number="1"
  role="Game Planner"
  period="2014 – 2016"
  company="卡坦科技 + 遊戲怪獸"
  lesson="從玩家視角設計規則"
  bridge="後來在 ViewSonic 的 AI 創新小組，我用同樣的能力快速做出聊天式互動作答系統的 PoC。"
  accent="var(--accent-game)"
/>
```

- [ ] **Step 3：啟動驗證視覺**

Run: `pnpm dev`
Expected:
- 看到測試頁渲染
- 「從玩家視角設計規則」用暖橘色顯示
- 三層結構：標籤 / 大字 lesson / 橋接句
- 整體置中、留白合理

- [ ] **Step 4：Commit**

```bash
git add components/IdentityCard.vue slides.md
git commit -m "feat: add IdentityCard component for three-identity slides"
```

---

### Task 4：建立 JourneyTimeline 元件（給 Slide 07 與 A1 使用）

**Files:**
- Create: `components/JourneyTimeline.vue`

- [ ] **Step 1：建立元件**

```vue
<!-- components/JourneyTimeline.vue -->
<script setup lang="ts">
interface TimelineNode {
  year: string
  title: string
  subtitle?: string
  accent?: string
  isCurrent?: boolean
}

defineProps<{
  nodes: TimelineNode[]
  conclusion?: string
}>()
</script>

<template>
  <div class="timeline">
    <div
      v-for="(node, idx) in nodes"
      :key="idx"
      class="node"
      :class="{ current: node.isCurrent }"
    >
      <div class="dot" :style="{ background: node.accent || 'var(--accent-now)' }">
        <span v-if="node.isCurrent">★</span>
      </div>
      <div class="line" v-if="idx < nodes.length - 1"></div>
      <div class="content">
        <div class="year">{{ node.year }}</div>
        <div class="title">{{ node.title }}</div>
        <div v-if="node.subtitle" class="subtitle">{{ node.subtitle }}</div>
      </div>
    </div>
    <div v-if="conclusion" class="conclusion">
      <hr class="section-divider" />
      <div class="conclusion-text">{{ conclusion }}</div>
    </div>
  </div>
</template>

<style scoped>
.timeline {
  padding: 1rem 4rem;
}

.node {
  display: grid;
  grid-template-columns: 60px 1fr;
  grid-template-rows: auto auto;
  align-items: start;
  position: relative;
}

.dot {
  width: 16px;
  height: 16px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 12px;
  margin: 4px 0 0 22px;
  grid-row: 1 / 2;
}

.node.current .dot {
  width: 24px;
  height: 24px;
  margin-left: 18px;
}

.line {
  width: 2px;
  background: #cbd5e1;
  margin-left: 29px;
  height: 2.5rem;
  grid-column: 1 / 2;
  grid-row: 2 / 3;
}

.content {
  grid-column: 2 / 3;
  grid-row: 1 / 2;
  padding-bottom: 1.5rem;
}

.year {
  font-size: 0.85em;
  color: #64748b;
}

.title {
  font-size: 1.1em;
  font-weight: 500;
  color: #1e293b;
}

.subtitle {
  font-size: 0.85em;
  color: #94a3b8;
}

.conclusion {
  margin-top: 1.5rem;
  text-align: center;
}

.conclusion-text {
  font-size: 1.3em;
  font-weight: 500;
  color: #1e293b;
  margin-top: 0.5rem;
}
</style>
```

- [ ] **Step 2：替換測試頁為 timeline 測試**

把 `slides.md` 末尾的 IdentityCard 測試換成：

```markdown
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
```

- [ ] **Step 3：啟動驗證**

Run: `pnpm dev`
Expected:
- 看到垂直時間軸，四個節點
- 三段身份用三種顏色
- 「邱庭瑋」節點較大、帶 ★
- 底部結論「會做產品的前端工程師」

- [ ] **Step 4：Commit**

```bash
git add components/JourneyTimeline.vue slides.md
git commit -m "feat: add JourneyTimeline component"
```

---

### Task 5：建立 ProjectAxis 元件（給 ViewSonic 與聯合報軸線投影片用）

**Files:**
- Create: `components/ProjectAxis.vue`

- [ ] **Step 1：建立元件**

```vue
<!-- components/ProjectAxis.vue -->
<script setup lang="ts">
defineProps<{
  company: string          // e.g. "ViewSonic"
  axisLabel: string         // e.g. "軸線 1 / AI 創新小組"
  heading?: string          // e.g. "我做的："
  bullets: string[]         // 主要 bullets
  footerLabel?: string      // e.g. "關鍵能力："
  footerText?: string       // e.g. "把 LLM..."
}>()
</script>

<template>
  <div class="project-axis">
    <div class="header">
      <span class="company">{{ company }}</span>
      <span class="axis-label">{{ axisLabel }}</span>
    </div>
    <hr class="section-divider" />

    <div v-if="heading" class="heading">{{ heading }}</div>
    <ul class="bullets">
      <li v-for="(b, idx) in bullets" :key="idx">{{ b }}</li>
    </ul>

    <template v-if="footerLabel || footerText">
      <hr class="section-divider" />
      <div v-if="footerLabel" class="footer-label">{{ footerLabel }}</div>
      <div v-if="footerText" class="footer-text">{{ footerText }}</div>
    </template>
  </div>
</template>

<style scoped>
.project-axis {
  padding: 2rem 3rem;
}

.header {
  display: flex;
  align-items: baseline;
  gap: 1rem;
}

.company {
  font-size: 0.95em;
  font-weight: 500;
}

.axis-label {
  font-size: 0.95em;
  color: #64748b;
}

.heading {
  font-size: 0.95em;
  color: #475569;
  margin: 1rem 0 0.5rem;
}

.bullets {
  list-style: none;
  padding: 0;
  margin: 0;
}

.bullets li {
  position: relative;
  padding-left: 1.5rem;
  line-height: 1.8;
  font-size: 1em;
}

.bullets li::before {
  content: "●";
  position: absolute;
  left: 0;
  color: #1e293b;
}

.footer-label {
  font-size: 0.9em;
  color: #475569;
  margin-top: 0.5rem;
}

.footer-text {
  font-size: 1.1em;
  font-weight: 500;
  line-height: 1.6;
  margin-top: 0.5rem;
}
</style>
```

- [ ] **Step 2：替換測試頁**

```markdown
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
  footerText="把 LLM / NLP 推論結果做成即時、可用的互動介面"
/>
```

- [ ] **Step 3：啟動驗證視覺**

Run: `pnpm dev`
Expected:
- ViewSonic 標題 + 軸線標籤
- 三個 bullet points
- 底部 footer 段落

- [ ] **Step 4：Commit**

```bash
git add components/ProjectAxis.vue slides.md
git commit -m "feat: add ProjectAxis component"
```

---

### Task 6：建立 SkillMatrix 元件（給 Slide 18 使用）

**Files:**
- Create: `components/SkillMatrix.vue`

- [ ] **Step 1：建立元件**

```vue
<!-- components/SkillMatrix.vue -->
<script setup lang="ts">
interface SkillGroup {
  level: string           // "主力 / Primary"
  dots: number            // 3, 2, or 1
  items: string[]         // ["TypeScript · React · Vue", ...]
}

defineProps<{
  groups: SkillGroup[]
  footnotes?: { label: string; text: string }[]
}>()
</script>

<template>
  <div class="skill-matrix">
    <div v-for="(g, idx) in groups" :key="idx" class="group">
      <div class="level">{{ g.level }}</div>
      <div v-for="(items, i) in g.items" :key="i" class="row">
        <span class="dots">
          <span v-for="n in 3" :key="n" :class="{ filled: n <= g.dots }">●</span>
        </span>
        <span class="items">{{ items }}</span>
      </div>
    </div>

    <template v-if="footnotes && footnotes.length">
      <hr class="section-divider" />
      <div v-for="(f, idx) in footnotes" :key="idx" class="footnote">
        <span class="footnote-label">{{ f.label }}:</span>
        <span class="footnote-text">{{ f.text }}</span>
      </div>
    </template>
  </div>
</template>

<style scoped>
.skill-matrix {
  padding: 2rem 3rem;
}

.group {
  margin-bottom: 1.5rem;
}

.level {
  font-size: 0.95em;
  color: #475569;
  margin-bottom: 0.5rem;
}

.row {
  display: flex;
  align-items: baseline;
  gap: 1rem;
  margin-bottom: 0.25rem;
}

.dots {
  font-size: 0.85em;
  letter-spacing: 0.2em;
  color: #cbd5e1;
  min-width: 70px;
}

.dots .filled {
  color: #1e293b;
}

.items {
  font-size: 1em;
}

.footnote {
  font-size: 0.9em;
  color: #475569;
  margin-bottom: 0.25rem;
}

.footnote-label {
  font-weight: 500;
  margin-right: 0.5rem;
}
</style>
```

- [ ] **Step 2：替換測試頁**

```markdown
---

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
```

- [ ] **Step 3：啟動驗證**

Run: `pnpm dev`
Expected:
- 三個分級區塊
- 主力顯示三個實心點，熟悉兩個，探索一個
- 底部兩列 footnotes

- [ ] **Step 4：Commit**

```bash
git add components/SkillMatrix.vue slides.md
git commit -m "feat: add SkillMatrix component"
```

---

## Phase 3：寫主簡報內容（Task 7-11）

### Task 7：寫 Cold Open + Part 2 三段身份（Slides 01-07）

**Files:**
- Modify: `slides.md`（**完全替換**之前的測試內容）

- [ ] **Step 1：完整替換 `slides.md`**

```markdown
---
theme: apple-basic
title: 邱庭瑋 - 自我介紹
download: true
lineNumbers: false
css: unocss
---

# Self Introduction

## 自我介紹

2026.05

<!--
Slide 01 — 標題卡
時長：~10s
-->

---
layout: cover
background: ./assets/photos/cover-hero.jpg
class: text-white
---

# 邱庭瑋  Cody Chiu

Frontend Engineer

<div class="mt-8 text-xl opacity-90">
TODO: slogan 待自填
</div>

<!--
Slide 02 — 自我介紹
時長：~20s
記得：補上 slogan
-->

---
layout: cover
background: ./assets/photos/divider-roots.jpg
class: text-white text-center
---

# 我這 10 年都在做產品

## 只是換了三個身份

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
  bridge="後來在 ViewSonic 的 AI 創新小組，我用同樣的能力快速做出聊天式互動作答系統的 PoC。"
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
  bridge="後來在 ClassSwift Mac 專案，我主動導入 OpenSpec / SDD，從制度面降低技術債的累積。"
  accent="var(--accent-test)"
/>

<!--
Slide 05 — 身份 2：測試工程師
時長：~75s（多 15 秒，這段是最重要的轉折期）
-->

---

<IdentityCard
  number="3"
  role="Frontend Engineer"
  period="2021 – 現在"
  company="聯合報 + ViewSonic"
  lesson="把想法落地的能力"
  bridge="最近的個人專案 LARP Nexus，從規則設計、品質把關到上線部署，三個身份終於合流到一個產品上。"
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
```

- [ ] **Step 2：啟動 dev server，逐張驗證 01-07**

Run: `pnpm dev`

Expected：
- Slide 01：標題卡，純文字
- Slide 02：旅行照背景 + 姓名 + slogan placeholder
- Slide 03：羈絆風景照 + 主標題 + 副標
- Slide 04-06：三張身份頁，accent 色不同（橘 / 藍 / 綠）
- Slide 07：時間軸，四個節點

用 `←` / `→` 切換投影片，每張看一遍

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Cold Open (01-02) and Part 2 three identities (03-07)"
```

---

### Task 8：寫 Part 3a — Slide 08 章節標題 + ViewSonic（09-12）

**Files:**
- Modify: `slides.md`（**附加**到既有內容後面）

- [ ] **Step 1：在 Slide 07 之後加上 Slide 08-12**

把以下內容**附加到 `slides.md` 的最後**（在 Slide 07 之後）：

```markdown

---
layout: cover
background: ./assets/photos/divider-craft.jpg
class: text-white text-center
---

# 代表作

## Featured Works

── 三個身份合流的證據

<!--
Slide 08 — Part 3 章節標題
時長：~15s
-->

---

# ViewSonic 優派國際

## Frontend Developer · 2024.01 – 2026.02 · 2 年 2 個月

---

<div class="mt-4 text-sm text-gray-500">
TODO: Quiz Generator + ClassSwift 縮圖待補
</div>

### 三個工作軸線：

- **上線產品開發與維護**
  Quiz Generator · ClassSwift (Mac)
- **AI 創新小組：PoC / MVP**
  聊天式互動作答 · 學習歷程追蹤
- **OpenSpec 流程導入**

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

# ViewSonic 軸線 2 / ClassSwift

<div class="mt-4 text-sm text-gray-500">
TODO: ClassSwift Mac 端 UI 截圖待補
</div>

---

ViewSonic 主力教育產品 · 課堂即時互動
我負責：Electron Mac 端開發與迭代

---

**Stack:**
Electron · TypeScript · Redux · Zod
Axios · husky · Vitest · E2E

<!--
Slide 11 — ViewSonic 軸線 2：ClassSwift
時長：~40s
-->

---

# ViewSonic 軸線 3 / OpenSpec

---

**問題：**
既有專案要怎麼跟 AI 開發工具整合？

**我的做法：**
主動導入 OpenSpec
── 為 AI 而生的 Spec-Driven Development

---

**結果：** 團隊建立能應用於 AI 的開發方式，降低技術債、提升程式碼一致性。

<!--
Slide 12 — ViewSonic 軸線 3：OpenSpec
時長：~40s
-->
```

- [ ] **Step 2：啟動驗證 Slide 08-12**

Run: `pnpm dev`
Expected：
- Slide 08：羈絆 craft 圖背景 + 「代表作」
- Slide 09：ViewSonic 概覽，三個軸線預告
- Slide 10：軸線 1 用 ProjectAxis 元件渲染
- Slide 11：軸線 2 ClassSwift，stack 條列
- Slide 12：軸線 3 OpenSpec，問題 / 做法 / 結果三段式

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Part 3a ViewSonic slides (08-12)"
```

---

### Task 9：寫 Part 3b — LARP Nexus（Slides 13-15）

**Files:**
- Modify: `slides.md`

- [ ] **Step 1：在 Slide 12 之後加入 13-15**

```markdown

---

# LARP Nexus · 個人專案

<div class="mt-2 text-sm text-blue-600">
github.com/.../larp-nexus  TODO: 替換為真實 URL
</div>

---

<div class="mt-4 text-sm text-gray-500">
TODO: GM 桌面端 + 玩家手機端雙截圖待補
</div>

即時多人 LARP 劇本管理平台
- GM 桌面端 + 玩家手機端
- 全程 AI 工具開發
  Claude Code (程式) + Stitch (UI)

<!--
Slide 13 — LARP Nexus 概覽
時長：~45s
-->

---

# LARP Nexus / 技術核心

---

### 關鍵功能：

- **多角色即時狀態同步** (Pusher WebSocket)
- **自動揭露引擎**
- **Runtime / Baseline 環境切換**
- **原子化知識庫**

---

**Stack:**
Next.js (App Router · Server Actions)
TypeScript · MongoDB · Tailwind · Pusher

<!--
Slide 14 — LARP Nexus 技術核心
時長：~55s
-->

---

# LARP Nexus / AI 開發實踐

---

### 全程 AI 工具開發：

- **程式面**：Claude Code
- **UI/UX**：Stitch
- **流程**：OpenSpec · 原子化知識庫
- **品質**：Vitest + E2E

---

→ 「人 + AI」協作可以做出完整產品。
&nbsp;&nbsp;&nbsp;我已經驗證過了。

<!--
Slide 15 — LARP Nexus AI 開發實踐
時長：~50s
-->
```

- [ ] **Step 2：啟動驗證 13-15**

Run: `pnpm dev`
Expected：
- Slide 13：LARP Nexus 標題 + GitHub link + 雙端截圖 placeholder
- Slide 14：技術核心，四個關鍵功能 + Stack
- Slide 15：AI 開發實踐，四種工具分工 + 結論句

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Part 3b LARP Nexus slides (13-15)"
```

---

### Task 10：寫 Part 3c — 聯合報（Slides 16-17）

**Files:**
- Modify: `slides.md`

- [ ] **Step 1：在 Slide 15 之後加入 16-17**

```markdown

---

# 聯合報 / 軸線 1

## 前端工程師 · 2021.10 – 2023.10

---

### 跨專案共用元件庫

- NPM 版本控管
- 跨多個專案共用
- 大幅降低重複代碼
- 提升跨專案開發效率

---

→ 我熟悉如何讓一群工程師高效共用程式碼。

<!--
Slide 16 — 聯合報軸線 1：跨專案共用元件庫
時長：~30s
-->

---

# 聯合報 / 軸線 2

---

### 獨立負責多項前端專案：

- **Vite + SPA** — 新聞專題頁面
- **Nuxt + SSR** — 需要 SEO 的場合
- **GTM (Google Tag Manager)** 數據追蹤

---

→ 從 0 到 1 的環境建置、
&nbsp;&nbsp;&nbsp;跨產品 / 設計 / 行銷的協作。

<!--
Slide 17 — 聯合報軸線 2：新聞專題 + GTM
時長：~30s
-->
```

- [ ] **Step 2：啟動驗證 16-17**

Run: `pnpm dev`
Expected：
- Slide 16：元件庫四點 + 結論
- Slide 17：三項目 + 結論

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Part 3c United Daily News slides (16-17)"
```

---

### Task 11：寫 Part 4 技能總覽（Slides 18-19）

**Files:**
- Modify: `slides.md`

- [ ] **Step 1：在 Slide 17 之後加入 18-19**

```markdown

---

# 技能總覽

## Skill Matrix

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

# AI 工具熟練度

---

### 日常使用：

- **Claude Code**　　　程式開發主力
- **Stitch**　　　　　 UI/UX 設計協作
- **OpenSpec**　　　　 AI-ready 開發流程

---

### 實戰經驗：

- **ViewSonic AI 創新小組** — LLM 介面整合
- **LARP Nexus** — 全程 AI 工具開發
- **ClassSwift** — OpenSpec SDD 導入

<!--
Slide 19 — AI 工具熟練度
時長：~30s
-->
```

- [ ] **Step 2：啟動驗證 18-19**

Run: `pnpm dev`
Expected：
- Slide 18：三個分級的技能矩陣 + footnotes
- Slide 19：兩段式（日常使用 + 實戰經驗）

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Part 4 skills slides (18-19)"
```

---

## Phase 4：Part 5 下一步 + 雙版本（Task 12-13）

### Task 12：寫 Part 5 下一步（Slides 20-23，通用版 22A）

**Files:**
- Modify: `slides.md`

- [ ] **Step 1：在 Slide 19 之後加入 20-23**

```markdown

---
layout: cover
background: ./assets/photos/divider-horizon.jpg
class: text-white text-center
---

# 為什麼是現在

## 為什麼是這裡

What's Next

<!--
Slide 20 — Part 5 章節標題
時長：~10s
-->

---

<div class="text-center mt-16">

2026 年初
ViewSonic Mac team 因公司戰略調整收掉。

---

對我來說，這是個正好的時機點
重新思考下一站要做什麼。

</div>

<!--
Slide 21 — 離職背景
時長：~25s
-->

---

# 我想找的下一站

---

- 跟得上 AI 浪潮、願意一起進化的團隊
- 能讓我繼續深化「AI + 前端整合」的環境
- 願意接觸更廣的軟體 stack，不限於前端

---

→ 我能帶來的：
&nbsp;&nbsp;&nbsp;做產品的視角 · 品質意識 · AI 開發實踐

<!--
Slide 22A — 想做的事（通用版）
時長：~50s
注意：Pacston 客製版在 slides.pacston.md
-->

---
layout: cover
background: ./assets/photos/closing-thanks.jpg
class: text-white text-center
---

# Thank you

## 謝謝聆聽

---

邱庭瑋  Cody Chiu

📧  TODO: email
💼  TODO: linkedin URL
🐙  TODO: github URL

<div class="mt-8 text-sm">
TODO: QR code for portfolio
</div>

<!--
Slide 23 — Thank You + 聯絡資訊
時長：~30s
-->
```

- [ ] **Step 2：啟動驗證 20-23**

Run: `pnpm dev`
Expected：
- Slide 20：地平線照片背景 + 章節標題
- Slide 21：大留白，三行字置中
- Slide 22：通用版「我想找的下一站」
- Slide 23：感謝頁，聯絡資訊 placeholder

- [ ] **Step 3：Commit**

```bash
git add slides.md
git commit -m "feat: implement Part 5 next-step slides (20-23, general version)"
```

---

### Task 13：建立 Pacston 客製版（slides.pacston.md）

**Files:**
- Create: `slides.pacston.md`

- [ ] **Step 1：複製 `slides.md` 為 `slides.pacston.md`**

Run（PowerShell）:
```powershell
Copy-Item slides.md slides.pacston.md
```

- [ ] **Step 2：替換 `slides.pacston.md` 中 Slide 22A 內容為 22B（Pacston 版）**

找到 `slides.pacston.md` 中 `# 我想找的下一站` 那一張，整張替換為：

```markdown
# 為什麼是 Pacston

---

- **AI + LegalTech**
  用 AI 賦能專業領域 ─
  正好是我做教育產品兩年來的延續。
- **HCI Frontend 職位**
  LLM 推論 → 即時互動介面，
  是我在 ViewSonic 兩年的主軸。

---

**我能帶來：**
AI 整合經驗 · 元件庫設計 · OpenSpec 流程

<!--
Slide 22B — 想做的事（Pacston 客製化版）
時長：~50s
-->
```

- [ ] **Step 3：驗證兩個版本各自可跑**

Run: `pnpm dev`（測試通用版）
Expected：Slide 22 是「我想找的下一站」

按 `Ctrl+C` 關閉，再 Run: `pnpm dev:pacston`
Expected：Slide 22 是「為什麼是 Pacston」

- [ ] **Step 4：Commit**

```bash
git add slides.pacston.md
git commit -m "feat: add Pacston-customized variant of slides"
```

---

## Phase 5：附錄 + Polish（Task 14-16）

### Task 14：寫附錄（Slides A1-A3）

**Files:**
- Modify: `slides.md`（與 `slides.pacston.md` 同步）

- [ ] **Step 1：在 Slide 23 之後加入 A1-A3**

在 `slides.md` 的最後加入（Slide 23 之後）：

```markdown

---
hideInToc: true
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
---

# 附錄 / 技術深度範例

## LARP Nexus — 自動揭露引擎

---

**問題：**
GM 在劇本進行中，需要根據條件
自動向特定角色揭露線索。

**我的設計：**
<div class="mt-4 text-sm text-gray-500">
TODO: Mermaid 流程圖 / 狀態機示意
</div>

---

**關鍵技術：**
Server Actions · WebSocket 廣播
狀態同步策略

<!--
Slide A2 — 技術深度範例（Q&A 備用）
-->

---
hideInToc: true
layout: image-right
image: ./assets/photos/appendix-hobby.jpg
---

# 附錄 / 個人興趣

## LARP (Live Action Role-Playing)

---

這個興趣訓練我：
- **系統思維**　　　(規則設計)
- **使用者同理心**　(玩家體驗)
- **即興反應能力**　(現場狀況)

---

→ 這也是 LARP Nexus 的起點。

<!--
Slide A3 — 個人興趣（Q&A 備用）
-->
```

- [ ] **Step 2：同步附錄到 `slides.pacston.md`**

把同樣三張附錄加到 `slides.pacston.md` 對應位置（Slide 23 之後）

- [ ] **Step 3：啟動驗證附錄**

Run: `pnpm dev`
Expected：
- Slide A1：完整時間軸，8 個節點
- Slide A2：技術深度範例（佔位）
- Slide A3：左文右圖（appendix-hobby.jpg）

- [ ] **Step 4：Commit**

```bash
git add slides.md slides.pacston.md
git commit -m "feat: implement appendix slides (A1-A3) for Q&A reference"
```

---

### Task 15：設定 PDF 匯出 + 驗證

**Files:**
- Modify: `package.json`（如果需要調整 export 設定）

- [ ] **Step 1：安裝 playwright（PDF export 需要）**

Playwright 已在 devDependencies。確認 chromium 已下載：

Run: `pnpm exec playwright install chromium`
Expected: chromium 安裝成功（如果已有則 skip）

- [ ] **Step 2：測試匯出通用版 PDF**

Run: `pnpm export`
Expected:
- 產生 `slides-export.pdf`
- 開啟 PDF 確認 23 張主簡報 + 3 張附錄都在
- 視覺與 dev server 一致（apple-basic 主題、photo 背景、元件樣式）

- [ ] **Step 3：測試匯出 Pacston 版 PDF**

Run: `pnpm export:pacston`
Expected:
- 產生 `slides.pacston-export.pdf`
- Slide 22 顯示 Pacston 客製版

- [ ] **Step 4：將兩個 PDF 加入 .gitignore**

修改 `.gitignore`，加入：

```
*-export.pdf
```

（PDF 是衍生產物，不應進版本控制）

- [ ] **Step 5：Commit**

```bash
git add .gitignore
git commit -m "chore: configure PDF export and ignore generated PDFs"
```

---

### Task 16：最終視覺檢查 + 撰寫 README

**Files:**
- Create: `README.md`

- [ ] **Step 1：完整跑一輪 dev server，逐張檢查**

Run: `pnpm dev`

檢查每張（共 23 主 + 3 附錄）：
- [ ] Slide 01：標題卡，無視覺異常
- [ ] Slide 02：照片背景，姓名 + slogan placeholder（記得後續填）
- [ ] Slide 03：章節標題 + 旅行照
- [ ] Slide 04-06：三身份頁，accent 色不同
- [ ] Slide 07：時間軸顯示正常
- [ ] Slide 08：章節標題 + craft 照
- [ ] Slide 09-12：ViewSonic 四張，layout 一致
- [ ] Slide 13-15：LARP Nexus 三張
- [ ] Slide 16-17：聯合報兩張
- [ ] Slide 18-19：技能矩陣 + AI 工具
- [ ] Slide 20：章節標題 + horizon 照
- [ ] Slide 21：離職背景（大留白）
- [ ] Slide 22：通用版「我想找的下一站」
- [ ] Slide 23：感謝頁 + 照片
- [ ] Slide A1：8 節點時間軸
- [ ] Slide A2：技術深度範例（含 TODO 提醒）
- [ ] Slide A3：左文右圖

- [ ] **Step 2：建立 README.md**

```markdown
# 自我介紹簡報

邱庭瑋 (Cody Chiu) 的面試自介簡報，使用 Slidev + apple-basic 主題。

## 開發

```bash
pnpm install
pnpm dev               # 通用版
pnpm dev:pacston       # Pacston 客製版
```

## 匯出 PDF

```bash
pnpm export            # 匯出通用版
pnpm export:pacston    # 匯出 Pacston 客製版
```

## 文件

- [Design Spec](./docs/specs/2026-05-19-self-introduce-design.md)
- [Implementation Plan](./docs/plans/2026-05-19-self-introduce-implementation.md)

## 待補的內容（TODO）

1. **Slide 02**：個人 slogan
2. **Slide 09**：Quiz Generator / ClassSwift 縮圖
3. **Slide 10**：LLM 整合架構圖 或 聊天介面截圖
4. **Slide 11**：ClassSwift Mac 端 UI 截圖
5. **Slide 13**：LARP Nexus 雙端截圖
6. **Slide 23**：email / LinkedIn / GitHub URL + portfolio QR code
7. **Slide A2**：自動揭露引擎流程圖（Mermaid）
```

- [ ] **Step 3：Commit**

```bash
git add README.md
git commit -m "docs: add README with dev/export instructions and TODO list"
```

---

## Self-Review

### Spec coverage 檢查

✅ Cold Open 兩張（標題 + 自介）→ Task 7
✅ 三段身份回顧五張 → Task 7（含 Slide 07 timeline）
✅ 代表作十張（ViewSonic 4 + LARP Nexus 3 + 聯合報 2 + 章節 1）→ Task 8-10
✅ 技能總覽兩張 → Task 11
✅ 下一步四張（含 22A 通用 + 22B Pacston）→ Task 12-13
✅ 附錄三張 → Task 14
✅ Slidev + apple-basic 主題 → Task 1
✅ 6 張照片整合 → 在各章節分隔頁與 cover 引用
✅ 雙版本（22A / 22B）→ Task 13 拆出 slides.pacston.md
✅ PDF export → Task 15
✅ 自訂元件：IdentityCard / JourneyTimeline / ProjectAxis / SkillMatrix → Task 3-6

### 已知 placeholders（spec 預期保留的 TODO）

這些 TODO 是 spec 設計階段就明確標記為「使用者後補」的內容，**非 plan 失敗**：
- Slogan、聯絡資訊、各種截圖、Mermaid 流程圖

在 plan 中已用 `TODO:` 註解清楚標示位置，並在 README 最後彙整列表。

### Type / 命名一致性

- 元件 props 名稱：IdentityCard 用 `accent`，與 `--accent-game` 等 CSS 變數命名一致
- JourneyTimeline 的 `nodes` 結構：在 Task 4 與 Task 7（Slide 07）、Task 14（Slide A1）使用一致
- `slides.md` 與 `slides.pacston.md` 只在 Slide 22 有差異，其他完全同步

### Scope check

✅ 單一 plan、單一可交付產物（簡報 + PDF 匯出）
✅ 不需拆分（沒有獨立子系統）

---

## Execution Handoff

Plan 完成並存到 `docs/plans/2026-05-19-self-introduce-implementation.md`。

### 兩種執行模式

**1. Subagent-Driven（推薦）**
- 每個 task 派一個全新的 subagent 執行
- 任務間有 review checkpoint
- 適合長期專案、需要多輪確認

**2. Inline Execution**
- 在當前 session 直接執行
- 批次執行 + checkpoint
- 適合快速完成

### 推薦選擇

對於這個專案（單人小規模、需要每張投影片視覺確認），**Inline Execution** 較合適 ── 你可以即時看 dev server 結果決定要不要往下走。

決定後告訴我哪個模式，我啟動對應的執行 sub-skill。
