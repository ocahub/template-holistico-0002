<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section v-if="p.items?.length || editing" class="t-sec t-white">
    <div class="t-wrap">
      <div class="t-head">
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
      </div>
      <p v-if="!p.items?.length" class="t-empty t-center">Sem depoimentos: no site, esta seção não aparece. Adicione no formulário ao lado.</p>
      <div class="t-cards">
        <figure v-for="(it, i) in p.items" :key="i" class="t-testi">
          <span class="t-testi__mark" aria-hidden="true">“</span>
          <RhText tag="blockquote" :path="`items.${i}.quote`" :value="it.quote" ph="Depoimento" ml />
          <figcaption><RhText tag="b" :path="`items.${i}.name`" :value="it.name" ph="Nome" /> · <RhText :path="`items.${i}.detail`" :value="it.detail" ph="Atendimento" /></figcaption>
        </figure>
      </div>
    </div>
  </section>
</template>
