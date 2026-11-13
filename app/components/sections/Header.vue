<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const store = useRhStore()
const { menu } = useRhSite()
const company = useRhCompany()
const logo = computed(() => p.value.logoImage || store.value?.logoUrl || '')
const name = computed(() => company.text(p.value.logo) || store.value?.name || '')
const tagline = computed(() => company.text(p.value.tagline))
// Mapa astral (00026): a amostra gratis entra no menu quando a loja oferece.
const sampleOn = useState('t:sample-on', () => false)
onMounted(async () => { sampleOn.value = await useRhBirthCharts().sampleEnabled() })
// Blog (00049): no menu quando o site tem post no ar.
const blog = useRhBlogInfo()
const links = computed(() => [
  { to: '/', label: 'Início' },
  { to: '/loja', label: company.text(p.value.shopLabel) || 'Loja' },
  ...(sampleOn.value ? [{ to: '/mapa-astral', label: 'Mapa astral grátis' }] : []),
  ...menu.value.map(m => ({ to: m.slug, label: m.title })),
  ...(blog.enabled ? [{ to: blog.path, label: 'Blog' }] : [])
])
const route = useRoute()
const open = ref(false)
watch(() => route.fullPath, () => { open.value = false })
const active = (to: string) => (to === '/' ? route.path === '/' : route.path.startsWith(to))
</script>

<template>
  <header class="t-header">
    <div class="t-wrap t-header__row">
      <NuxtLink to="/" :aria-label="name"><BrandMark :name="name" :tagline="tagline" :logo="logo" /></NuxtLink>
      <nav class="t-nav" aria-label="Principal">
        <NuxtLink v-for="l in links" :key="l.to" :to="l.to" :class="{ 't-nav--on': active(l.to) }">{{ l.label }}</NuxtLink>
        <div class="t-header__actions"><RhAccountButton /><RhCartButton /></div>
      </nav>
      <div class="t-header__mobile">
        <RhCartButton />
        <button type="button" class="t-burger" :aria-expanded="open" :aria-label="open ? 'Fechar menu' : 'Abrir menu'" @click="open = !open">
          <svg v-if="!open" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" d="M4 7h16M4 12h16M4 17h10" /></svg>
          <svg v-else viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"><path stroke-linecap="round" d="M6 6l12 12M18 6 6 18" /></svg>
        </button>
      </div>
    </div>
    <nav v-if="open" class="t-mnav" aria-label="Principal">
      <div class="t-wrap">
        <NuxtLink v-for="l in links" :key="l.to" :to="l.to">{{ l.label }}</NuxtLink>
        <NuxtLink to="/minha-conta" class="t-mnav__small">Minha conta</NuxtLink>
        <NuxtLink to="/minha-conta/pedidos" class="t-mnav__small">Meus pedidos</NuxtLink>
      </div>
    </nav>
    <div class="t-rule" />
  </header>
</template>
