
<template>
  <Home
   v-if="currentPage === 'home'"
   :goOrganisms="goOrganisms"
   :goMap="goMap"
   />

  <Organisms
    v-else-if="currentPage === 'organisms'"
    :goHome="goHome"
   />
</template>

<script setup>
import { ref } from 'vue'
import Home from './components/Home.vue'
import Organisms from './components/pages/Organisms.vue'

const currentPage = ref('home')

const goHome = () => {
  currentPage.value = 'home'
}

const goOrganisms = () => {
  currentPage.value = 'organisms'
}
</script>