<template>
    <div class="page">
        <div class="header">
            <img :src="banner" alt="bannerLogo" />
            <h2 class="title-overlay">Park Information</h2>

            <div class="back">
                <button @click="goHome">
                    <img :src="back" :alt="back">
                    <div class="backbutton-overlay">Back</div>
                </button>
            </div>
        </div>

        <div class="main-layout">
            <div class="map-section">
                <div class="map-layout">
                    <div class="map-canvas" :style="mapImageStyle">
                        <img :src="map" alt="Map">

                        <button
                            v-if="activeSite"
                            type="button"
                            class="site-marker"
                            :style="markerStyle"
                            @click="goSiteDetails(activeSite)"
                        >
                            <i class="fa fa-map-marker" aria-hidden="true" />
                            <span class="marker-label">{{ activeSite.name }}</span>
                        </button>
                    </div>
                </div>

                <div class="zoom-actions" v-if="activeSiteId">
                    <button @click="resetZoom">Reset Zoom</button>
                </div>
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
        <footer class="footer">
            <h3>Made by:</h3>
            <h4>Christopher, Saa, Matteo, Yahaya</h4>
            <p>© 2026 Conner Prairie</p>
        </footer>
    </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import banner from '../../../assets/Banner.png'
import back from '../../../assets/LeftArrow.png'
import map from '../../../assets/ConnorPraireMap.png'
import site1 from '../../../assets/TreetopOutpost.jpg'
import site2 from '../../../assets/RedBridge.jpg'
import site3 from '../../../assets/Prairietown.jpg'
import site4 from '../../../assets/PromisedLand.webp'
import site5 from '../../../assets/WilliamConnerHouse.jpg'
import site6 from '../../../assets/Trails.webp'
import site7 from '../../../assets/LenapeCamp.webp'
import site8 from '../../../assets/Animals.jpg'
import site9 from '../../../assets/BalloonRides.webp'
import site10 from '../../../assets/Museum.webp'


const sites = [
{
    id: 1,
    name: 'Treetop Outpost',
    image: site1,
    focusX: 7,
    focusY: 37,
    type: 'attraction',
    accessibility: ['Paved path access', 'Partial wheelchair access (varies by activity)'],
    amenities: ['Benches', 'Water fountain', 'Restroom nearby'],
    includes: ['27. Nature Amphitheater', '28. River Lookout', '29. Treehouse', '30. Fort Hoosier', '31. Prairie Overlook'],
    nearbySites: ['Prairietown','The Junction'],
},
{
    id: 2,
    name: 'The Junction',
    image: site2,
    focusX: 8,
    focusY: 56,
    type: 'facility',
    accessibility: ['Flat central hub', 'Wide walking paths'],
    amenities: ['Picnic tables', 'Shade structures', 'Directional signage'],
    includes: ['32. River Crossing - Open Seasonally', '33. Discovery Station'],
    nearbySites: ['Treetop Outpost', 'Prairietown', 'Promised Land as Proving Ground'],
},
{
    id: 3,
    name: 'Prairietown Est. 1836',
    image: site3,
    focusX: 25,
    focusY: 49,
    type: 'historical',
    accessibility: ['Wheelchair accessible paths', 'Open walking space'],
    amenities: ['Food vendors', 'Restrooms', 'Seating areas'],
    includes: ['13. Blacksmith Shop', "14. Curtis' Home", "15. Whitaker's Store", '16. Schoolhouse', "17. Dr. Campbell's Office & Home", '18. Turners home', "19. McClure's Home", '20. Carpenter Shop', "21. Baker Brother's Pottery Shop", '22. Golden Eagle Inn'],
    nearbySites: ['Treetop Outpost', 'The Junction', 'Animal Encounters','Promised Land as Proving Ground',  'William Conner House'],
},
{
    id: 4,
    name: 'Promised Land as Proving Ground',
    image: site4,
    focusX: 24,
    focusY: 71,
    type: 'historical',
    accessibility: ['Mostly flat terrain', 'Grass + gravel paths'],
    amenities: ['Interpretive signage', 'Open space'],
    includes: ['23. Origins Cabin', '24. Resistance Cabin', '25. Reclamation Building', '26. Reflections Cabin'],
    nearbySites: ['The Junction', 'Prairietown', 'Animal Encounters', '1859 Balloon Voyage', 'Museum Experience Center'],
},
{
    id: 5,
    name: 'William Conner House',
    image: site5,
    focusX: 35,
    focusY: 41,
    type: 'historical',
    accessibility: ['Limited wheelchair access (historic building)', 'Ramp access in select areas'],
    amenities: ['Guided tours', 'River views', 'Historic exhibits'],
    includes: ['9. William Conner House (1st Floor Accessible)', '10. Spring House', '11. Loom House', '12. Heirloom Garden'],
    nearbySites: ['Prairietown', 'Animal Encounters', 'Trails at Conner Prairie', 'Lenape Camp'],
},
{
    id: 6,
    name: 'Trails at Conner Prairie',
    image: site6,
    focusX: 49,
    focusY: 25,
    type: 'nature',
    accessibility: ['Natural surface trails', 'Not fully wheelchair accessible'],
    amenities: ['Nature trails', 'Scenic overlooks'],
    includes: ['34. R.B Annis Vista Trail (Rugged)', '35. Prairie Trail (Paved)'],
    nearbySites: ['Lenape Camp', 'William Conner House'],
},
{
    id: 7,
    name: 'Lenape Camp',
    image: site7,
    focusX: 48,
    focusY: 41,
    type: 'historical',
    accessibility: ['Grass paths', 'Some uneven terrain'],
    amenities: ['Interactive exhibits', 'Educational signage'],
    includes: ['5. Trading Post', '6. Bark House', '7. Lifeways Cabin'],
    nearbySites: ['Trails at Conner Prairie', 'William Conner House', 'Animal Encounters', '1859 Balloon Voyage'],
},
{
    id: 8,
    name: 'Animal Encounters',
    image: site8,
    focusX: 39,
    focusY: 58,
    type: 'attraction',
    accessibility: ['Wide dirt paths', 'Generally wheelchair accessible'],
    amenities: ['Animal viewing areas', 'Handwashing stations'],
    includes: ['8. Animal Encounters'],
    nearbySites: ['1859 Balloon Voyage', 'Promised Land as Proving Ground', 'Museum Experience Center'],
},
{
    id: 9,
    name: '1859 Balloon Voyage',
    image: site9,
    focusX: 45,
    focusY: 60,
    type: 'attraction',
    accessibility: ['Paved access to viewing area', 'Limited ride accessibility'],
    amenities: ['Viewing area', 'Open field space'],
    includes: ['1. Balloon Kiosk', '2. 1859 Balloon Voyage Exhibit', '3. Cafe of the Common', '4. 1859 Balloon Voyage Ride'],
    nearbySites: ['Museum Experience Center', 'Animal Encounters', 'William Conner House', 'Lenape Camp'],
},
{
    id: 10,
    name: 'Museum Experience Center',
    image: site10,
    focusX: 47,
    focusY: 77,
    type: 'facility',
    accessibility: ['Fully wheelchair accessible', 'Elevator access'],
    amenities: ['Restrooms', 'Gift shop', 'Indoor exhibits'],
    includes: [],
    nearbySites: ['Promised Land as Proving Ground', 'Animal Encounters', '1859 Balloon Voyage'],
}
]

const activeSiteId = ref(null)
const zoomScale = 2.2

const activeSite = computed(() => sites.find((site) => site.id === activeSiteId.value) ?? null)

const clamp = (value, min, max) => Math.min(max, Math.max(min, value))

const mapImageStyle = computed(() => {
    if (!activeSite.value) {
        return {
            transform: 'translate(0%, 0%) scale(1)',
        }
    }

    const tx = clamp(50 - (activeSite.value.focusX * zoomScale), (1 - zoomScale) * 100, 0)
    const ty = clamp(50 - (activeSite.value.focusY * zoomScale), (1 - zoomScale) * 100, 0)

    return {
        transform: `translate(${tx}%, ${ty}%) scale(${zoomScale})`,
    }
})

const markerStyle = computed(() => {
    if (!activeSite.value) {
        return {}
    }

    return {
        left: `${activeSite.value.focusX}%`,
        top: `${activeSite.value.focusY}%`,
    }
})

const focusOnSite = (site) => {
    activeSiteId.value = site.id
}

const resetZoom = () => {
    activeSiteId.value = null
}

defineProps({
  goHome: Function,
  goSiteDetails: Function,
})
</script>


<style scoped>
@font-face {
    font-family: 'Marker';
    src: url('../../../fonts/PermanentMarker-Regular.ttf') format('truetype');
}
.page {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

/* HEADER */
.header {
    position: relative;
    top: 0;
    left: 0;
    width: 100%;
    background-color: #357A46;

    display: flex;
    justify-content: center;
    padding-bottom: 30px;
    margin-bottom: 15px;
}

.header img {
    width: 600px;
    display: block;
}

.header::after {
    content: "";
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 18%;

    background-image: url('../../../assets/Plank.png');
    background-size: contain;
    background-repeat: repeat-x;

    pointer-events: none;
}

.title-overlay {
    position: absolute;
    top: 15%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: rgb(255, 255, 255);
    font-size: 2rem;
    font-weight: bold;
}

/* backbutton */
.backbutton-overlay {
    position: absolute;
    top: 25%;
    left: 55%;
    transform: translate(-50%, -50%);
    color: orange;
    font-family: 'Marker';
    font-size: 2rem;
    font-weight: bold;
    text-shadow:
        -1px -1px 0 black,
         1px -1px 0 black,
        -1px  1px 0 black,
         1px  1px 0 black;
}

.back {
    position: absolute;
    top: 40px;
    left: 40px;
    background: none;
}

.back button {
    all: unset;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;

    width: 100%;
    height: 100%;
}

.backbutton-overlay:hover {
    text-shadow: 0 0 3px yellow;
    font-size: 35px;
}

.back img {
    width: 100px;
    height: 100px;
}

/* BODY */
.main-layout {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: 40px;
    padding: 0px 30px 30px 0x;
    overflow: hidden;
    flex: 1;
}

/* zoom button */
.zoom-actions button {
    width: 140px;
    height: 40px;
    font-size: 16px;
    background-color: #8B4E2E;
    color: white;
    border-radius: 99px;
    cursor: pointer;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border: 1px solid;
    border-color: #FFC300;
}

.zoom-actions button:hover {
    background-color: #5A3218;
    box-shadow: 0 6px 14px rgba(0, 0, 0, 0.25);
}

/* map */
.map-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
}

.map-layout {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    
    overflow: hidden;
    border-radius: 15px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border: 5px solid;
    border-color: #FFC300;
    gap: 10px;
}

.map-canvas {
    position: relative;
    width: 100%;
    transition: transform 0.45s ease;
    transform-origin: top left;
}

.map-layout img {
    width: 100%;
    min-height: 55vh;
    max-height: 55vh;
    display: block;
}

.site-marker {
    position: absolute;
    transform: translate(-50%, -100%);
    background: transparent;
    border: none;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 6px;
}

.site-marker .fa-map-marker {
    color: #ff0000;
    font-size: 20px;
    line-height: 1;
    text-shadow: 0 0 5px rgba(255, 255, 255, 0.9);
}

.marker-label {
    background-color: rgba(0, 0, 0, 0.75);
    color: white;
    font-size: 12px;
    padding: 4px 8px;
    border-radius: 999px;
    white-space: nowrap;
}

/* right bar */
.sites-panel {
    min-width: 415px;
    max-width: 415px;
    height: 100%;
    overflow-y: auto;
    border-radius: 15px;
    padding: 18px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border: 5px solid;
    border-color: #FFC300;
    background-color: rgba(48, 132, 41, 1);
    max-height: 56.1vh;
}

.sites-panel h3 {
    margin: 8px 0px 15px;
    text-align: center;
    font-size: 1.5rem;
    background-color: #8B4E2E;
    border-radius: 9px;
    box-shadow: 0 0 15px rgba(48, 132, 41, 0.99);
    border: 3.5px solid;
    border-color: #FFC300;
    padding: 3px;
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
    font-size: 16px;
    background-color: #8B4E2E;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 99px;
    cursor: pointer;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border: 1px solid;
    border-color: #FFC300;
}

.detail-button:hover {
    background-color: #5A3218;
    box-shadow: 0 6px 14px rgba(0, 0, 0, 0.25);
}

/* FOOTER */
.footer {
    background-color: #8B4E2E;
    padding: 0px 0px 0px 15px;
    text-align: left;
    height: 80px;
    display: flex;
    flex-direction: column;
    line-height: 0.1;
    margin-top: 15px;
}

.footer h3 {
    font-size: 20px;
    margin-bottom: 0px;
    color: #5c2f1a;
}
.footer h4 {
    font-size: 14px;
    margin-bottom: 3px;
    color: hsl(29, 66%, 46%);
}
.footer p {
    margin-bottom: 10px;
}
</style>