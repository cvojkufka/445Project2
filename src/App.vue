
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
    :goSites="goSites"
  />

   <Learn 
   v-else-if="currentPage === 'learn'"
   :item="selectedItem"
   :goHome="goHome"
   />

   <Sites
    v-else-if="currentPage === 'sites'"
   :goMap="goMap"
    :goSiteDetails="goSiteDetails"
    />

    <SiteDetail
    v-else-if="currentPage === 'site-detail'"
    :site="selectedSite"
    :goSites="goSites"
   />

</template>

<script setup>
import { ref } from 'vue'
import Home from './components/Home.vue'
import Organisms from './components/pages/organism/Organisms.vue'
import Learn from './components/pages/organism/Learn.vue'
import Map from './components/pages/map/Map.vue'
import Sites from './components/pages/map/Sites.vue'
import SiteDetail from './components/pages/map/SiteDetail.vue'

const currentPage = ref('home')
const selectedItem = ref(null)
const selectedSite = ref(null)

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
  selectedItem.value = item
  currentPage.value = 'learn'
}

const goSites = () => {
  currentPage.value = 'sites'
}

const goSiteDetails = (site) => {
  selectedSite.value = site
  currentPage.value = 'site-detail'
}

</script>