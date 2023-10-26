<template>
    <Bar
      id="my-chart-id"
      :options="chartOptions"
      :data="chartData"
    />
  </template>
  
  <script>
  import { Bar } from 'vue-chartjs'
  import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js'
  
  ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)
  
  export default {
    name: 'BarChart',
    components: { Bar },
    data() {
      return {
        chartData: {
          labels: [ 'January', 'February', 'March' ],
          datasets: [ { 
            data: [37, 18, 32],
            backgroundColor: [
              'rgba(255, 99, 132, 0.6)', 
              'rgba(75, 192, 192, 0.6)', 
              'rgba(153, 102, 255, 0.6)', 
            ],
        } ]
            
        },
        chartOptions: {
          responsive: true
        }
      }
    }
  }
  </script>