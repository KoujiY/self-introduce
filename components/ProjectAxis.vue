<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'

const props = defineProps<{
  company: string
  axisLabel: string
  heading?: string
  bullets: string[]
  footerLabel?: string
  footerText?: string
  footerBullets?: string[]
  image?: string
  imageFallback?: string
  imageCaption?: string
}>()

// Slidev's markdown <img src="..."> gets rewritten with the build --base
// prefix automatically, but component-prop strings don't. Resolve them
// ourselves so /images/foo.png becomes /self-introduce/images/foo.png on
// GitHub Pages (and stays /images/foo.png in dev).
function withBase(path: string): string {
  if (/^https?:\/\//i.test(path)) return path
  return `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`
}

const resolvedImage = computed(() =>
  props.image ? withBase(props.image) : undefined,
)
const resolvedFallback = computed(() =>
  props.imageFallback ? withBase(props.imageFallback) : undefined,
)

const imgRef = ref<HTMLImageElement>()

function applyFallback() {
  const img = imgRef.value
  const fb = resolvedFallback.value
  if (!img || !fb) return
  if (img.src.endsWith(fb)) return
  img.src = fb
  const link = img.closest('a')
  if (link) link.href = fb
}

onMounted(() => {
  const img = imgRef.value
  if (!img || !resolvedFallback.value) return

  if (img.complete && img.naturalWidth === 0) {
    applyFallback()
    return
  }

  img.onerror = applyFallback
})
</script>

<template>
  <div class="project-axis" :class="{ 'with-image': resolvedImage }">
    <div class="header">
      <span class="company">{{ company }}</span>
      <span class="axis-label">{{ axisLabel }}</span>
    </div>
    <hr class="section-divider" />

    <div class="body">
      <a
        v-if="resolvedImage"
        :href="resolvedImage"
        target="_blank"
        class="image-block image-link"
      >
        <img
          ref="imgRef"
          :src="resolvedImage"
          :alt="imageCaption || axisLabel"
          @error="applyFallback"
        />
        <div v-if="imageCaption" class="image-caption">{{ imageCaption }} · 點圖看原圖</div>
      </a>

      <div class="content">
        <div v-if="heading" class="heading">{{ heading }}</div>
        <ul class="bullets">
          <li v-for="(b, idx) in bullets" :key="idx">{{ b }}</li>
        </ul>

        <template v-if="footerLabel || footerText || footerBullets">
          <hr class="section-divider" />
          <div v-if="footerLabel" class="footer-label">{{ footerLabel }}</div>
          <ul v-if="footerBullets" class="footer-bullets">
            <li v-for="(b, idx) in footerBullets" :key="idx">{{ b }}</li>
          </ul>
          <div v-else-if="footerText" class="footer-text">{{ footerText }}</div>
        </template>
      </div>
    </div>
  </div>
</template>

<style scoped>
.project-axis {
  padding: 2rem 3rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 1100px;
  margin: 0 auto;
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

/* Body layout */
.body {
  display: flex;
  flex-direction: column;
}

.project-axis.with-image .body {
  flex-direction: row;
  gap: 2.5rem;
  align-items: center;
}

.content {
  flex: 1;
}

/* Image block (also the <a> tag — wraps img + caption) */
.image-block {
  text-align: center;
  flex-shrink: 0;
  display: inline-block;
  cursor: zoom-in;
  transition: opacity 0.2s;
  text-decoration: none;
  color: inherit;
}

.image-block:hover {
  opacity: 0.85;
}

.project-axis.with-image .image-block {
  flex: 0 0 auto;
  max-width: 420px;
}

.image-block img {
  max-height: 300px;
  max-width: 100%;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  display: block;
}

.image-caption {
  font-size: 0.75em;
  color: #64748b;
  margin-top: 0.5rem;
}

/* Content text styles */
.heading {
  font-size: 0.95em;
  color: #475569;
  margin: 0 0 0.5rem;
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

.footer-bullets {
  list-style: none;
  padding: 0;
  margin: 0.5rem 0 0;
}

.footer-bullets li {
  position: relative;
  padding-left: 1.5rem;
  line-height: 1.8;
  font-size: 1em;
}

.footer-bullets li::before {
  content: "●";
  position: absolute;
  left: 0;
  color: #1e293b;
}
</style>
