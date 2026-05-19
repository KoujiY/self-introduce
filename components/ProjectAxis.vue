<script setup lang="ts">
defineProps<{
  company: string
  axisLabel: string
  heading?: string
  bullets: string[]
  footerLabel?: string
  footerText?: string
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
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  max-width: 900px;
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
