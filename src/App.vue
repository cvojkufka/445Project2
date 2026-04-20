
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

  <Map
    v-else-if="currentPage === 'map'"
    :goHome="goHome"
    :goSiteDetails="goSiteDetails"
  />

   <Learn 
   v-else-if="currentPage === 'learn'"
   :item="currentItem"
   :goHome="goHome"
   :goOrganisms="goOrganisms"
   :prevItem="prevItem"
   :nextItem="nextItem"
   />

    <SiteDetail
    v-else-if="currentPage === 'site-detail'"
    :site="selectedSite"
    :goMap="goMap"
   />

</template>

<script setup>
import { ref, computed } from 'vue'
import Home from './components/Home.vue'
import Organisms from './components/pages/organism/Organisms.vue'
import Learn from './components/pages/organism/Learn.vue'
import Map from './components/pages/map/Map.vue'
import SiteDetail from './components/pages/map/SiteDetail.vue'
import data from './components/data/plantsAtCP.json'

const currentPage = ref('home')
const selectedSite = ref(null)
const currentIndex = ref(0)
const currentItem = computed(() => data[currentIndex.value])

const goHome = () => {
  currentPage.value = 'home'
}

const goOrganisms = () => {
  currentPage.value = 'organisms'
}

const goMap = () => {
  currentPage.value = 'map'
}

const goLearn = (item) => {
  currentIndex.value = data.findIndex(organism => organism.id === item.id)
  currentPage.value = 'learn'
}

const goSiteDetails = (site) => {
  selectedSite.value = site
  currentPage.value = 'site-detail'
}

const prevItem = () => {
  currentIndex.value = (currentIndex.value - 1 + data.length) % data.length
}

const nextItem = () => {
  currentIndex.value = (currentIndex.value + 1) % data.length
}

</script>