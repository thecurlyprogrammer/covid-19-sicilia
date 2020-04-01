<template>
  <D3LineChart :config="chart_config" :datum="chart_data"></D3LineChart>
</template>

<script>
import { D3LineChart } from 'vue-d3-charts';

export default {
  props: ['casiTotali'],
  data() {
    return {
      casi_totali: [],
      chart_data: [
        { hours: 238, production: 134, date: 2000 },
        { hours: 938, production: 478, date: 2001 },
        { hours: 1832, production: 1392, date: 2002 },
        { hours: 2092, production: 2343, date: 2003 },
        { hours: 2847, production: 2346, date: 2004 },
        { hours: 2576, production: 2233, date: 2005 },
        { hours: 2524, production: 2325, date: 2006 },
        { hours: 1648, production: 2456, date: 2007 },
        { hours: 2479, production: 2329, date: 2008 },
        { hours: 3200, production: 2438, date: 2009 },
      ],
      chart_config: {
        values: ['hours', 'production'],
        date: {
          key: 'data',
          inputFormat: '%Y',
          outputFormat: '%Y',
        },
        points: false,
        axis: {
          yTicks: 5,
        },
      },
    };
  },
  components: {
    D3LineChart,
  },
  mounted() {
    this.casi_totali = this.casiTotali;
    console.log(this.casi_totali);
  },
};
</script>
