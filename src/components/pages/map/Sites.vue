<template>
    <div class="header">
        <img :src="banner" alt="bannerLogo" />
        <h2 class="overlay-text">Nearby Sites</h2>
    </div>

    <div class="back-to-map">
        <button type="button" @click="goMap">Back to Map</button>
    </div>

    <div class="sites-grid">
        <div v-for="site in sites" :key="site.id" class="site-card">
            <button type="button" class="image-button" @click="goSiteDetails(site)">
                <img :src="site.image" :alt="site.name" />
            </button>
            <button type="button" class="detail-button" @click="goSiteDetails(site)">{{ site.name }} details</button>
        </div>
    </div>

</template>

<script setup>
import banner from '../../../assets/Banner.png'


defineProps({
    goMap: Function,
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
    color: white;
    font-size: 2rem;
    font-weight: bold;
}

.back-to-map {
    display: flex;
    justify-content: center;
    margin-top: 170px;
    margin-bottom: 20px;
    position: relative;
    z-index: 2;
}

.back-to-map button {
    border: none;
    background-color: rgba(48, 132, 41, 1);
    color: white;
    padding: 0.5rem 1.4rem;
    font-size: 1rem;
    cursor: pointer;
    position: relative;
    z-index: 3;
}

.sites-grid {
    margin-top: 0;
    display: grid;
    grid-template-columns: repeat(2, minmax(240px, 1fr));
    gap: 30px 80px;
    max-width: 900px;
    margin-left: auto;
    margin-right: auto;
}

.site-card {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.image-button {
    margin-top: 0;
    padding: 0;
    border: none;
    background: transparent;
    cursor: pointer;
}

.site-card img {
    width: 100%;
    max-width: 360px;
    height: 220px;
    object-fit: cover;
    border-radius: 12px;
}

.detail-button {
    margin-top: 12px;
    font-size: 1.2rem;
    border: none;
    border-radius: 999px;
    background-color: rgba(48, 132, 41, 1);
    color: white;
    padding: 0.6rem 1.4rem;
    cursor: pointer;
}

</style>