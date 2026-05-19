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
