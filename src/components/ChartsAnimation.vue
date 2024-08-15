<script lang="ts">
import { defineComponent, ref, onMounted } from 'vue'
import {
  Chart as ChartJS,
  ArcElement,
  Title,
  Tooltip,
  Legend,
  BarElement,
  PointElement,
  CategoryScale,
  LinearScale
} from 'chart.js'
import { Pie, Bar, Bubble } from 'vue-chartjs'

ChartJS.register(
  ArcElement,
  Tooltip,
  Legend,
  CategoryScale,
  LinearScale,
  BarElement,
  PointElement,
  Title,
  Tooltip,
  Legend
)

export default defineComponent({
  name: 'App',
  components: {
    Pie,
    Bar,
    Bubble
  },
  setup() {
    const chart1 = ref(null) // Reference for the first chart
    const chart2 = ref(null) // Reference for the second chart
    const chart3 = ref(null) // Reference for the third chart

    const data1 = {
      labels: ['A', 'B', 'C'],
      datasets: [
        {
          backgroundColor: ['#41B883', '#E46651', '#00D8FF'],
          data: [30, 20, 50]
        }
      ]
    }

    const data2 = {
      labels: ['X', 'Y', 'Z'],
      datasets: [
        {
          backgroundColor: ['#DD1B16', '#4B8F29', '#8E2C2F'],
          data: [20, 40, 40]
        }
      ]
    }

    const data3 = {
      labels: ['X', 'Y', 'Z'],
      datasets: [
        {
          label: 'Data One',
          backgroundColor: '#f87979',
          data: [
            {
              x: 20,
              y: 25,
              r: 5
            },
            {
              x: 40,
              y: 10,
              r: 10
            },
            {
              x: 30,
              y: 22,
              r: 30
            }
          ]
        },
        {
          label: 'Data Two',
          backgroundColor: '#7C8CF8',
          data: [
            {
              x: 10,
              y: 30,
              r: 15
            },
            {
              x: 20,
              y: 20,
              r: 10
            },
            {
              x: 15,
              y: 8,
              r: 30
            }
          ]
        }
      ]
    }

    const options = {
      responsive: true,
      maintainAspectRatio: false,
      animation: {
        duration: 1000 // Disable initial animation
      }
    }

    const startAnimation = () => {
      const chartInstance1 = chart1.value?.$data?.chart
      const chartInstance2 = chart2.value?.$data?.chart
      const chartInstance3 = chart3.value?.$data?.chart
      if (chartInstance1) {
        chartInstance1.options.animation.duration = 1000
        chartInstance1.update()

        setTimeout(() => {
          if (chartInstance2) {
            chartInstance2.options.animation.duration = 1000
            chartInstance2.update()

            setTimeout(() => {
              if (chartInstance3) {
                chartInstance3.options.animation.duration = 1000
                chartInstance3.update()
              }
            }, 1000)
          }
        }, 1000)
      }
    }

    onMounted(() => {
      startAnimation()
    })

    return {
      data1,
      data2,
      data3,
      options,
      chart1,
      chart2,
      chart3
    }
  }
})
</script>

<template>
  <div>
    <Bar :data="data1" :options="options" ref="chart1" />
  </div>
  <div>
    <Pie :data="data2" :options="options" ref="chart2" />
  </div>
  <div>
    <Bubble :data="data3" :options="options" ref="chart3" />
  </div>
</template>
