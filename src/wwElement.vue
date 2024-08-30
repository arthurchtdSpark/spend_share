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
            'Other (10)'
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
        tooltip: {
          pointFormat: '{series.name}: <b>{point.y:.1f}%</b>' // Format du tooltip avec un chiffre après la virgule
        },
        legend: {
          layout: 'horizontal',
          align: 'center',
          verticalAlign: 'bottom',
          floating: false,
          y: 10
        },
        plotOptions: {
          series: {
            groupPadding: 0.1,
            animation: {
              duration: 1500, // Durée de l'animation en millisecondes
              easing: 'easeOutBounce', // Type d'animation (par exemple, easing pour un effet "rebond")
            },
            dataLabels: {
              enabled: true, // Active les étiquettes de données
              format: '{point.y:.1f}%' // Format d'affichage des valeurs
            }
          }
        },
        exporting: {
          enabled: false,
        },
        series: [{
          name: 'Spend Share',
          data: [26.1, 25.2, 15.0, 14.0, 7.8, 3.2, 1.6, 1.5, 1.2, 0.8, 0.6, 3.0], // Données pour Spend Share
          color: 'rgb(160, 189, 241)' // Couleur pour Spend Share
        }, {
          name: 'Effect Share',
          data: [27.6, 9.0, 15.4, 8.3, 4.1, 2.6, 11.0, 1.0, 5.2, 1.5, 1.4, 12.8], // Données pour Effect Share
          color: 'rgb(48, 111, 225)' // Couleur pour Effect Share
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
