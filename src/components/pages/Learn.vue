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
</template>

<script setup>
import banner from '../../assets/Banner.png'
import home from '../../assets/Home.png'

    defineProps ({
        goHome: Function
    })
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
</style>