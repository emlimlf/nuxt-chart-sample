<script setup lang="ts">
import { useHead } from '#imports';

useHead({
  title: 'Nuxt App',
});
</script>

<template>
  <div>
    <Header />
    <slot />
  </div>
</template>
