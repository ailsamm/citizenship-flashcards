<script setup lang="ts">
import { RouterView } from 'vue-router'
</script>

<template>
  <header></header>

  <div class="wrapper">
    <RouterView />
  </div>


</template>

<style scoped>
#app {
  height: 100%;
}
.wrapper {
  width: 100%;
  height: 100%;
}
</style>
