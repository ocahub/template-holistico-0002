<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const store = useRhStore()
const company = useRhCompany()
const { global, menu } = useRhSite()
const header = computed(() => global('header')?.props ?? {})
const name = computed(() => company.text(header.value.logo) || store.value?.name || '')
const insta = computed(() => company.values.value.instagram)
</script>

<template>
  <footer class="t-footer">
    <div class="t-wrap t-footer__grid">
      <div>
        <BrandMark :name="name" :tagline="company.text(header.tagline)" light />
        <RhText tag="p" class="t-footer__about" path="about" :value="p.about" ph="Sobre a marca" ml />
        <MoonPhases class="t-moons--start" />
      </div>
      <nav aria-label="Rodapé">
        <p class="t-footer__title">Navegue</p>
        <ul>
          <li><NuxtLink to="/">Início</NuxtLink></li>
          <li><NuxtLink to="/loja">{{ company.text(header.shopLabel) || 'Loja' }}</NuxtLink></li>
          <li v-for="m in menu" :key="m.id"><NuxtLink :to="m.slug">{{ m.title }}</NuxtLink></li>
          <li><NuxtLink to="/minha-conta">Minha conta</NuxtLink></li>
        </ul>
      </nav>
      <div>
        <p class="t-footer__title">Fale comigo</p>
        <ul>
          <li><RhWhatsappButton source="rodape"><RhText path="whatsapp" :value="p.whatsapp" ph="WhatsApp" /></RhWhatsappButton></li>
          <li><RhText path="email" :value="p.email" ph="E-mail" /></li>
          <li v-if="insta"><a :href="`https://www.instagram.com/${insta.replace('@', '')}/`" target="_blank" rel="noopener"><RhText path="instagram" :value="p.instagram" ph="Instagram" /></a></li>
        </ul>
        <RhText tag="p" class="t-footer__hours" path="hours" :value="p.hours" ph="Horário" />
      </div>
    </div>
    <div class="t-footer__bottom">
      <div class="t-wrap t-footer__copy">
        <p>© {{ new Date().getFullYear() }} {{ name }}. Todos os direitos reservados.</p>
        <RhText tag="p" path="note" :value="p.note" ph="Linha final" />
      </div>
    </div>
  </footer>
</template>
