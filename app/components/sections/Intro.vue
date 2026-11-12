<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-hero t-intro">
    <div class="t-glow t-glow--b" aria-hidden="true" />
    <div class="t-wrap t-hero__grid" :class="p.image ? 't-intro__grid' : 't-hero__grid--solo'">
      <div v-if="p.image" class="t-arch t-intro__photo"><img :src="p.image" alt="" fetchpriority="high"></div>
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h1" class="t-hero__title t-intro__title" path="title" :value="p.title" ph="Título" />
        <RhText tag="p" class="t-lead t-hero__lead" path="lead" :value="p.lead" ph="Texto em destaque" ml />
        <RhText v-if="p.text || editing" tag="p" class="t-body t-pre" path="text" :value="p.text" ph="Texto" ml />
        <div v-if="p.button || p.button2 || editing" class="t-actions">
          <TButton v-if="p.button || editing" class="t-btn" :link="p.link" source="apresentacao"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
          <TButton v-if="p.button2 || editing" class="t-btn t-btn--line" :link="p.link2" source="apresentacao"><RhText path="button2" :value="p.button2" ph="Botão secundário" /></TButton>
        </div>
      </div>
    </div>
  </section>
</template>
