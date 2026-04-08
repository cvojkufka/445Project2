<template>
  <div class="page">
    <div class="top-section">
      <h1>Organisms Page</h1>
      <p>Select an organism to view what is around you.</p>
      <button class="home-button" @click="goHome">Back to Home</button>
    </div>

    <div class="buttons">
      <button
        v-for="item in data"
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
  </div>
</template>

<script setup>
import data from '../data/organisms.json'

defineProps({
  goHome: Function
})

const getImagePath = (fileName) => {
  return new URL(`../../assets/${fileName}`, import.meta.url).href
}
</script>

<style>
.page {
  padding: 30px;
}

.top-section {
  text-align: center;
  margin-bottom: 40px;
}

.home-button {
  margin-top: 15px;
  padding: 10px 16px;
  cursor: pointer;
}

.buttons {
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
}
</style>