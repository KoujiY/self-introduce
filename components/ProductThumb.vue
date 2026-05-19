<script setup lang="ts">
defineProps<{
  src: string
  fallback?: string
  alt: string
  caption: string
}>()

// Same fallback mechanism as ProjectAxis: when <img> 404s, swap src and
// parent <a> href to the fallback URL. dataset.fallbackApplied prevents
// loops if the fallback itself fails.
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
  <a :href="src" target="_blank" class="text-center hover:opacity-80 transition-opacity">
    <img
      :src="src"
      :alt="alt"
      :data-fallback="fallback"
      class="h-28 mx-auto rounded shadow-md cursor-zoom-in"
      @error="handleImageError"
    />
    <div class="text-xs text-gray-500 mt-2">{{ caption }}</div>
  </a>
</template>
