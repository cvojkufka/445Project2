<template>
  <div>
    <h1>Organisms Page</h1>
    <p>This is where organisms content will go.</p>
    <button @click="goHome">Back to Home</button>
  </div>
</template>

<script setup>
defineProps({
  goHome: Function
})
</script>