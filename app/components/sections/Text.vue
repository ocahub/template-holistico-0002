<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
</script>

<template>
  <section class="t-sec t-white">
    <div class="t-wrap t-narrow">
      <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
      <RhText tag="p" class="t-body t-pre" path="body" :value="p.body" ph="Texto" ml />
    </div>
  </section>
</template>
