<template>
    <img class="background" :src="background" alt="background" />

    <div class="assistant">
      <img class="prairie-dog" :src="prairieDog" />
      <div class="speech-container">
        <img class="speech" :src="speech" alt="bubble" />
        <p class="speech-text">{{ speechText }}</p>
      </div>
    </div>

    <div class="header">
        <img :src="banner" alt="bannerLogo" />
        <h2 class="title">{{ title }}</h2>
    </div>
</template>

<script setup>
import banner from '../../assets/Banner.png'
import prairieDog from '../../assets/Prairie-dog.png'
import background from '../../assets/Tablet Background.png'
import speech from '../../assets/Speech.png'

defineProps({
  title: String,
  speechText: String
})
</script>

<style scoped>
.header { 
  position: absolute;
  top: 0;
  left: 50%;
  transform: translateX(-50%);
  width: fit-content;
}

.header img {
  width: 100%;
}

.background {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  height: auto;
}

.assistant {
  position: fixed;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  z-index: 2;
}

.prairie-dog {
  width: 250px;
  display: block;
}

.speech-container {
  position: absolute;
  bottom: 50px;
  left: 280px;
  width: 300px;
}

.speech {
  width: 100%;
  display: block;
}

.speech-text {
  position: absolute;
  top: 20px;
  left: 20px;
  right: 20px;
  margin: 0;
  text-align: left;
  line-height: 1.2;
  font-size: 14px;
}
</style>