<template>
  <div>
    <h1>Sample Chart</h1>
    <div style="width: 100%; height: 500px;">
      <VChart :option="option" />
    </div>
  </div>
</template>

<script setup lang="ts">
const { data } = await useAsyncData('chart-data', () => $fetch('/api/chart-data'));

console.log(data.value);

useHead({
  title: 'Sample Chart',
});

const option = ref<ECOption>({
  dataset: {
    dimensions: ['Product', '2015', '2016', '2017'],
    source: data.value as any,
  },
  xAxis: { type: 'category' },
  yAxis: {},
  series: [{ type: 'bar' }],
})

</script>
