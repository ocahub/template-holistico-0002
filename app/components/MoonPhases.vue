<script setup lang="ts">
// As fases da lua: um divisor decorativo (crescente, quarto, cheia, quarto, minguante).
const phases = [
  'M12 3a9 9 0 1 0 0 18a6 9 0 1 1 0-18Z',
  'M12 3a9 9 0 1 0 0 18Z',
  null,
  'M12 3a9 9 0 1 1 0 18Z',
  'M12 3a9 9 0 1 1 0 18a6 9 0 1 0 0-18Z'
]
</script>

<template>
  <div class="t-moons" aria-hidden="true">
    <svg v-for="(d, i) in phases" :key="i" viewBox="0 0 24 24">
      <circle cx="12" cy="12" r="9" :fill="d ? 'none' : 'currentColor'" stroke="currentColor" stroke-width="1.2" />
      <path v-if="d" :d="d" fill="currentColor" />
    </svg>
  </div>
</template>
