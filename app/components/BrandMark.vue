<script setup lang="ts">
// A marca: o logo da loja (imagem) ou a lua crescente com o nome e a linha de baixo.
defineProps<{ name: string, tagline?: string, logo?: string, light?: boolean }>()
const maskId = `t-moon-${useId()}`
</script>

<template>
  <span class="t-brand" :class="{ 't-brand--light': light }">
    <img v-if="logo" class="t-brand__img" :src="logo" :alt="name">
    <template v-else>
      <svg class="t-brand__moon" viewBox="0 0 64 64" aria-hidden="true">
        <mask :id="maskId"><rect width="64" height="64" fill="#fff" /><circle cx="38" cy="26" r="19" fill="#000" /></mask>
        <circle cx="28" cy="34" r="22" fill="currentColor" :mask="`url(#${maskId})`" />
        <path d="m48 12 1.6 3.9 3.9 1.6-3.9 1.6L48 23l-1.6-3.9-3.9-1.6 3.9-1.6Z" class="t-brand__star" />
      </svg>
      <span class="t-brand__text">
        <span class="t-brand__name">{{ name }}</span>
        <span v-if="tagline" class="t-brand__tag">{{ tagline }}</span>
      </span>
    </template>
  </span>
</template>
