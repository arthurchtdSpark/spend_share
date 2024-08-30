<template>
  <div ref="chartContainer"></div>
</template>

<script>
import Highcharts from 'highcharts';

export default {
  props: {
    content: { type: Object, required: true },
  },

  data() {
    return {
      chartInstance: null, // Store chart instance here
    };
  },

  computed: {

    chartOptions() {
      
      return {
        chart: {
          type: 'column',
        },
        title: {
          text: null
        },
        xAxis: {
          categories: [
            'Google Ireland', 'Google Portugal', 'Google Netherlands', 'Google Italy',
            'Tiktok Belgium', 'Tiktok Portugal', 'Tiktok Italy', 'Google Spain',
            'Google Germany', 'Meta Netherlands', 'Meta Belgium', 'Meta Switzerland',
            'Meta Germany', 'Meta Ireland', 'Meta Spain', 'Meta Portugal',
            'Meta Italy', 'Google Belgium', 'Google Switzerland', 'Tiktok Switzerland',
            'Tiktok Spain'
          ]
        },
        yAxis: {
          title: {
            enabled:false
          }
        },
        legend: {
          enabled: false // Désactive la légende
         },

         exporting: {
            enabled: false,
        },

        series: [{
          name: 'ROI',
          data: [
            144.67, 13.8, 9.5, 7.3, 7.24,
            6.72, 5.32, 4.4, 2.33, 2.04,
            1.11, 1.09, 0.87, 0.7, 0.62,
            0.55, 0.38, 0.034, 0, 0
          ],
          dataLabels: {
            enabled: true,
            verticalAlign: 'bottom', // Positionne les étiquettes en haut
          },
          color: '#8BD7B6', 

          
        }]
      };
    },
  },

  watch: {
    chartOptions: {
      handler() {
        this.createChart();
      },
      deep: true, // Ensure it watches nested objects
    },
  },

  mounted() {
    this.createChart();
  },

  methods: {
    createChart() {
      if (this.chartInstance) {
        this.chartInstance.destroy(); // Destroy the existing chart before re-creating it
      }
      this.chartInstance = Highcharts.chart(this.$refs.chartContainer, this.chartOptions);
    },
  },
};
</script>

<style>
/* Add styles if necessary */
</style>
