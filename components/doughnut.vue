<template>
  <Doughnut
    :chart-options="{
      responsive: true,
      maintainAspectRatio: true
    }"
    :chart-data="{
      labels: this.labels,
      datasets: [
        {
          backgroundColor: ['#fff7f3', '#fde0dd' , '#fcc5c0', '#fa9fb5', '#f768a1', '#ae017e' , '#7a0177', '#49006a'],
          data: this.counts,
        }
      ]
    }"
  />
</template>

<script>
import { Doughnut } from 'vue-chartjs/legacy'
import { Chart as ChartJS, Title, Tooltip, Legend, ArcElement, CategoryScale, LinearScale } from 'chart.js'

ChartJS.register(Tooltip, Legend, ArcElement, CategoryScale)

export default {
  name: 'DoughnutChart',
  components: {
    Doughnut
  },
  props: {
    labels: Array,
    counts: Array,
    chartId: {
      type: String,
      default: 'doughnut-chart',
    }
  }
}
</script>