<template>
  <div class="echarts-box">
    <div id="geo3D"></div>
  </div>
</template>

<script setup>
import * as echarts from 'echarts'
import chinaJson from '@/assets/json/china.json'

const echart = echarts

onMounted(() => {
  initChart()
})

onUnmounted(() => {
  echart.dispose()
})

function initChart() {
  echart.registerMap('china', { geoJSON: chinaJson })
  const chart = echart.init(document.getElementById('geo3D'))
  const option = {
    tooltip: {},
    geo3D: {
      map: 'china',
      roam: true, // 是否开启鼠标缩放和平移漫游
      itemStyle: {
        color: '#1a8cff', // 地图颜色
        opacity: 0.7,
        borderWidth: 1,
        borderColor: 'rgba(255,255,255,0.8)'
      },
      label: {
        show: true,
        textStyle: {
          color: '#000', // 标签颜色
          fontSize: 10
        }
      },
      shading: 'color', // 着色方式，'color' 或 'lambert'
      light: {
        main: {
          intensity: 1.2,
          shadow: true
        },
        ambient: {
          intensity: 0.2
        }
      }
    },
    series: []
  }
  chart.setOption(option)
}
</script>

<style scoped>
#geo3D {
  height: 100vh;
  width: 100vw;
}
</style>
