<template>
    <div class="page">
        <div class="header">
            <img :src="banner" alt="bannerLogo" />
            <h2 class="overlay-text">{{ site?.name || 'site' }}</h2>

            <div class="back">
                <button @click="goMap">
                    <img :src="back" :alt="back">
                    <div class="backbutton-overlay">Back</div>
                </button>
            </div>
        </div>

        <div class="main-layout">
            <div class="left-image">
                <img :src="site.image" :alt="site.name" />
            </div>

            <div class="right-details">
                <div class="detail-group">
                    <div class="detail-title">
                        <img :src="typeIcon" alt="Type of place icon" />
                        <h3>Type</h3>
                    </div>

                    <p class = "type-text">
                        <p>{{ site.type }}</p>
                    </p>
                </div>

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
                        <img :src="nearbyIcon" alt="Nearby areas icon" />
                        <h3>Nearby Areas</h3>
                    </div>
                    <ul>
                        <li v-for="item in site.nearbySites" :key="`near-${item}`">{{ item }}</li>
                    </ul>
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
import banner from '../../../assets/Banner.png'
import accessibilityIcon from '../../../assets/accessibility.jpg'
import amenitiesIcon from '../../../assets/amenities.webp'
import nearbyIcon from '../../../assets/nearby.png'
import typeIcon from '../../../assets/type.png'
import back from '../../../assets/LeftArrow.png'

defineProps({
    site: Object,
    goMap: Function,
})
</script>

<style scoped>
.page {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
}

.main-layout {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    gap: 40px;
    padding: 0px 30px 30px 0x;
    overflow: hidden;
    flex: 1;
}

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

.overlay-text {
    position: absolute;
    top: 15%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: rgb(255, 255, 255);
    font-size: 2rem;
    font-weight: bold;
}



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

/*left side*/
.left-image img {
    width: 700px;
    max-width: 700px;

    max-height: 450px;
    min-height: 450px;
    object-fit: cover;

    overflow: hidden;
    border-radius: 15px;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
    border: 5px solid;
    border-color: #FFC300;
    gap: 10px;
}


/* right side */
.right-details {
    width: 400px;
    min-height: 450px;
    max-height: 450px;
    border-radius: 15px;
    padding: 16px 20px;
    background-color: #8B4E2E;
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);

    border: 5px solid;
    border-color: #FFC300;

    overflow-y: auto;
}

.right-details h3 {
    margin: 0 0 8px;
}

.detail-group {
    background-color: rgba(48, 132, 41, 1);
    border-radius: 15px;
    padding: 6px 2px 10px 15px;
    margin-bottom: 15px;
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
    margin: 0 0 0px;
    padding-left: 20px;
}




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
