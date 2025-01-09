<template>
  <div>
    <h1>Sample Chart</h1>
    <div style="width: 100%; height: 500px;">
      <VChart :option="option" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { time } from 'echarts';

const { data } = await useAsyncData('chart-data', () => $fetch('/api/issues-data'));
// const chartType = ref('bar');

// const handleChartTypeChange = () => {
//   // if (option.value) {
//   //   option.value.series = [{ type: chartType.value as any}]
//   // }
// };
useHead({
  title: 'Sample Chart',
});

const option = ref<ECOption>({
  xAxis: { type: 'category',
    data: data.value?.map((item: any) => new Date(item.BUCKET_DT_FROM).getTime()) ?? [],
    axisTick: {
        alignWithLabel: true
      },
    axisLabel: {
        formatter: (value: string) => {
          return formatDate(value, '{MMM}\n{yy}');

        },
        interval: 0
    }, },
  yAxis: [
    { type: 'value', position: 'left', alignTicks: true, },
    { type: 'value', position: 'left', alignTicks: true, },
    { type: 'value', position: 'right', alignTicks: true, }
  ],
  series: [
    { type: 'bar', name: 'Issues Opened', data: data.value?.map((item: any) => item.ISSUES_OPENED ?? 0) ?? [], yAxisIndex: 1,},
    { type: 'bar', name: 'Issues Closed', data: data.value?.map((item: any) => item.ISSUES_CLOSED ?? 0) ?? [], yAxisIndex: 1,},
    { type: 'line', name: 'Cumulative Issues', data: data.value?.map((item: any) => item.CUMULATIVE_ISSUES ?? 0) ?? [], yAxisIndex: 2,},
  ],
  legend: {
    data: ['ISSUES_OPENED', 'ISSUES_CLOSED', 'CUMULATIVE_ISSUES'],
    orient: 'vertical',
    left: 'left',
  },
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      type: 'cross'
    },
    formatter: (params: any) => {
      return `${formatDate(params[0].axisValue, '{MMM} {yyyy}')}<br>
        ${params[0].seriesName}: ${params[0].value} <br>
        ${params[1].seriesName}: ${params[1].value} <br>
        ${params[2].seriesName}: ${params[2].value} `;
    }
  },
})

const formatDate = (value: string, format: string) => {
  return time.format(new Date(parseInt(value)), format, false);
}
</script>
