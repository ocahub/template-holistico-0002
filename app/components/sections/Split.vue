<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-soft">
    <div class="t-wrap t-split" :class="{ 't-split--left': p.side === 'esquerda' }">
      <div class="t-split__text">
        <RhText tag="p" class="t-quote-text" path="text" :value="p.text" ph="Frase" ml />
        <TButton v-if="p.button || editing" class="t-btn" :link="p.link" source="texto-foto"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
      </div>
      <div class="t-split__photo"><img v-if="p.image" :src="p.image" alt="" loading="lazy"></div>
    </div>
  </section>
</template>
