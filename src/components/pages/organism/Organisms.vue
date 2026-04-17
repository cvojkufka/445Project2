<template>
  <div class="header">
    <img :src="banner" alt="bannerLogo" />
    <h2 class="overlay-text">Organisms!</h2>
  </div>

  <div class="home">
    <button @click="goHome">
      <img :src="home" :alt="home">
    </button>
  </div>

  <div class="search-container">
    <input 
      v-model="searchQuery"
      type="text"
      placeholder="Search for an organism..."
      class="search-input"
    />
  </div>

    <div class="buttons">
      <button @click="goLearn(item)"
        v-for="item in filteredData"
        :key="item.id"
        type="button"
        class="organism-button"
      >
        <img :src="getImagePath(item.image)" :alt="item.name" />
        <div class="name-box">
          <p>{{ item.name }}</p>
        </div>
      </button>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import data from '../../data/plantsAtCP.json'
import banner from '../../../assets/Banner.png'
import home from '../../../assets/Home.png'

defineProps({
  goHome: Function,
  goLearn: Function
})

const searchQuery = ref('')

const filteredData = computed(() => {
  if (!searchQuery.value) return data

  return data.filter(item =>
    item.type.toLowerCase().includes(searchQuery.value.toLowerCase())||
    item.name.toLowerCase().includes(searchQuery.value.toLowerCase())||
    item.description.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})


const getImagePath = (fileName) => {
  return new URL(`../../../assets/${fileName}`, import.meta.url).href
}
</script>

<style scoped>
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

/*Organism Buttons*/
.buttons {
  padding: 100px;
  display: flex;
  justify-content: center;
  gap: 30px;
  flex-wrap: wrap;
}

.organism-button {
  background: none;
  border: none;
  cursor: pointer;
  text-align: center;
}

.organism-button img {
  width: 200px;
  height: 200px;
  object-fit: cover;
  display: block;
}

.name-box {
  width: 200px;
  background-color: #a3a2a2;
  padding: 12px;
  margin-top: 0;
  text-align: center;
  color: rgb(0, 0, 0);
  font-size: 22px;
}

/*Search Bar*/
.search-container {
  margin-top: 200px;
  display: flex;
  justify-content: center;
}

.search-input {
  width: 300px;
  padding: 12px 16px;
  border-radius: 25px;
  border: 1px solid #ccc;
  outline: none;
  font-size: 16px;
  

  box-shadow: 0 4px 10px rgba(0,0,0,0.1);
  transition: 0.2s ease;
}

.search-input:focus {
  border-color: #4CAF50;
  box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}
</style>