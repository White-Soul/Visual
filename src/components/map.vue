<template>
  <div class="map" ref="map"></div>
</template>

<script>
import * as echarts from "echarts";
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
import china from "../assets/china.json";
export default {
  data() {
    return {
      chart: null,
    };
  },
  methods: {
    init() {
      echarts.registerMap("china", china);
      this.chart = markRaw(echarts.init(this.$refs.map));
      let option = {
        title: { text: "地图" },
        series: {
          name: "地图",
          map: "china",
          type: "map",
          itemStyle: {
            borderWidth: 1,
            borderColor: "skyblue",
          },
        },
      };
      this.chart.setOption(option);
    },
  },
  mounted() {
    this.init();
  },
};
</script>

<style>
.map {
  width: 600px;
  height: 600px;
  float: left;
}
</style>