<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
const company = useRhCompany()
const v = computed(() => company.values.value)
</script>

<template>
  <section class="t-hero t-contact">
    <div class="t-glow t-glow--a" aria-hidden="true" />
    <div class="t-wrap">
      <div class="t-contact__head">
        <RhText tag="p" class="t-eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
        <RhText tag="h1" class="t-hero__title" path="title" :value="p.title" ph="Título" />
        <RhText tag="p" class="t-lead" path="text" :value="p.text" ph="Texto" ml />
      </div>
      <div class="t-contact__grid">
        <div class="t-card">
          <h2 class="t-h3">WhatsApp</h2>
          <p class="t-small">{{ v.whatsapp || 'Cadastre o WhatsApp em Loja › Dados da loja › Contatos do site.' }}</p>
          <ul class="t-topics">
            <li v-for="(it, i) in p.topics" :key="i">
              <RhWhatsappButton :message="it.message" source="contato"><RhText :path="`topics.${i}.label`" :value="it.label" ph="Assunto" /> <span aria-hidden="true">→</span></RhWhatsappButton>
            </li>
          </ul>
          <RhWhatsappButton class="t-btn" source="contato"><RhText path="button" :value="p.button" ph="Botão" /></RhWhatsappButton>
        </div>
        <div class="t-contact__side">
          <a v-if="v.email" :href="`mailto:${v.email}`" class="t-card t-contact__card"><p class="t-eyebrow">E-mail</p><p class="t-contact__value">{{ v.email }}</p></a>
          <a v-if="v.instagram" :href="`https://www.instagram.com/${v.instagram.replace('@', '')}/`" target="_blank" rel="noopener" class="t-card t-contact__card"><p class="t-eyebrow">Instagram</p><p class="t-contact__value">{{ v.instagram }}</p></a>
          <div v-if="p.hours || editing" class="t-card"><p class="t-eyebrow">Horário de atendimento</p><RhText tag="p" path="hours" :value="p.hours" ph="Horário" /></div>
        </div>
      </div>
    </div>
  </section>
</template>
