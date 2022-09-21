<template>
  <div class="visualMap" ref="visualMap"></div>
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
      this.chart = markRaw(echarts.init(this.$refs.visualMap));
      this.option = {
        dataset: {
          source: [
            ["score", "amount", "product"],
            [89.3, 58212, "Matcha Latte"],
            [57.1, 78254, "Milk Tea"],
            [74.4, 41032, "Cheese Cocoa"],
            [50.1, 12755, "Cheese Brownie"],
            [89.7, 20145, "Matcha Cocoa"],
            [68.1, 79146, "Tea"],
            [19.6, 91852, "Orange Juice"],
            [10.6, 101852, "Lemon Juice"],
            [32.7, 20112, "Walnut Brownie"],
          ],
        },
        grid: { containLabel: true },
        xAxis: { name: "amount" },
        yAxis: { type: "category" },
        visualMap: {
          orient: "horizontal",
          left: "center",
          min: 10,
          max: 100,
          text: ["High Score", "Low Score"],
          // Map the score column to color
          dimension: 0,
          inRange: {
            color: ["#D7DA8B", "#E15457"],
          },
        },
        series: [
          {
            type: "bar",
            encode: {
              // Map the "amount" column to X axis.
              x: "amount",
              // Map the "product" column to Y axis
              y: "product",
            },
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
.visualMap {
  width: 600px;
  height: 400px;
  float: left;
}
</style>
视觉元素
symbol: 图元的图形类别。
symbolSize: 图元的大小。
color: 图元的颜色。
colorAlpha: 图元的颜色的透明度。
opacity: 图元以及其附属物（如文字标签）的透明度。
colorLightness: 颜色的明暗度。
colorSaturation: 颜色的饱和度。
colorHue: 颜色的色调。