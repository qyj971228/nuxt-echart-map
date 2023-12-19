<template>
  <div class="echarts-box">
    <div id="chart_country"></div>
  </div>
</template>

<script setup>
import * as echarts from 'echarts'
import chinaJson from '@/assets/json/china.json'
import populationJson from '@/assets/json/population.json'

const emits = defineEmits(['handle-click'])

const echart = echarts
const colors = [
  'rgba(255, 255, 191)',
  'rgba(254, 238, 165)',
  'rgba(254, 218, 139)',
  'rgba(253, 191, 113)',
  'rgba(251, 160, 90)',
  'rgba(246, 123, 74)',
  'rgba(234, 89, 58)',
  'rgba(218, 55, 42)',
  'rgba(193, 27, 39)',
  'rgba(165, 0, 38)'
]
const computeColor = (num) => {
  const n = Number(num) / 1000
  const color = colors[Math.floor(n)] ?? colors[colors.length - 1]
  return color
}
const regions = populationJson.data.map((el) => ({
  name: el.name,
  itemStyle: {
    areaColor: computeColor(el.count),
    borderColor: '#000'
  }
}))
const options = {
  geo: {
    map: 'china',
    regions: [...regions]
  },
  visualMap: {
    type: 'piecewise',
    splitNumber: 10,
    min: 0,
    max: 10000,
    selectedMode: false,
    inRange: {
      color: [...colors]
    }
  },
  // 背景颜色
  backgroundColor: {
    type: 'linear',
    x: 0,
    y: 0,
    x2: 0,
    y2: 1,
    colorStops: [
      {
        offset: 0,
        color: '#2980b9'
      },
      {
        offset: 1,
        color: 'rgba(44, 80, 77, 0)'
      }
    ]
  }
}

function chartClick(params) {
  console.log(params.name)
  emits('handle-click')
}

onMounted(() => {
  initChart()
})

onUnmounted(() => {
  echart.dispose()
})

function initChart() {
  echart.registerMap('china', { geoJSON: chinaJson })
  const chart = echart.init(document.getElementById('chart_country'))
  chart.setOption(options)
  chart.on('click', chartClick)
}
</script>

<style scoped>
#chart_country {
  width: 100vw;
  height: 100vh;
}
</style>
