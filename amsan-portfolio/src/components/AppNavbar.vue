<script setup lang="ts">
import { onMounted, ref } from 'vue'

  type SectionId = "accueil" | "aPropos" | "projets" | "contact";

  const liens: Array<{ id: SectionId; label: string }> = [
    {id : "accueil", label: "Accueil" },
    {id : "aPropos", label: "À propos" },
    {id : "projets", label: "Projets" },
    {id : "contact", label: "Contact" },
  ]

  const activeSection = ref<SectionId>("accueil")

  function goTo(id: SectionId) {
    activeSection.value = id as SectionId
    history.replaceState(null, '', `#${id}`)

    const el = document.getElementById(id)
    if (!el) return
    el.scrollIntoView({ behavior: 'smooth', block: 'start' })
  }

  onMounted(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting){
          const id = entry.target.id as SectionId
          activeSection.value = id
          history.replaceState(null, '', `#${id}`)
        }
      })
    },
      {
        threshold: [0.5],
      }
    )

    liens.forEach((lien) => {
      const section = document.getElementById(lien.id)
      if (section) observer.observe(section)
    })
  })

</script>

<template>
  <nav id="navbar">
    <a
      v-for="lien in liens"
      :key="lien.id"
      :href="`#${lien.id}`"
      class="lien"
      :class="{active: activeSection === lien.id}"
      @click.prevent="goTo(lien.id)"
    >
      {{lien.label}}
    </a>
  </nav>
</template>

<style scoped>
  #navbar {
    position: fixed;
    top: 0;
    width: 100%;
    padding: 30px 0;

    display: flex;
    justify-content: center;
    align-items: center;
    gap: 40px;
  }

  .lien {
    text-decoration: none;
    font-family: 'Poppins', sans-serif;
    font-size: 18px;
    position: relative;
    padding-bottom: 5px;

    background: var(--degradeVertical);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .lien::before {
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 0;
    height: 2px;
    background: var(--degradeHorizontal);
    transform: translateX(-50%);
    transition: width 0.3s ease, opacity 0.3s ease;
    opacity: 0;
  }

  .lien:hover::before {
    width: 100%;
    opacity: 1;
  }

  .lien.active::before {
    width: 100%;
    opacity: 1;
  }

</style>
