<template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <SiteNavigationVue />
    <RouterView />
  </div>
</template>
<script setup>
import SiteNavigationVue from "./components/SiteNavigation.vue";
</script>
<style lang="scss"></style>
