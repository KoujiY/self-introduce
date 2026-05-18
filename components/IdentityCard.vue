<script setup lang="ts">
defineProps<{
  number: string
  role: string
  period: string
  company: string
  lesson: string
  bridge: string
  accent?: string
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

.lesson-emphasis {
  font-size: 2.5em;
  font-weight: 600;
  letter-spacing: 0.02em;
  margin: 1rem 0;
}

.bridge {
  font-size: 0.9em;
  color: #64748b;
  line-height: 1.6;
  margin-top: 1rem;
}
</style>
