
<template>
  <Home
   v-if="currentPage === 'home'"
   :goOrganisms="goOrganisms"
   :goMap="goMap"
   />

  <Organisms
    v-else-if="currentPage === 'organisms'"
    :goHome="goHome"
    :goLearn="goLearn"
   />

   <Learn 
   v-else-if="currentPage === 'learn'"
   :item="selectedItem"
   :goHome="goHome"
   />
</template>

<script setup>
import { ref } from 'vue'
import Home from './components/Home.vue'
import Organisms from './components/pages/Organisms.vue'
import Learn from './components/pages/Learn.vue'

const currentPage = ref('home')
const selectedItem = ref(null)

const goHome = () => {
  currentPage.value = 'home'
}

const goOrganisms = () => {
  currentPage.value = 'organisms'
}

const goLearn = (item) => {
  selectedItem.value = item
  currentPage.value = 'learn'
}
</script>