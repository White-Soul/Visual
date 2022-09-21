<template>
  <div>
    <div class="dataset" ref="dataset"></div>
    <div class="mapping" ref="mapping"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
export default {
  data() {
    return {
      chart: null,
      option: {},
    };
  },
  methods: {
    initDataset() {
      this.chart = markRaw(echarts.init(this.$refs.dataset));
      this.option = {
        title: { text: "数据集" },
        legend: {},
        tooltip: {},
        dataset: {
          //   source: [
          //     ["product", "2015", "2016", "2017"],
          //     ["Matcha Latte", 43.3, 85.8, 93.7],
          //     ["Milk Tea", 83.1, 73.4, 55.1],
          //     ["Cheese Cocoa", 86.4, 65.2, 82.5],
          //     ["Walnut Brownie", 72.4, 53.9, 39.1],
          //   ],
          dimensions: ["product", "2015", "2016", "2017"],
          source: [
            { product: "Matcha Latte", 2015: 43.3, 2016: 85.8, 2017: 93.7 },
            { product: "Milk Tea", 2015: 83.1, 2016: 73.4, 2017: 55.1 },
            { product: "Cheese Cocoa", 2015: 86.4, 2016: 65.2, 2017: 82.5 },
            { product: "Walnut Brownie", 2015: 72.4, 2016: 53.9, 2017: 39.1 },
          ],
        },
        xAxis: { type: "category" },
        yAxis: {},
        series: [{ type: "bar" }, { type: "bar" }, { type: "bar" }],
      };
      this.chart.setOption(this.option);
    },
    initMapping() {
      this.chart = markRaw(echarts.init(this.$refs.mapping));
      this.option = {
        legend: {},
        tooltip: {},
        dataset: {
          source: [
            ["product", "2012", "2013", "2014", "2015"],
            ["Matcha Latte", 41.1, 30.4, 65.1, 53.3],
            ["Milk Tea", 86.5, 92.1, 85.7, 83.1],
            ["Cheese Cocoa", 24.1, 67.2, 79.5, 86.4],
          ],
        },
        xAxis: [
          { type: "category", gridIndex: 0 },
          { type: "category", gridIndex: 1 },
        ],
        yAxis: [{ gridIndex: 0 }, { gridIndex: 1 }],
        grid: [{ bottom: "55%" }, { top: "55%" }],
        series: [
          // 这几个系列会在第一个直角坐标系中，每个系列对应到 dataset 的每一行。
          { type: "bar", seriesLayoutBy: "row" },
          { type: "bar", seriesLayoutBy: "row" },
          { type: "bar", seriesLayoutBy: "row" },
          // 这几个系列会在第二个直角坐标系中，每个系列对应到 dataset 的每一列。
          { type: "bar", xAxisIndex: 1, yAxisIndex: 1 },
          { type: "bar", xAxisIndex: 1, yAxisIndex: 1 },
          { type: "bar", xAxisIndex: 1, yAxisIndex: 1 },
          { type: "bar", xAxisIndex: 1, yAxisIndex: 1 },
        ],
      };
      this.chart.setOption(this.option);
    },
  },
  mounted() {
    this.initDataset();
    this.initMapping();
  },
};
</script>

<style>
.dataset {
  width: 600px;
  height: 400px;
  float: left;
}
.mapping {
  width: 600px;
  height: 400px;
  float: left;
}
</style>