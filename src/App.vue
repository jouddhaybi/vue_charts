<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import ChartsAnimation from './components/ChartsAnimation.vue'
</script>

<template>
  <div class="charts_holder">
    <ChartsAnimation />
  </div>
</template>

<style scoped>
.charts_holder {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
</style>
