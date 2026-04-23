<template>
  <Overlay 
    title="Learn!"
    :speechText="`Wow! A ${item.name}!`"
  />

  <div class="switch">
    <button class="back-sign" @click="goOrganisms">
      <div class="sign-wrapper">
        <img :src="sign" alt="back-sign" />
        <span class="sign-text">Back To Organisms</span>
      </div>
    </button>

    <button class="home-sign" @click="goHome">
      <div class="sign-wrapper">
        <img :src="sign" alt="home-sign" />
        <span class="sign-text">Home</span>
      </div>
    </button>
  </div>

  <div class="content-wrapper">
    <div class="card-row">
      <button class="left-button" @click="prevItem">
        <img :src="arrow" alt="left" />
      </button>

      <div class="card">
        <img :src="getImagePath(item.image)" :alt="item.name" />
        <div class="text">
          <p>
            <h1>Name:</h1> {{ item.name }}
            <h1>Scientific Name:</h1> {{ item.scientific_name }}
            <h1>Description:</h1> {{ item.description }}
          </p>
        </div>
      </div>

      <button class="right-button" @click="nextItem">
        <img :src="arrow" alt="right" />
      </button>
    </div>
  </div>
</template>

<script setup>
import Overlay from '../../overlay/Overlay.vue'
import sign from '../../../assets/Sign.png'
import arrow from '../../../assets/Arrow.png'

defineProps({
  goHome: Function,
  goOrganisms: Function,
  item: Object,
  prevItem: Function,
  nextItem: Function
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

.back-sign,
.home-sign {
  position: absolute;
  top: 50px;
  background: transparent;
  border: none;
  cursor: pointer;
}

.back-sign {
  left: 20px;
}

.home-sign {
  right: 20px;
}

.sign-wrapper {
  position: relative;
  display: inline-block;
}

.sign-wrapper:hover {
  transform: scale(1.1);
}

.sign-wrapper img {
  width: clamp(120px, 20vw, 400px);
  display: block;
}

.home-sign img {
  transform: scaleX(-1);
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

.content-wrapper {
  position: absolute;
  top: 230px;
  left: 50%;
  transform: translateX(-50%) scale(1);
  transform-origin: top center;
  width: fit-content;
  z-index: 5;
}

.card-row {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 60px;
}

.card {
  display: flex;
  align-items: stretch;
  gap: 50px;
  height: clamp(250px, 50vh, 350px);
}

.left-button,
.right-button {
  background: transparent;
  border: none;
  padding: 0;
  margin: 0;
  cursor: pointer;
  line-height: 0;
}

.left-button:hover,
.right-button:hover {
  transform: scale(1.1);
}

.left-button img,
.right-button img {
  display: block;
  width: clamp(10px, 10vw, 200px);
  height: auto;
}

.right-button img {
  transform: scaleX(-1);
}

.text {
  border-radius: 50px;
  width: clamp(300px, 30vw, 370px);
  height: clamp(150px, 40vh, 350px);
  padding: 20px;
  background-color: #02532c;
  display: flex;
  line-height: 1.4;
  text-align: left;
  color: white;
}

.card img {
  border-radius: 500px;
  height: clamp(180px, 35vh, 350px);
  width: clamp(180px, 35vh, 350px);
  object-fit: cover;
}

.text h1 {
  font-size: 16px;
  color: #FFC300;
  margin-bottom: 1px;
}

.text p {
  font-size: 15px;
  color: #E0E0E0;;
}
</style>