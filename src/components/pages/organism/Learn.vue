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

  <div class="card">
    <img :src="getImagePath(item.image)" :alt="item.name" />
    <div class="text">
      <p>
        Name: {{ item.name }}
        <br />
        Scientific Name: {{ item.scientific_name }}
        <br />
        Description: {{ item.description }}
      </p>
    </div>
  </div>

  <div class="traverse">
    <button class="left-button" @click="prevItem">
      <img :src="arrow" alt="left" />
    </button>

    <button class="right-button" @click="nextItem">
      <img :src="arrow" alt="right" />
    </button>
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
  padding: 0;
  margin: 0;
  cursor: pointer;
  line-height: 0;
  display: block;
  width: 420px;
  height: auto;
}

.back-sign {
  left: 20px;
}

.home-sign {
  right: 20px;
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

.home-sign img {
  transform: scaleX(-1);
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

.card {
  display: flex;
  align-items: stretch;
  gap: 30px;
  position: absolute;
  top: 35%;
  left: 32%;
  transform: scale(1.2);
  z-index: 5;
}

.text {
  border-radius: 50px;
  width: 350px;
  height: 250px;
  padding: 20px;
  background-color: #02532c;
  display: flex;
  line-height: 1.4;
  text-align: left;
  color: white;
}

.card img {
  border-radius: 500px;
  height: 250px;
  width: 250px;
  object-fit: cover;
}

.traverse {
  position: absolute;
  top: 40%;
  left: 0;
  width: 100%;
  transform: translateY(-50%);
  z-index: 20;
  pointer-events: none;
}

.left-button,
.right-button {
  position: absolute;
  background: transparent;
  border: none;
  padding: 0;
  margin: 0;
  cursor: pointer;
  display: inline-block;
  line-height: 0;
  pointer-events: auto;
}

.left-button {
  left: 15%;
}

.right-button {
  right: 15%;
}

.left-button img,
.right-button img {
  display: block;
  width: 200px;
  height: auto;
  object-fit: cover;
}

.right-button img {
  transform: scaleX(-1);
}
</style>