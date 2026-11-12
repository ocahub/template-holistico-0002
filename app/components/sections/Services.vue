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
      <div class="t-cards">
        <article v-for="(it, i) in p.items" :key="i" class="t-svc">
          <RhText tag="span" class="t-svc__icon" :path="`items.${i}.icon`" :value="it.icon" ph="✦" />
          <RhText tag="h3" class="t-h3" :path="`items.${i}.title`" :value="it.title" ph="Título" />
          <RhText tag="p" class="t-svc__text" :path="`items.${i}.text`" :value="it.text" ph="Texto" ml />
          <TButton v-if="it.linkLabel || editing" class="t-arrow" :link="it.link" source="servicos"><RhText :path="`items.${i}.linkLabel`" :value="it.linkLabel" ph="Link" /> <span aria-hidden="true">→</span></TButton>
        </article>
      </div>
      <RhText v-if="p.note || editing" tag="p" class="t-note" path="note" :value="p.note" ph="Frase de fechamento" />
    </div>
  </section>
</template>
