# Project: 自我介紹簡報

邱庭瑋的面試自介簡報。Slidev + apple-basic 主題，主簡報 21 張 + 附錄 3 張。詳細結構見 [README.md](./README.md)。

## Workflow

### Don't auto-commit

改完 code、回報狀態，然後**停下來**。除非使用者明確說 "OK / commit it / 看起來不錯 / 通過" 之類，**不要自己跑 `git commit`**。

**Why:** 使用者要對 git history 有控制權。Auto-commit 等於把沒驗證、可能有 bug 的改動烤進 log，事後要 revert 反而更亂。使用者習慣先 visually verify(開 dev server、看投影片)，通過了才 commit。**不管我自己多有把握，驗證是使用者的事，不是我的。**

**How to apply:**
- Edit / Write 改完專案檔之後，**最後一個動作是 status report，不是 `git add`**。
- 不要 chain `git add` + `git commit`。
- 收到明確 confirm 才推進到 commit 階段。

## Gotchas

### `mvp-chat.png` 因 NDA 不上 git

- 原圖 `public/images/mvp-chat.png` 是離職前內部 Figma 截圖，在 `.gitignore` 裡(請保持這樣)
- 替代圖 `public/images/mvp-chat-mock.svg` 是公開安全的 mock，有上 git
- Slide 08 / 09 在本地會顯示真圖;**GitHub Pages 上沒有真圖，瀏覽器 404 後 runtime 切到 SVG**
- 切換邏輯在 `components/ProductThumb.vue` 和 `components/ProjectAxis.vue` —— `@error` Vue 事件 + `onMounted` 內 `img.onerror = applyFallback` 雙保險

### 千萬不要在 markdown 寫 `<img src="/path">` 指向可能不存在的檔

Slidev 把 markdown 編成 Vue。Vue compiler 的 `transformAssetUrls` 會把**靜態** `<img src="/path">` 轉成 `import _imports from '/path'`。檔案不在 disk 時，Vite import-analysis **直接讓 dev server / build 崩潰**，沒有機會跑到 runtime fallback。

**正確做法:** 用元件 prop 傳路徑，元件內部用 `:src="image"` 動態 binding。String prop 不會觸發 asset transform。

```vue
<!-- 錯誤:Vite 會炸 -->
<img src="/images/mvp-chat.png" />

<!-- 正確:string prop，Vite 不參與 -->
<ProductThumb src="/images/mvp-chat.png" fallback="/images/mvp-chat-mock.svg" />
```

### Component prop 傳 asset 路徑時要手動套 `BASE_URL`

上一條的副作用:既然 prop 字串 Vite 完全不碰，**build `--base /self-introduce/` 的 base path 也不會自動套到 prop 上**。Dev 一切正常(`BASE_URL = "/"`)，deploy 到 GitHub Pages 就 404，因為 `/images/foo.png` 走到 `https://koujiy.github.io/images/foo.png`(少了 `/self-introduce/`)。

**正確做法:** 元件內部用 `import.meta.env.BASE_URL` 前綴，Vite build 時會把這個常數替換成實際 base path。

```ts
function withBase(path: string): string {
  if (/^https?:\/\//i.test(path)) return path
  return `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`
}
```

`ProductThumb` / `ProjectAxis` 已經這樣處理。新元件若也吃 asset 路徑 prop，記得照做。

## 歷史紀錄

設計階段的 spec / plan 已封存在 [docs/archive/](./docs/archive/)。實作已收斂，內容可能與目前不符，僅供回溯。
