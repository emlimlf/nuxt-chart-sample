<template>
  <div>
    <h1>Sample Chart</h1>
    <div class="flex flex-row items-center justify-center gap-4">
      <span>
        <input type="radio" name="chart-type" value="bar" v-model="chartType" @change="handleChartTypeChange" /> Bar
      </span>
      <span>
        <input type="radio" name="chart-type" value="line" v-model="chartType" @change="handleChartTypeChange" /> Line
      </span>
      <span>
        <input type="radio" name="chart-type" value="pie" v-model="chartType" @change="handleChartTypeChange" /> Pie
      </span>
    </div>
    <div style="width: 100%; height: 500px;">
      <VChart :option="option" />
    </div>
  </div>
</template>

<script setup lang="ts">
const { data } = await useAsyncData('chart-data', () => $fetch('/api/chart-data'));
const chartType = ref('bar');

const handleChartTypeChange = () => {
  if (option.value) {
    option.value.series = [{ type: chartType.value as any}]
  }
};
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
  series: [{ type: chartType.value as any}],
})

</script>
