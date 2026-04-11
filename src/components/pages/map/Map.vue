<template>
    <div class="header">
        <img :src="banner" alt="bannerLogo" />
        <h2 class="overlay-text">Map</h2>
    </div>
  
    <div class="home">
        <button @click="goHome">
        <img :src="home" :alt="home">
        </button>
    </div>

    <div class="map-image-wrapper">
        <img :src="map" alt="Map">
    </div>

    <div class="nearby-sites">
        <button @click="goSites">
            Nearby Sites
        </button>
    </div>
</template>

<script setup>
import banner from '../../../assets/Banner.png'
import home from '../../../assets/Home.png'
import map from '../../../assets/map.webp'

defineProps({
  goHome: Function,
  goSites: Function
})
</script>


<style scoped>
.header {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: min(70vw, 650px);
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

.map-image-wrapper {
    display: flex;
    justify-content: center;
    margin-top: 220px;
}

.map-image-wrapper img {
    width: min(90vw, 850px);
    height: auto;
}

.nearby-sites {
    display: flex;
    justify-content: center;
    margin-top: 20px;
}

.nearby-sites button {
    box-sizing: border-box;
    font-size: 40px;
    border-radius: 3rem;
    background-color: rgba(48, 132, 41, 1);
    color: white;
    padding: 0.5rem 5rem;
}

</style>