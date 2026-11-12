<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
const photos = computed(() => !!(p.value.image1 || p.value.image2 || p.value.image3))
</script>

<template>
  <section class="t-sec t-soft">
    <div class="t-wrap t-timeline" :class="{ 't-timeline--solo': !photos }">
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
        <RhText tag="p" class="t-body" path="text" :value="p.text" ph="Texto" ml />
        <ol class="t-timeline__list">
          <li v-for="(it, i) in p.items" :key="i">
            <RhText tag="p" class="t-kicker" :path="`items.${i}.step`" :value="it.step" ph="Etiqueta" />
            <RhText tag="h3" class="t-h3" :path="`items.${i}.title`" :value="it.title" ph="Título" />
            <RhText tag="p" class="t-body" :path="`items.${i}.text`" :value="it.text" ph="Texto" ml />
          </li>
        </ol>
        <RhText v-if="p.closing || editing" tag="p" class="t-closing" path="closing" :value="p.closing" ph="Frase de fechamento" ml />
        <RhText v-if="p.closingText || editing" tag="p" class="t-body t-pre" path="closingText" :value="p.closingText" ph="Texto de fechamento" ml />
      </div>
      <div v-if="photos" class="t-timeline__photos">
        <div v-if="p.image1" class="t-arch t-timeline__big"><img :src="p.image1" alt="" loading="lazy"></div>
        <div v-if="p.image2" class="t-timeline__small"><img :src="p.image2" alt="" loading="lazy"></div>
        <div v-if="p.image3" class="t-timeline__small"><img :src="p.image3" alt="" loading="lazy"></div>
      </div>
    </div>
  </section>
</template>
