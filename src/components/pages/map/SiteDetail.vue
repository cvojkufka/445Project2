<template>
    <div class="header">
        <img :src="banner" alt="bannerLogo" />
        <h2 class="overlay-text">{{ site?.name || 'site' }}</h2>
    </div>

    <div class="back-row">
        <button type="button" @click="goSites">Back to Nearby Sites</button>
    </div>

    <div v-if="site" class="content">
        <div class="left-image">
            <img :src="site.image" :alt="site.name" />
        </div>

        <div class="right-details">
            <div class="detail-group">
                <div class="detail-title">
                    <img :src="accessibilityIcon" alt="Accessibility icon" />
                    <h3>Accessibility</h3>
                </div>
                <ul>
                    <li v-for="item in site.accessibility" :key="`access-${item}`">{{ item }}</li>
                </ul>
            </div>

            <div class="detail-group">
                <div class="detail-title">
                    <img :src="amenitiesIcon" alt="Amenities icon" />
                    <h3>Amenities</h3>
                </div>
                <ul>
                    <li v-for="item in site.amenities" :key="`amenity-${item}`">{{ item }}</li>
                </ul>
            </div>

            <div class="detail-group">
                <div class="detail-title">
                    <img :src="nearbyIcon" alt="Nearby sites icon" />
                    <h3>Nearby Sites</h3>
                </div>
                <ul>
                    <li v-for="item in site.nearbySites" :key="`near-${item}`">{{ item }}</li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script setup>
import banner from '../../../assets/Banner.png'
import accessibilityIcon from '../../../assets/accessibility.jpg'
import amenitiesIcon from '../../../assets/amenities.webp'
import nearbyIcon from '../../../assets/nearby.png'

defineProps({
    site: Object,
    goSites: Function,
})
</script>

<style scoped>
.header {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: min(70vw, 650px);
    pointer-events: none;
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
    text-transform: capitalize;
}

.back-row {
    display: flex;
    justify-content: center;
    margin-top: 170px;
    margin-bottom: 20px;
    position: relative;
    z-index: 2;
}

.back-row button {
    border: none;
    border-radius: 999px;
    background-color: rgba(48, 132, 41, 1);
    color: white;
    padding: 0.5rem 1.4rem;
    font-size: 1rem;
    cursor: pointer;
    position: relative;
    z-index: 3;
}

.content {
    max-width: 1000px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 30px;
    align-items: start;
}

.left-image img {
    width: 100%;
    max-width: 460px;
    height: auto;
    object-fit: cover;
    border-radius: 12px;
}

.right-details {
    border-radius: 12px;
    padding: 16px 20px;
}

.right-details h3 {
    margin: 0 0 8px;
}

.detail-group {
    margin-bottom: 18px;
}

.detail-title {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 8px;
}

.detail-title img {
    width: 34px;
    height: 34px;
    object-fit: contain;
    flex-shrink: 0;
}

.detail-title h3 {
    margin: 0;
}

.right-details ul {
    margin: 0 0 16px;
    padding-left: 20px;
}
</style>
