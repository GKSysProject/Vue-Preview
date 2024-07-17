<template>
    <div class="main">
      <div class="main-table">
        <div ref="chart" style="width: 600px; height: 400px"></div>
        <!-- Use the AppNavigation component -->
        <AppNavigation @yearSelected="onYearSelected" />
      </div>
    </div>
  </template>
  
  <script>
  import * as echarts from "echarts";
  import AppNavigation from "./AppNavigation.vue";
  
  export default {
    components: {
      AppNavigation,
    },
    data() {
      return {
        chart: null,
      };
    },
    mounted() {
      this.initChart();
      this.fetchChartData(2020);
    },
    methods: {
      initChart() {
        this.chart = echarts.init(this.$refs.chart);
      },
      async fetchChartData(year) {
        try {
          const response = await fetch(`${this.$config.serverUrl}/year?y=${year}`);
          const data = await response.json();
          this.updateChart(data);
        } catch (error) {
          console.error("Error fetching chart data:", error);
        }
      },
      updateChart(data) {
        const option = {
          title: {
            text: "历年高考一分一段表",
          },
          tooltip: {
            trigger: "axis",
          },
          xAxis: {
            type: "category",
            data: data.xAxis,
          },
          yAxis: {
            type: "value",
          },
          series: [
            {
              data: data.series,
              type: "line",
            },
          ],
        };
        this.chart.setOption(option);
      },
      onYearSelected(year) {
        this.fetchChartData(year);
      },
    },
  };
  </script>
  
  <style scoped>
  .main {
    position: relative;
    margin-top: 150px;
    margin-left: 50px;
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    width: 70%;
    height: 400px;
    border-radius: 5px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
    overflow: hidden; 
  }
  
  .main-table {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    min-width: 600px;
    width: 80%;
    height: 400px;
    border-radius: 5px; 
    overflow: hidden; 
    background-color: #ffffff; 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); 
    box-sizing: border-box;
    padding: 10px;
  }
  .main-table > img {
    width: 100%;
    border-bottom: 1px solid #ccc;
  }
  .main-stu {
    display: flex;
    flex-direction: column;
    line-height: 1.5;
    flex: 1;
    justify-content: center;
    align-items: center;
    padding: 20px; 
    background-color: #fafafa; 
    border-left: 1px solid #ddd; 
  }
  .main-stu span {
    margin: 0;
    font-size: 16px; 
    color: #333; 
  }
  .main-stu h2 {
    margin-bottom: 10px;
    font-size: 20px; 
    color: #007bff;
  }
  </style>
  