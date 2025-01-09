<template>
  <header class="flex flex-row items-center justify-between p-4">
    <h1>Nuxt.js ECharts Demo</h1>
    <div class="flex flex-row items-center justify-center gap-4">
      <NuxtLink to="/" class="text-blue-500 hover:text-blue-700" :class="{ 'text-blue-700': route.path === '/' }">Issues Chart</NuxtLink>
      <NuxtLink to="/map-chart" class="text-blue-500 hover:text-blue-700" :class="{ 'text-blue-700': route.path === '/map-chart' }">Map Chart</NuxtLink>
    </div>
  </header>
</template>

<script setup lang="ts">
const route = useRoute();
</script>
