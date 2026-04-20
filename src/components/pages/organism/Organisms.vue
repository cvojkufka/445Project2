<template>
  <Overlay 
    title="Organisms!"
    speechText="Look at all those organisms! Try clicking one!"
  />

  <div class="switch">
    <button class="home-sign" @click="goHome">
      <div class="sign-wrapper">
        <img :src="sign" alt="home-sign" />
        <span class="sign-text">Home</span>
      </div>
    </button>
  </div>

  <div class="buttons">
    <button
      v-for="item in visibleOrganisms"
      :key="item.id"
      @click="goLearn(item)"
      type="button"
      class="organism-button"
    >
      <img :src="getImagePath(item.image)" :alt="item.name" />
      <div class="name-box">
        <p>{{ item.name }}</p>
      </div>
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import data from '../../data/plantsAtCP.json'
import sign from '../../../assets/Sign.png'
import Overlay from '../../overlay/Overlay.vue'

defineProps({
  goHome: Function,
  goLearn: Function
})

const startIndex = ref(0)

const visibleOrganisms = computed(() => {
  return data.slice(startIndex.value, startIndex.value + 3)
})

const getImagePath = (fileName) => {
  return new URL(`../../../images/${fileName}`, import.meta.url).href
}
</script>

<style scoped>
.switch {
  position: relative;
  width: 100%;
  z-index: 10;
}

.home-sign {
  position: absolute;
  top: 50px;
  left: 20px;
  background: transparent;
  border: none;
  padding: 0;
  margin: 0;
  cursor: pointer;
  line-height: 0;
  display: block;
  width: 420px;
  height: auto;
}

.sign-wrapper {
  position: relative;
  display: block;
  width: 420px;
}

.sign-wrapper img {
  width: 420px;
  display: block;
}

.sign-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 22px;
  font-weight: bold;
  text-align: center;
  pointer-events: none;
  white-space: nowrap;
}

/*Organism Buttons*/
.buttons {
  position: absolute;
  top: 280px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  justify-content: center;
  gap: 60px;
  width: 100%;
  z-index: 5;
}

.organism-button {
  background: none;
  border: none;
  cursor: pointer;
  text-align: center;
}

.organism-button img {
  width: 220px;
  height: 220px;
  object-fit: cover;
  border-radius: 500px;
  display: block;
}

.name-box {
  margin-top: 12px;
}

.name-box p {
  color: white;
  font-size: 20px;
  font-weight: bold;
}
</style>