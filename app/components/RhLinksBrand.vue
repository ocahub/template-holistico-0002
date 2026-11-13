<script setup lang="ts">
// A marca da pagina /links (kit, 00050): a mesma do cabecalho - o logo da loja ou a lua com o nome.
const { global } = useRhSite()
const store = useRhStore()
const company = useRhCompany()
const p = computed(() => (global('header')?.props ?? {}) as Record<string, any>)
const logo = computed(() => p.value.logoImage || store.value?.logoUrl || '')
const name = computed(() => company.text(p.value.logo) || store.value?.name || '')
const tagline = computed(() => company.text(p.value.tagline))
</script>

<template>
  <div class="t-links-brand"><BrandMark :name="name" :tagline="tagline" :logo="logo" /></div>
</template>

<style>
.t-links-brand { display: flex; justify-content: center; transform: scale(1.35); transform-origin: center top; margin-bottom: 12px; }
</style>
