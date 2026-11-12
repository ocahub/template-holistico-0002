<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-sec t-soft">
    <div class="t-wrap t-faq">
      <div>
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h2" class="t-h2" path="title" :value="p.title" ph="Título" />
        <RhWhatsappButton v-if="p.whatsapp || editing" class="t-lead t-link" source="perguntas"><RhText path="whatsapp" :value="p.whatsapp" ph="Convite para o WhatsApp" /></RhWhatsappButton>
      </div>
      <div>
        <details v-for="(it, i) in p.items" :key="i" class="t-faq__item" :open="editing">
          <summary><RhText :path="`items.${i}.q`" :value="it.q" ph="Pergunta" /><span class="t-faq__plus" aria-hidden="true">+</span></summary>
          <RhText tag="p" :path="`items.${i}.a`" :value="it.a" ph="Resposta" ml />
        </details>
      </div>
    </div>
  </section>
</template>
