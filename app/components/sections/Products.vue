<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-white">
    <div class="t-wrap">
      <div class="t-head">
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
        <RhText v-if="p.subtitle || editing" tag="p" class="t-lead" path="subtitle" :value="p.subtitle" ph="Texto" ml />
      </div>
      <RhProductShowcase :kind="p.source" :count="p.count" :layout="p.layout">
        <template #empty><p v-if="editing" class="t-empty">Nenhum produto deste tipo à venda na loja. No site, esta vitrine não aparece.</p></template>
      </RhProductShowcase>
      <div v-if="p.button || editing" class="t-center t-more"><NuxtLink to="/loja" class="t-btn t-btn--line"><RhText path="button" :value="p.button" ph="Botão" /></NuxtLink></div>
    </div>
  </section>
</template>
