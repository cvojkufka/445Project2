<template>
    <div>
    <h1>Learn Page</h1>
    <p>This is where learn content will go.</p>
    <button @click="goHome">Back to Home</button>
  </div>
</template>

<script setup>
    defineProps ({
        goHome: Function
    })
</script>