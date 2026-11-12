<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-wine">
    <div class="t-wrap t-about">
      <div class="t-arch t-about__photo"><img v-if="p.image" :src="p.image" alt="" loading="lazy"></div>
      <div>
        <RhText tag="p" class="t-eyebrow t-eyebrow--gold" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-about__title" path="title" :value="p.title" ph="Título" />
        <RhText tag="p" class="t-about__text" path="text" :value="p.text" ph="Texto" ml />
        <TButton v-if="p.button || editing" class="t-btn t-btn--light" :link="p.link" source="sobre"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
      </div>
    </div>
  </section>
</template>
