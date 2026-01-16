<script setup lang="ts">
  // Components
  import AppNavbar from '@/components/AppNavbar.vue'

  // Sections
  import Accueil from '@/sections/AccueilSection.vue'
  import APropos from '@/sections/AProposSection.vue'
  import Projets from '@/sections/ProjetsSection.vue'
  import Contact from '@/sections/ContactSection.vue'
</script>

<template>
  <AppNavbar/>

  <Accueil/>
  <APropos/>
  <Projets/>
  <Contact/>
</template>

<style scoped></style>
