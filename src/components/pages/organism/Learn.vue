<template>
    <Overlay 
    title="Learn!"
    :speechText="`Wow! A ${item.name}!`"
  />

  <div class="content">
    <button class="back-sign" @click="goOrganisms">
    <div class="sign-wrapper">
      <img :src="sign" alt="back-sign"/>
      <span class="sign-text">Back To Organisms</span>
    </div>
    </button>

    <button class="home-sign" @click="goHome">
      <div class="sign-wrapper">
        <img :src="sign" alt="home-sign"/>
        <span class="sign-text">Home</span>
      </div>
    </button>
  </div>

  <div class="card">
    <img :src="getImagePath(item.image)" :alt="item.name" />
    <div class="text">
        <p>Name: {{ item.name }}
        <br>Scientific Name: {{ item.scientific_name }}</br>
        <br>Description: {{ item.description }}
        </p>
    </div>
  </div>
</template>

<script setup>
import Overlay from '../../overlay/Overlay.vue'
import sign from '../../../assets/Sign.png'

    defineProps ({
        goHome: Function,
        goOrganisms: Function,
        item: Object
    })

const getImagePath = (fileName) => {
  return new URL(`../../../images/${fileName}`, import.meta.url).href
}
</script>

<style scoped>
.content {
  position: relative;
  z-index: 5;
  width: 100%;
  height: 100vh;
}

.back-sign,
.home-sign {
  position: absolute;
  top: -15%;
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
}

.back-sign {
  left: 1%;
}

.home-sign {
  right: 1%;
}

.back-sign img,
.home-sign img {
  width: 420px;
}

.home-sign img {
  transform: scaleX(-1);
}

.sign-wrapper {
  position: relative;
  display: inline-block;
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
}

/*Card Layout*/
.card {
  display: flex;
  align-items: stretch;
  gap: 0px;

  position: absolute;
  top: 320px;
  left: 420px;
  transform: scale(1.5);
}

.text {
  width: 300px;
  height: 300px;
  padding: 20px;
  background-color: #a3a2a2;

  display: flex;
  line-height: 1.4;
  text-align: left;
  color: rgb(0, 0, 0);
}

.card img {
  height: 300px;
  width: 300px;
  object-fit: cover;
}
</style>