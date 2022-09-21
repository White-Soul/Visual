<template>
  <div class="dataZoom" ref="dataZoom"></div>
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
    init() {
      this.chart = markRaw(echarts.init(this.$refs.dataZoom));
      //   如果想在坐标系内进行拖动，以及用鼠标滚轮（或移动触屏上的两指滑动）进行缩放，那么需要 再再加上一个 inside 型的 dataZoom 组件。
      this.option = {
        xAxis: {
          type: "value",
        },
        yAxis: {
          type: "value",
        },
        // 当然我们可以通过 dataZoom.xAxisIndex 或 dataZoom.yAxisIndex 来指定 dataZoom 控制哪个或哪些数轴。
        dataZoom: [
          {
            // 这个dataZoom组件，默认控制x轴。
            type: "slider", // 这个 dataZoom 组件是 slider 型 dataZoom 组件
            start: 10, // 左边在 10% 的位置。
            end: 60, // 右边在 60% 的位置。
          },
          {
            // 这个dataZoom组件，也控制x轴。
            type: "inside", // 这个 dataZoom 组件是 inside 型 dataZoom 组件
            start: 10, // 左边在 10% 的位置。
            end: 60, // 右边在 60% 的位置。
          },
        ],
        series: [
          {
            type: "scatter", // 这是个『散点图』
            itemStyle: {
              opacity: 0.8,
            },
            symbolSize: function (val) {
              return val[2] * 40;
            },
            data: [
              ["14.616", "7.241", "0.896"],
              ["3.958", "5.701", "0.955"],
              ["2.768", "8.971", "0.669"],
              ["9.051", "9.710", "0.171"],
              ["14.046", "4.182", "0.536"],
              ["12.295", "1.429", "0.962"],
              ["4.417", "8.167", "0.113"],
              ["0.492", "4.771", "0.785"],
              ["7.632", "2.605", "0.645"],
              ["14.242", "5.042", "0.368"],
            ],
          },
        ],
      };
      this.chart.setOption(this.option);
    },
  },
  mounted() {
    this.init();
  },
};
</script>

<style>
.dataZoom {
  width: 600px;
  height: 400px;
  float: left;
}
</style>