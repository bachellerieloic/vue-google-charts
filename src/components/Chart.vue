<template>
  <div id="app" style="width:60vw; margin-left:auto; margin-right:auto">
    <GChart type="LineChart" :data="chartData" :options="chartOptions"/>
    <GChart type="ColumnChart" :data="chartData" :options="chartOptions"/>
    <GChart type="AreaChart" :data="chartData" :options="chartOptions"/>
    <GChart type="PieChart" :data="chartData" :options="chartOptions"/>
    <button @click="updateData" style="margin-top:20px">Click to change the data</button>
<!--    <button @click="addYear" v-if="!yearAdded" style="margin-top:20px">Add Year</button>-->
<!--    <button @click="removeYear" v-else style="margin-top:20px">Remove Year</button>-->

    {{ JSON.stringify(chartDataRows)}}
  </div>
</template>

<script>
import { GChart } from "vue-google-charts";
export default {
  name: "Chart",
  components: {
    GChart
  },
  data () {
    return {
      chartDataHeader: ['Year', 'Sales', 'Expenses', 'Profit'],
      year: ['2018', 200, 300, 400, 500],
      yearAdded: false,
      chartDataRows: [
        ['2014', 1000, 400, 200],
        ['2015', 1170, 460, 250],
        ['2016', 660, 1120, 300],
        ['2017', 1030, 540, 350]
      ],
      updatedChartData: [],
      chartOptions: {
        chart: {
          title: 'Company Performance',
          subtitle: 'Sales, Expenses, and Profit: 2014-2017'
        }
      }
    }
  },
  computed: {
    chartData () {
      return [ this.chartDataHeader, ...this.updatedChartData ]
    }
  },
  methods: {
    updateData () {
      this.updatedChartData = this.chartDataRows
          .map(row => {
            return row.map((item, index) => {
              if (index !== 0) {
                const max = item + 1000
                const min = 0
                return Math.floor(Math.random() * (max - min)) + min
              }
              return item
            })
          })
    },
    addYear() {
      this.chartDataRows.push(this.year);
      this.yearAdded = true;
      this.updateData();
    },
    removeYear(){
      this.chartDataRows.pop();
      this.yearAdded = false;
      this.updateData();

    }
  },
  created () {
    this.updateData()
  }
};
</script>

