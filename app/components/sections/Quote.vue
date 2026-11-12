<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-wine t-center">
    <div class="t-wrap">
      <MoonPhases />
      <RhText tag="blockquote" class="t-quote" path="text" :value="p.text" ph="Frase" ml />
      <TButton v-if="p.button || editing" class="t-btn t-btn--light" :link="p.link" source="citacao"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
    </div>
  </section>
</template>
