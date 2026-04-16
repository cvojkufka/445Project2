<template>
  <div class="header">
    <img :src="banner" alt="bannerLogo" />
    <h2 class="overlay-text">Welcome!</h2>
  </div>

  <div class="welcome-layout">
    <div class="organisms">
      <button type="button" @click="goOrganisms">
          <img :src="organisms" alt="Click me!">
      </button>
      <div class="box">
          <p>Organisms Around You</p>
      </div>
    </div>

    <div class="welcome-message">
      <p>
        Welcome to our site! Explore the organisms around us on the left,
        or use the map on the right to find paths and nearby locations.
      </p>
    </div>

    <div class="map">
      <button type="button" @click="goMap">
          <img :src="map" alt="Click me!">
      </button>
      <div class="box">
          <p>Path Finding</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import banner from '../assets/Banner.png'
import organisms from '../assets/Organisms.png'
import map from '../assets/Map.png'

defineProps ({
  goOrganisms: Function,
  goMap: Function,
})
</script>

<style scoped>
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
  color: rgb(255, 255, 255);
  font-size: 2rem;
  font-weight: bold;
}

.welcome-layout {
  margin-top: 22rem;
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 60px;
}

.map img,
.organisms img {
    width: 200px;
    height: auto;
}

.map,
.organisms {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.welcome-message {
  width: min(30vw, 350px);
  min-height: 250px;
  padding: 20px;
  border-radius: 12px;
  display: flex;
  align-items: center;
  text-align: center;
  font-size: 1.5rem;
  line-height: 1.5;
}

/*Info Boxes*/
.box {
  width: 215px;           /* Sets the BOX width */
  height: 100px;          /* Sets the BOX height */
  padding: 20px;          /* Space inside the box (between content and border) */
  margin: 0px;           /* Space outside the box from button */
  background-color: #a3a2a2; /* Background */
  text-align: center;
  color: rgb(0, 0, 0);
}
</style>