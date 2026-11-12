<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-hero">
    <div class="t-glow t-glow--a" aria-hidden="true" />
    <div class="t-glow t-glow--b" aria-hidden="true" />
    <div class="t-wrap t-hero__grid" :class="{ 't-hero__grid--solo': !p.image }">
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h1" class="t-hero__title" path="title" :value="p.title" ph="Título" />
        <RhText tag="p" class="t-lead t-hero__lead" path="subtitle" :value="p.subtitle" ph="Texto" ml />
        <div class="t-actions">
          <TButton class="t-btn" :link="p.link" source="abertura"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
          <TButton v-if="p.button2 || editing" class="t-btn t-btn--line" :link="p.link2" source="abertura"><RhText path="button2" :value="p.button2" ph="Botão secundário" /></TButton>
        </div>
        <ul v-if="p.bullets?.length" class="t-hero__bullets">
          <li v-for="(b, i) in p.bullets" :key="i"><span aria-hidden="true">✦</span> <RhText :path="`bullets.${i}.label`" :value="b.label" ph="Destaque" /></li>
        </ul>
      </div>
      <div v-if="p.image" class="t-hero__media">
        <ZodiacWheel class="t-hero__wheel" />
        <div class="t-arch t-hero__photo"><img :src="p.image" alt="" fetchpriority="high"></div>
        <div v-if="p.badgeTitle || editing" class="t-card t-hero__badge">
          <span class="t-hero__badge-icon" aria-hidden="true">☾</span>
          <span><RhText tag="b" path="badgeTitle" :value="p.badgeTitle" ph="Selo" /><RhText path="badgeText" :value="p.badgeText" ph="Texto do selo" /></span>
        </div>
      </div>
    </div>
  </section>
</template>
