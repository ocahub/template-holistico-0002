<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-deep">
    <div class="t-wrap t-steps">
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
        <RhText v-if="p.subtitle || editing" tag="p" class="t-lead" path="subtitle" :value="p.subtitle" ph="Texto" ml />
      </div>
      <ol class="t-steps__list" :style="{ '--cols': Math.min(p.items?.length || 1, 4) }">
        <li v-for="(it, i) in p.items" :key="i" class="t-card">
          <span class="t-steps__n">{{ Number(i) + 1 }}</span>
          <RhText tag="h3" class="t-h3" :path="`items.${i}.title`" :value="it.title" ph="Título" />
          <RhText tag="p" class="t-small" :path="`items.${i}.text`" :value="it.text" ph="Texto" ml />
        </li>
      </ol>
    </div>
  </section>
</template>
