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
          type: 'bar',
          backgroundColor:'transparent',
        },
        title: {
          text: null,
        },
        xAxis: {
          categories: [
            'Google Ireland', 'Google Portugal', 'Google Netherlands', 'Google Italy',
            'Tiktok Portugal', 'Tiktok Belgium', 'Tiktok Italy', 'Other (14)'
          ],
        },
        yAxis: {
          title: {
            text: null,
          },
        },
        legend: {
          enabled: true, // Active la légende
        },
        exporting: {
          enabled: false,
        },
        plotOptions: {
          bar: {
            borderRadius: '20%',
            dataLabels: {
                enabled: true
            },
            groupPadding: 0.1
        }
        },
        series: [
          {
            name: 'Lower bound',
            data: [90, 10, 5, 20, 6, 9, 10, 260], // Valeurs pour Lower bound
            color: 'rgb(160, 189, 241)', // Couleur pour Lower bound
          },
          {
            name: 'ROI',
            data: [10, 10, 10, 10, 10, 5, 20, 430], // Valeurs pour ROI
            color: 'rgb(61, 61, 166)', // Couleur pour ROI
          },
          {
            name: 'Upper bound',
            data: [20, 20, 10, 10, 10, 10, 40, 45], // Valeurs pour Upper bound
            color: 'rgb(104, 150, 233)', // Couleur pour Upper bound
          }, 
        ],
      }
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
