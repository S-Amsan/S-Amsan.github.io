<script setup lang="ts">
  import { onMounted } from 'vue'
  import BackgroundIconAnimation from '@/components/BackgroundIconAnimation.vue'

  onMounted(() => {
    const bouton = document.getElementById('boutonCv')
    if (!bouton) return
    bouton.addEventListener('click', function () {
      const fileUrl = '/documents/Cv.pdf'

      const anchor = document.createElement('a')
      anchor.href = fileUrl
      anchor.download = 'test.pdf'
      document.body.appendChild(anchor)
      anchor.click()
      document.body.removeChild(anchor)
    })
  })

</script>

<template>
  <section id="accueil">
    <BackgroundIconAnimation/>
    <text id="nomTextFond" class="text-degradé">Amsan</text>
    <div id="contenu">
      <text id="metierText" class="text-degradé-calme">Développeur Full Stack</text>
      <div id="amsanContainer">
        <img src="../assets/images/cursorMac.png" alt="" id="cursor">
        <img src="../assets/images/Amsan_Cartoon.png" alt="" id="amsanImage" />
      </div>
      <div id="contenuBas">
        <text id="presentationText" class="text-degradé-calme">
          Étudiant en 3ᵉ année de BUT Informatique à l’IUT Paris Rives de Seine,
          je développe des applications web et mobiles en accordant une attention particulière à la qualité du code,
          à l’architecture et à l’expérience utilisateur.
        </text>
        <button id="boutonCv">
          <span id="boutonText">TÉLÉCHARGER MON CV</span>
        </button>
      </div>
    </div>
  </section>
</template>

<style scoped>
  #nomTextFond {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);

    font-family: 'Alkalami', serif;
    font-size: 430px;
    letter-spacing: 30px;
    user-select: none;
    z-index: -1;
  }
  #contenu {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }
  #metierText {
    font-family: 'Poppins', sans-serif;
    font-weight: 550;
    font-size: 50px;

    user-select: none;
  }
  #amsanContainer{
    position: relative;
    display: flex;
  }
  @keyframes cursorAnimation {
    0% {
      top: 50px;
      left: 70px;
      rotate: 120deg;
    }
    20% {
      top: 20px;
      left: 90px;
      rotate: 130deg;
    }
    50%{
      top: -10px;
      left: 150px;
      rotate: 180deg;
    }
    80%{
      top: 20px;
      left: 220px;
      rotate: 230deg;
    }
    100% {
      top: 50px;
      left: 230px;
      rotate: 250deg;
    }
  }
  #cursor{
    position: absolute;

    width: 30px;
    height: 30px;

    animation: 3s cursorAnimation infinite alternate;

    user-select: none;
  }
  #amsanImage {
    width: 350px;
    height: 525px;

    filter: grayscale(100%) brightness(0.25) contrast(1.3);

    transition: filter 1s ease;
    cursor: pointer;
    user-select: none;

    z-index: 2;
  }

  #amsanImage:hover {
    filter: none;
  }

  #contenuBas {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    gap: 20px;
  }
  #presentationText {
    font-family: 'Poppins', sans-serif;
    font-weight: 500;
    font-size: 20px;
    text-align: center;
    width: 33%;
  }
  #boutonCv {
    position: relative;
    padding: 15px 30px;
    border-radius: 30px;
    border: 2px solid transparent;

    background:
      linear-gradient(#ffffff, #ffffff) padding-box,
      var(--degradeHorizontal) border-box;

    cursor: pointer;
    overflow: hidden;
  }
  #boutonCv::before {
    content: '';
    position: absolute;
    inset: 0;
    background: var(--degradeHorizontal);
    border-radius: inherit;

    transform: scaleX(0);
    transform-origin: left;
    transition: transform 0.4s ease;

    z-index: 0;
  }
  #boutonText {
    position: relative;
    z-index: 1;

    background: var(--degradeVertical);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;

    transition: -webkit-text-fill-color 0.3s ease;
  }
  #boutonCv:hover::before {
    transform: scaleX(1);
  }

  #boutonCv:hover #boutonText {
    background: none;
    -webkit-text-fill-color: #ffffff;
  }
</style>
