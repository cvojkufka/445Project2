<template>
  <div class="header">
    <img :src="banner" alt="bannerLogo" />
    <h2 class="overlay-text">Welcome!</h2>
  </div>

  <div class="organisms">
    <button type="button" @click="goOrganisms">
        <img :src="organisms" alt="Click me!">
    </button>
    <div class="box">
        <p>Organisms Around You</p>
    </div>
  </div>

  <div class="map">
    <button type="button" @click="alert('Clicked!')">
        <img :src="map" alt="Click me!">
    </button>
    <div class="box">
        <p>Path Finding</p>
    </div>
  </div>
</template>

<script setup>
import banner from '../assets/Banner.png'
import organisms from '../assets/Organisms.png'
import map from '../assets/Map.png'

defineProps ({
  goOrganisms: Function,
  goMap: Function
})
</script>

<style>
/*Heading Banner And Text*/
.header { 
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: fit-content;
}

.header img {
  width: 100%;
}

.overlay-text {
  position: absolute;
  top: 20%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: white;
  font-size: 2rem;
  font-weight: bold;
}

/*Organisms Button from Screen*/
.organisms {
    left: 400px;
}

/*Map Button from Screen*/
.map {
    right: 400px;
}

/*Button Placement and Sizing*/
.map,
.organisms {
    position: absolute;
    top: 270px;
}

.map img,
.organisms img {
    width: 200px;
    height: auto;
}

/*Info Boxes*/
.box {
  width: 215px;           /* Sets the BOX width */
  height: 100px;          /* Sets the BOX height */
  padding: 20px;          /* Space inside the box (between content and border) */
  margin: 0px;           /* Space outside the box from button */
  background-color: #a3a2a2; /* Background */
  text-align: center;
}
</style>