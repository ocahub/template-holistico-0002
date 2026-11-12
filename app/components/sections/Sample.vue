<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
// So quando a loja oferece a amostra gratis do mapa (painel › Mapa astral).
const on = useState('t:sample-on', () => false)
onMounted(async () => { on.value = await useRhBirthCharts().sampleEnabled() })
</script>

<template>
  <section v-if="on || editing" class="t-sample">
    <div class="t-wrap t-sample__row">
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h3" path="title" :value="p.title" ph="Título" />
        <p v-if="editing && !on" class="t-empty">A amostra grátis está desligada na loja: no site, esta faixa não aparece.</p>
      </div>
      <NuxtLink to="/mapa-astral" class="t-btn"><RhText path="button" :value="p.button" ph="Botão" /></NuxtLink>
    </div>
  </section>
</template>
