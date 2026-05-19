<script setup lang="ts">
import { onMounted, ref } from 'vue'

const props = defineProps<{
  src: string
  fallback?: string
  alt: string
  caption: string
}>()

const imgRef = ref<HTMLImageElement>()

function applyFallback() {
  const img = imgRef.value
  if (!img || !props.fallback) return
  if (img.src.endsWith(props.fallback)) return
  img.src = props.fallback
  const link = img.closest('a')
  if (link) link.href = props.fallback
}

onMounted(() => {
  const img = imgRef.value
  if (!img || !props.fallback) return

  if (img.complete && img.naturalWidth === 0) {
    applyFallback()
    return
  }

  img.onerror = applyFallback
})
</script>

<template>
  <a :href="src" target="_blank" class="text-center hover:opacity-80 transition-opacity">
    <img
      ref="imgRef"
      :src="src"
      :alt="alt"
      class="h-28 mx-auto rounded shadow-md cursor-zoom-in"
      @error="applyFallback"
    />
    <div class="text-xs text-gray-500 mt-2">{{ caption }}</div>
  </a>
</template>
