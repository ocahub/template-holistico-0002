<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
</script>

<template>
  <section class="t-sec t-soft">
    <div class="t-wrap">
      <div class="t-head">
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
      </div>
      <div class="t-sessions" :style="{ '--cols': Math.min(p.items?.length || 1, 3) }">
        <article v-for="(it, i) in p.items" :key="i" class="t-session">
          <div class="t-arch t-session__photo"><img v-if="it.image" :src="it.image" alt="" loading="lazy"></div>
          <RhText tag="p" class="t-kicker" :path="`items.${i}.eyebrow`" :value="it.eyebrow" ph="Chamada" />
          <RhText tag="h3" class="t-h3" :path="`items.${i}.title`" :value="it.title" ph="Título" />
          <RhText tag="p" class="t-svc__text" :path="`items.${i}.text`" :value="it.text" ph="Texto" ml />
          <TButton class="t-arrow" :link="it.link" source="sessoes"><RhText :path="`items.${i}.linkLabel`" :value="it.linkLabel" ph="Link" /> <span aria-hidden="true">→</span></TButton>
        </article>
      </div>
    </div>
  </section>
</template>
