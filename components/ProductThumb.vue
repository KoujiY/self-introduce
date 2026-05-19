<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'

const props = defineProps<{
  src: string
  fallback?: string
  alt: string
  caption: string
}>()

// Slidev's markdown <img src="..."> gets rewritten with the build --base
// prefix automatically, but component-prop strings don't. Resolve them
// ourselves so /images/foo.png becomes /self-introduce/images/foo.png on
// GitHub Pages (and stays /images/foo.png in dev).
function withBase(path: string): string {
  if (/^https?:\/\//i.test(path)) return path
  return `${import.meta.env.BASE_URL}${path.replace(/^\//, '')}`
}

const resolvedSrc = computed(() => withBase(props.src))
const resolvedFallback = computed(() =>
  props.fallback ? withBase(props.fallback) : undefined,
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
  <a :href="resolvedSrc" target="_blank" class="text-center hover:opacity-80 transition-opacity">
    <img
      ref="imgRef"
      :src="resolvedSrc"
      :alt="alt"
      class="h-28 mx-auto rounded shadow-md cursor-zoom-in"
      @error="applyFallback"
    />
    <div class="text-xs text-gray-500 mt-2">{{ caption }}</div>
  </a>
</template>
