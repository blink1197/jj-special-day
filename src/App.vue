<script setup>
import HomeView from './views/HomeView.vue';
</script>

<template>
  <div class="mobile-wrapper">
    <HomeView />
  </div>
</template>

<style scoped>
.mobile-wrapper {
  max-width: 480px;
  margin: 0 auto;
  background: #fff;
  min-height: 100vh;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
}
</style>
