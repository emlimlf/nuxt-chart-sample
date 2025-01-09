<template>
  <div>
    <h1>Map Chart</h1>
    <div style="width: 100%; height: 500px;">
      <VChart :option="option" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { registerMap } from 'echarts';

const { data } = await useAsyncData('mag-geo', () => $fetch('/api/map-geo'));
console.log(data.value);

registerMap('world', data.value as any);
const option = ref<ECOption>({
  visualMap: {
    left: 'right',
    min: 500,
    max: 100000,
    inRange: {
      color: [
        '#313695',
        '#4575b4',
        '#74add1',
        '#abd9e9',
        '#e0f3f8',
        '#ffffbf',
        '#fee090',
        '#fdae61',
        '#f46d43',
        '#d73027',
        '#a50026',
      ],
    },
    text: ['High', 'Low'],
    calculable: true,
  },
  series: [
    {
      name: 'USA PopEstimates',
      type: 'map',
      roam: true,
      map: 'world',
        emphasis: {
          label: {
            show: true
          }
        },
        data: [
          { name: 'United States of America', value: 48202 },
          { name: 'China', value: 4823 },
          { name: 'Canada', value: 22023 },
          { name: 'Australia', value: 2023 },
          ]
      }
    ]
})

</script>