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
          type: 'pie', 
          backgroundColor: 'transparent',
        },
        exporting: {
          enabled: false,
        },
        title: {
          text: null
        },
        tooltip: {
          pointFormat: '{series.name}: <b>{point.percentage:.1f}%</b>'
        },
        plotOptions: {
          pie: {
            allowPointSelect: true,
            cursor: 'pointer',
            innerSize: '50%',
            dataLabels: {
                enabled: true,
                format: '<b>{point.name}</b>: {point.percentage:.1f} %',
            },
            colors: [
                    '#FFB3BA', // Rose pastel
                    '#FFDFBA', // Orange pastel
                    '#FFFFBA', // Jaune pastel
                    '#BAFFC9', // Vert pastel
                    '#BAE1FF', // Bleu pastel
                    '#D4A5A5', // Rouge pastel
                    '#B39EB5', // Violet pastel
                  ], // Utilisation des couleurs pastel
          }
        },
        series: [{
          name: 'Channel',
          colorByPoint: true,
          data: [
            { name: 'Meta Belgium', y: 26.13 },
            { name: 'Meta Italy', y: 25.17 },
            { name: 'Meta Switzerland', y: 14.96 },
            { name: 'Meta Spain', y: 14.03 },
            { name: 'Meta Portugal', y: 7.85 },
            { name: 'Meta Germany', y: 3.17 },
            { name: 'Other', y: 8.71 }
          ]
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
