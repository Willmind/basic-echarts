<template>
  <div class='echart' ref="chartDom"></div>
</template>

<script setup>

import { onMounted, ref, watch } from "vue";
import * as echarts from "echarts";

const myChart = ref(null);
const chartDom = ref(null);

const props = defineProps({
  options: {
    type: Object,
    default: {},
    required: true
  }
});
const resizeHandler = () => {
  myChart.resize();
};
watch(() => props.options, (newOptions) => {
  myChart.value.setOption(newOptions);
}, {
  deep: true
});

onMounted(() => {
  myChart.value = echarts.init(chartDom.value);
  myChart.value.setOption(props.options, true);
  window.addEventListener("resize", () => {
    myChart.resize();
  });
});
</script>

<style scoped>
.echart {
  width: 800px;
  height: 500px;
}

</style>
