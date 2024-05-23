<template>
  <div class="main">
    <div class="main-table">
      <div ref="chart" style="width: 600px; height: 400px"></div>
      <!-- Use the AppNavigation component -->
      <AppNavigation @yearSelected="onYearSelected" />
    </div>
    <div class="main-stu">
      <span>您的成绩为：250</span>
      <span>您的成绩位于全省前50%</span>
    </div>
  </div>
</template>

<script>
import * as echarts from "echarts";
import AppNavigation from "./AppNavigation.vue";

export default {
  name: "AppMain",
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
    this.fetchChartData(2020); // Initial fetch for the default year
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$refs.chart);
    },
    async fetchChartData(year) {
      try {
        const response = await fetch(`http://127.0.0.1:3080/test?y=${year}`);
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
  border-radius: 5px; /* 添加圆角 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 添加阴影 */
  background-color: #f9f9f9; /* 背景颜色 */
  overflow: hidden; /* 确保子元素不溢出 */
}

.main-table {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  min-width: 600px;
  width: 80%;
  height: 400px;
  border-radius: 5px; /* 添加圆角 */
  overflow: hidden; /* 确保子元素不溢出 */
  background-color: #ffffff; /* 背景颜色 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 添加阴影 */
  box-sizing: border-box;
  padding: 10px;
}
.main-table > img {
  width: 100%;
  border-bottom: 1px solid #ccc; /* 图片下方的分割线 */
}
.main-stu {
  display: flex;
  flex-direction: column;
  line-height: 1.5; /* 使用倍数来代替百分比 */
  flex: 1;
  justify-content: center;
  align-items: center;
  padding: 20px; /* 内边距 */
  background-color: #fafafa; /* 背景颜色 */
  border-left: 1px solid #ddd; /* 左边的分割线 */
}
.main-stu span {
  margin: 0; /* 移除默认的段落边距 */
  font-size: 16px; /* 字体大小 */
  color: #333; /* 字体颜色 */
}
.main-stu h2 {
  margin-bottom: 10px; /* 标题下方的间距 */
  font-size: 20px; /* 标题字体大小 */
  color: #007bff; /* 标题颜色 */
}
</style>
