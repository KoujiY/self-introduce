<script setup lang="ts">
interface SkillGroup {
  level: string
  dots: number
  items: string[]
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
