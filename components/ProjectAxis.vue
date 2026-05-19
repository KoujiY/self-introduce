<script setup lang="ts">
defineProps<{
  company: string
  axisLabel: string
  heading?: string
  bullets: string[]
  footerLabel?: string
  footerText?: string
  footerBullets?: string[]
  image?: string
  imageCaption?: string
  imageFallback?: string
}>()

// Image fallback handler. Reads the fallback URL from data-fallback so a
// closure isn't needed; uses data-fallback-applied to avoid loops if the
// fallback itself 404s.
function handleImageError(event: Event) {
  const img = event.target as HTMLImageElement
  if (img.dataset.fallbackApplied) return
  const fb = img.dataset.fallback
  if (!fb) return
  img.dataset.fallbackApplied = 'true'
  img.src = fb
  const link = img.closest('a')
  if (link) link.href = fb
}
</script>

<template>
  <div class="project-axis" :class="{ 'with-image': image }">
    <div class="header">
      <span class="company">{{ company }}</span>
      <span class="axis-label">{{ axisLabel }}</span>
    </div>
    <hr class="section-divider" />

    <div class="body">
      <div v-if="image" class="image-block">
        <a :href="image" target="_blank" class="image-link">
          <img
            :src="image"
            :alt="imageCaption || axisLabel"
            :data-fallback="imageFallback"
            @error="handleImageError"
          />
        </a>
        <div v-if="imageCaption" class="image-caption">{{ imageCaption }} · 點圖看原圖</div>
      </div>

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

/* Image block */
.image-block {
  text-align: center;
  flex-shrink: 0;
}

.project-axis.with-image .image-block {
  flex: 0 0 auto;
  max-width: 420px;
}

.image-link {
  display: inline-block;
  cursor: zoom-in;
  transition: opacity 0.2s;
}

.image-link:hover {
  opacity: 0.85;
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
