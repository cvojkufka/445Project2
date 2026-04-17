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

    <div class="map-layout">
        <div class="map-image-wrapper">
            <img :src="map" :style="mapImageStyle" alt="Map">
        </div>

        <div class="zoom-actions" v-if="activeSiteId">
            <button type="button" @click="resetZoom">Reset zoom</button>
        </div>

        <div class="sites-panel">
            <h3>All Sites</h3>

            <div class="sites-grid">
                <div v-for="site in sites" :key="site.id" class="site-card">
                    <button
                        type="button"
                        class="image-button"
                        :class="{ active: activeSiteId === site.id }"
                        @click="focusOnSite(site)"
                    >
                        <img :src="site.image" :alt="site.name" />
                    </button>
                    <button type="button" class="detail-button" @click="goSiteDetails(site)">
                        {{ site.name }} details
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import banner from '../../../assets/Banner.png'
import home from '../../../assets/Home.png'
import map from '../../../assets/ConnorPraireMap.png'
import site1 from '../../../assets/NW.jpeg'
import site2 from '../../../assets/NE.jpeg'
import site3 from '../../../assets/SW.jpeg'
import site4 from '../../../assets/SE.jpeg'

const sites = [
    {
        id: 1,
        name: 'Northwest Corner',
        image: site1,
        focusX: 26,
        focusY: 33,
        accessibility: ['Wheelchair-friendly path', 'Accessible parking'],
        amenities: ['Benches', 'Water fountain', 'Restroom nearby'],
        nearbySites: ['William Conner House', 'Lenape Camp', 'Prairietown'],
    },
    {
        id: 2,
        name: 'Northeast Corner',
        image: site2,
        focusX: 64,
        focusY: 34,
        accessibility: ['Flat trail entry', 'Handrail support points'],
        amenities: ['Picnic tables', 'Shade area'],
    },
    {
        id: 3,
        name: 'Southwest Corner',
        image: site3,
        focusX: 31,
        focusY: 67,
        accessibility: ['Low-slope approach', 'Wide viewing space'],
        amenities: ['Bike rack', 'Information sign'],
        nearbySites: ['Promised Land as Proving Ground', 'Muesuem Experience Center', '1859 Balloon Voyage', 'Animal Encounter'],
    },
    {
        id: 4,
        name: 'Southeast Corner',
        image: site4,
        focusX: 70,
        focusY: 68,
        accessibility: ['Step-free route', 'Accessible drop-off zone'],
        amenities: ['Rest area', 'Trail map kiosk', 'Parking'],
    },
]

const activeSiteId = ref(null)
const mapFocus = ref({ x: 50, y: 50 })

const mapImageStyle = computed(() => ({
    transform: activeSiteId.value ? 'scale(2.2)' : 'scale(1)',
    transformOrigin: `${mapFocus.value.x}% ${mapFocus.value.y}%`,
}))

const focusOnSite = (site) => {
    activeSiteId.value = site.id
    mapFocus.value = {
        x: site.focusX,
        y: site.focusY,
    }
}

const resetZoom = () => {
    activeSiteId.value = null
    mapFocus.value = { x: 50, y: 50 }
}

defineProps({
  goHome: Function,
  goSiteDetails: Function,
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
    align-items: flex-start;
    width: min(90vw, 850px);
    overflow: hidden;
    border-radius: 14px;
}

.map-image-wrapper img {
    width: 100%;
    height: auto;
    display: block;
    transition: transform 0.45s ease;
}

.map-layout {
    margin-top: 220px;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: 40px;
    padding: 0 30px 30px;
}

.zoom-actions {
    position: absolute;
    top: 190px;
    left: 50%;
    transform: translateX(-50%);
}

.zoom-actions button {
    border: none;
    border-radius: 999px;
    padding: 0.45rem 1rem;
    cursor: pointer;
    background: #ffffff;
}

.sites-panel {
    width: min(42vw, 520px);
    border-radius: 16px;
    padding: 18px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
}

.sites-panel h3 {
    margin: 0 0 16px;
    text-align: center;
    font-size: 1.5rem;
}

.sites-grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(160px, 1fr));
    gap: 18px;
}

.site-card {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.image-button {
    padding: 0;
    border: none;
    background: transparent;
    cursor: pointer;
    border-radius: 12px;
}

.image-button.active {
    outline: 3px solid rgba(48, 132, 41, 1);
}

.site-card img {
    width: 100%;
    max-width: 220px;
    height: 150px;
    object-fit: cover;
    border-radius: 12px;
}

.detail-button {
    margin-top: 10px;
    font-size: 1rem;
    border: none;
    background-color: rgba(48, 132, 41, 1);
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 999px;
    cursor: pointer;
}

</style>