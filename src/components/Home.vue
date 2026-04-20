<template>
  <Overlay 
    title="Welcome!"
    speechText="Hi! Click on one of the signs to get started!"
  />

  <div class="content">
    <button class="left-sign" @click="goOrganisms">
      <div class="sign-wrapper">
        <img :src="sign" alt="sign button" />
        <span class="sign-text">Organisms 10m</span>
      </div>
    </button>

    <button class="right-sign" @click="goMap">
      <div class="sign-wrapper">
        <img :src="sign" alt="sign button" />
        <span class="sign-text">Map 25m</span>
      </div>
    </button>
  </div>
</template>

<script setup>
import Overlay from './overlay/Overlay.vue'
import sign from '../assets/Sign.png'

defineProps ({
  goOrganisms: Function,
  goMap: Function,
})
</script>

<style scoped>
.content {
  position: relative;
  z-index: 5;
  width: 100%;
  height: 100vh;
}

.left-sign,
.right-sign {
  position: absolute;
  top: 35%;
  background: none;
  border: none;
  padding: 0;
  cursor: pointer;
}

.left-sign {
  left: 15%;
}

.right-sign {
  right: 15%;
}

.left-sign img,
.right-sign img {
  width: 420px;
}

.right-sign img {
  transform: scaleX(-1);
}

.sign-wrapper {
  position: relative;
  display: inline-block;
}

.sign-wrapper img {
  width: 420px;
  display: block;
}


.sign-text {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);

  color: white;
  font-size: 22px;
  font-weight: bold;
  text-align: center;

  pointer-events: none;
}
</style>