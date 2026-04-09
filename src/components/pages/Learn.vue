<template>
    <div class="header">
    <img :src="banner" alt="bannerLogo" />
    <h2 class="overlay-text">Learn!</h2>
  </div>

  <div class="home">
    <button @click="goHome">
      <img :src="home" :alt="home">
    </button>
  </div>

  <div class="card">
    <img :src="getImagePath(item.image)" :alt="item.name" />
    <div class="text">
        <p>Name: {{ item.name }}
        <br>Species: {{ item.species }}
        <br>Description: {{ item.description }}
        </p>
    </div>
  </div>
</template>

<script setup>
import banner from '../../assets/Banner.png'
import home from '../../assets/Home.png'

    defineProps ({
        goHome: Function,
        item: Object
    })

const getImagePath = (fileName) => {
  return new URL(`../../assets/${fileName}`, import.meta.url).href
}
</script>

<style>
/*Banner*/
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

/*Home Button*/
.home {
  display: flex;
  align-items: center;

  height: 100px;
  width: 100px;

  border-radius: 100px;
  border: 2px solid black;
  background: white;

  overflow: hidden;
  cursor: pointer;
  justify-content: center;
  top: 50px;
  left: 150px;
  position: absolute;
}

.home img {
  width: 100%;
  height: auto;
  object-fit: cover;
  transform: scale(1.7);
}

/*Card Layout*/
.card {
  display: flex;
  align-items: stretch;
  gap: 0px;

  position: absolute;
  top: 320px;
  left: 500px;
  transform: scale(1.5);
}

.text {
  width: 400px;
  height: 300px;
  padding: 20px;
  background-color: #a3a2a2;

  display: flex;
  text-align: left;
  color: rgb(0, 0, 0);
}

.card img {
  height: 300px;
  width: auto;
  object-fit: cover;
}
</style>