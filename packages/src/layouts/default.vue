<template>
  <div class="layout default">

    <AlgoliaModal />

    <SiteHeader />

    <Sidebar />

    <slot />

    <SiteFooter />

  </div>
</template>

<script setup>
// ===================================================================== Imports
import { storeToRefs } from 'pinia'

// ======================================================================= Setup
if (process.client && window.matchMedia('(prefers-color-scheme: dark)').matches) {
  useHead({
    meta: [
      { name: 'msapplication-config', content: '/public/favicon/light/browserconfig.xml' }
    ],
    link: [
      { rel: 'icon', type: 'image/x-icon', href: '/public/favicon/light/favicon-96x96.png' },
      { rel: 'manifest', href: '/public/favicon/light/manifest.json' }
    ]
  })
}

const generalStore = useGeneralStore()

// ======================================================================== Data
const { theme } = storeToRefs(generalStore)

// ======================================================================= Hooks
onMounted(() => {
  const initialTheme = localStorage.getItem('theme')
  generalStore.setTheme(initialTheme || theme.value)
})
</script>
