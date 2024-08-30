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
      
      return {chart: {
          type: 'bar',
          backgroundColor:'transparent'
        },
        title: {
          text: null
        },
        xAxis: {
          categories: [
            'Meta Belgium',
            'Meta Italy',
            'Meta Switzerland',
            'Meta Spain',
            'Meta Portugal',
            'Meta Germany',
            'Google Italy',
            'Meta Ireland',
            'Google Spain',
            'Meta Netherlands',
            'Google Germany',
            'Tiktok Belgium',
            'Tiktok Spain',
            'Tiktok Italy',
            'Google Belgium',
            'Other (6)'
          ],
          title: {
            text: null
          }
        },
        yAxis: {
          min: 0,
          title: {
            text: null,
            align: 'high'
          },
          labels: {
            overflow: 'justify'
          }
        },
        legend: {
          enabled:false
        },
        plotOptions: {
          series: {
            stacking: 'normal', // Empile les séries l'une en dessous de l'autre
            pointWidth: 25, // Largeur des barres
            dataLabels: {
              enabled: true, // Active les étiquettes de données
              crop:false,
              overflow:'allow',
              align: 'right',
              x: 70,
              format: '{point.y:,.1f}€' // Format d'affichage des valeurs avec le formatage anglais
            }
          },

          animation: {
              duration: 1500, // Durée de l'animation en millisecondes
              easing: 'easeOutBounce', // Type d'animation (par exemple, easing pour un effet "rebond")
          },

        },
        exporting: {
          enabled: false,
        },
        series: [
          {
            name: 'Spend',
            data: [
              218325,
              210328,
              125022,
              117205,
              65589,
              26454,
              13299,
              12602,
              10327,
              6293,
              5235,
              4924,
              4287,
              3299,
              2959
            ], // Données pour Spend Share
            color: 'rgb(104, 150, 233)',
          }
        ]
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
