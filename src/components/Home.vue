<template>
  <div class="header">
    <img :src="banner" alt="bannerLogo" />
    <h2 class="overlay-text">Welcome!</h2>
  </div>

  <div class="organisms">
    <button type="button" @click="alert('Clicked!')">
        <img :src="organisms" alt="Click me!">
    </button>
    <p>Organisms in your Area</p>
  </div>

  <div class="map">
    <button type="button" @click="alert('Clicked!')">
        <img :src="map" alt="Click me!">
    </button>
    <p>Path Finding</p>
  </div>
</template>

<script setup>
import banner from '../assets/Banner.png'
import organisms from '../assets/Organisms.png'
import map from '../assets/Map.png'
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

/*Organisms Button*/
.organisms {
    position: absolute;
    top: 290px;
    left: 400px;
}

.organisms img {
    width: 200px;
    height: auto;
}

/*Map Button*/
.map {
    position: absolute;
    top: 290px;
    right: 400px;
}

.map img {
    width: 200px;
    height: auto;
}
</style>