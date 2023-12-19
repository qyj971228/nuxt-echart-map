<template>
  <div class="echarts-box">
    <div id="chart_province"></div>
  </div>
</template>

<script setup>
import * as echarts from 'echarts'
import neimengguJson from '@/assets/json/neimenggu.json'

const emits = defineEmits(['handle-click'])

const echart = echarts

onMounted(() => {
  initChart()
})

onUnmounted(() => {
  echart.dispose()
})

function initChart() {
  echart.registerMap('neimenggu', { geoJSON: neimengguJson })
  const chart = echart.init(document.getElementById('chart_province'))
  chart.setOption({
    geo: [
      {
        map: 'neimenggu'
      }
    ]
  })
  chart.on('click', (params) => {
    console.log(params.name)
    emits('handle-click')
  })
}
</script>

<style scoped>
#chart_province {
  width: 100vw;
  height: 100vh;
}
</style>
