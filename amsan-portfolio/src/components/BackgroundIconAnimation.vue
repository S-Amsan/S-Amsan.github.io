<script setup lang="ts">
  import JsIcon from "../assets/images/technologies/Js.png"
  import TsIcon from "../assets/images/technologies/Ts.png"
  import Vue3 from "../assets/images/technologies/Vue3.png"
  import { onMounted, ref } from 'vue'

  type Technologie = {
    image : string,
    couleur : string,
    position : number,
    delay : number
  }

  const technologies = ref<Technologie[]>([
    {image : JsIcon, couleur : "#FFFF00", position : 0, delay : 0},
    {image : TsIcon, couleur : "#479bff", position : 0, delay : 0},
    {image : Vue3, couleur : "#a9f1d3", position : 0, delay : 0},
  ])

  const getRandomPosition : () => number = () => {
    return Math.random() * (90 - 10) + 10
  }

  const getRandomDelay : () => number = () => {
    return ((Math.random() * 1000))
  }

  onMounted(() => {

    technologies.value = technologies.value.map((t,i) => ({
      ...t,
      position : getRandomPosition(),
      delay : getRandomDelay() + (2000 * i),
    }))

  })

  function onAnimationIteration(t: Technologie, e: AnimationEvent) {
    if (e.animationName.startsWith("flottement")) return
    t.position = getRandomPosition()
    t.delay = getRandomDelay()
  }


</script>

<template>
  <div class="container">
    <img
      v-for="(t, index) in technologies"
      :key="index"
      :src="t.image"
      alt=""
      class="technologie"
      :style="{
        boxShadow: `0px 1px 11px 0px ${t.couleur}`,
        top: `${t.position}%`,
        animationDelay: `${t.delay}ms`,
      }"
      @animationiteration="onAnimationIteration(t, $event)"
    >
  </div>
</template>

<style scoped>
  .container{
    position: absolute;
    width: 100%;
    height: 100%;

    overflow: hidden;

    pointer-events: none;
  }

  @keyframes glissement {
    from {
      left: -5%;
    }
    to {
      left: 100%;
    }
  }

  @keyframes flottement {
    0%, 100% { transform: translateY(0); }
    50%      { transform: translateY(-10px); }
  }


  .technologie{
    position: absolute;

    left : -5%;

    width: 30px;
    height: 30px;

    border-radius: 5px;

    animation: 15s linear glissement infinite,
                          flottement 2.5s ease-in-out infinite;

    pointer-events: auto;
    user-select: none;
    z-index: 1;
  }
  .technologie:hover{
    animation-play-state: paused;
    cursor: pointer;
  }

</style>
