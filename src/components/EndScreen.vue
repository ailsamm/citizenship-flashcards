<script setup lang="ts">
import Button from './Button.vue';

// ----------------------------------------------------------------
// Emits
// ----------------------------------------------------------------
const emit = defineEmits<{
  (e: 'navigate-home'): void;
}>();

// ----------------------------------------------------------------
// Functionality
// ----------------------------------------------------------------
function navigateHome() {
  emit('navigate-home');
}
</script>

<template>
  <div class="end-screen__container">
    <div class="end-screen__title">
      <h1>All done! Congratulations!</h1>
      <p>🇺🇸🇺🇸🇺🇸</p>
    </div>
    <Button label="Back Home" :on-click="navigateHome" />
  </div>
</template>

<style>
.end-screen__container {
  display: flex;
  flex-direction: column;
  align-items: center;

  position: relative;

  & > .end-screen__title {
    font-size: 1.5rem;
    margin-bottom: 2rem;
    text-align: center;

    & > p {
      font-size: 3rem;
    }
  }
}

.button-comp {
  margin-top: 2rem;
}
</style>
