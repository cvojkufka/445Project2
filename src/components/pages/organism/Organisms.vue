<template>
  <Overlay 
    title="Organisms!"
    speechText="Look at all those organisms around you! Try clicking one!"
  />

  <div class="switch">
    <button class="home-sign" @click="goHome">
      <div class="sign-wrapper">
        <img :src="sign" alt="home-sign" />
        <span class="sign-text">Home</span>
      </div>
    </button>
  </div>

  <div class="scroll-wrapper">
    <div class="buttons" ref="scrollContainer" @wheel.prevent="handleWheel">
      <button
        v-for="item in data"
        :key="item.id"
        type="button"
        class="organism-button"
        @click="goLearn(item)"
      >
        <img :src="getImagePath(item.image)" :alt="item.name" />
        <div class="name-box">
          <p>{{ item.name }}</p>
        </div>
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import data from '../../data/plantsAtCP.json'
import sign from '../../../assets/Sign.png'
import Overlay from '../../overlay/Overlay.vue'

defineProps({
  goHome: Function,
  goLearn: Function
})

const scrollContainer = ref(null)

const handleWheel = (event) => {
  if (scrollContainer.value) {
    scrollContainer.value.scrollLeft += event.deltaY
  }
}

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
  cursor: pointer;
}

.sign-wrapper {
  position: relative;
  display: inline-block;
}

.sign-wrapper img {
  width: clamp(120px, 20vw, 400px);
  display: block;
}

.sign-wrapper:hover {
  transform: scale(1.1);
}


.sign-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: clamp(12px, 1.6vw, 22px);
  font-weight: bold;
  text-align: center;
  pointer-events: none;
  white-space: nowrap;
}

.scroll-wrapper {
  position: absolute;
  top: 230px;
  left: 50%;
  transform: translateX(-50%);
  width: 90%;
  overflow: hidden;
  z-index: 5;
}

.buttons {
  display: flex;
  flex-wrap: nowrap;
  gap: 60px;
  overflow-x: auto;
  overflow-y: hidden;
  padding: 20px;
  scrollbar-width: none;
  -ms-overflow-style: none;
  background-color: #8B4E2E;
  border-radius: 15px;
  border: 4px solid;
  border-color: #FFC300;
}

.buttons::-webkit-scrollbar {
  display: none;
}

.organism-button {
  flex: 0 0 auto;
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

.organism-button img:hover {
  box-shadow: 
    0 0 10px rgba(255, 195, 0, 0.6),
    0 0 20px rgba(255, 195, 0, 0.5),
    0 0 40px rgba(255, 195, 0, 0.4);
}


.name-box {
  margin-top: 15px;
  background-color: rgba(48, 132, 41, 1);
  border-radius: 15px;
  padding: 7px;

  border: 1px solid;
  border-color: #FFC300;
}

.name-box p {
  margin: 0;
  color: white;
  font-size: 20px;
  font-weight: bold;
  text-align: center;
}
</style>