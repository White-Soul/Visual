<template>
  <div class="dynamic" ref="dynamic"></div>
</template>

<script>
import * as echarts from "echarts";
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
var base = +new Date(2014, 9, 3);
var oneDay = 24 * 3600 * 1000;
var date = [];
var now = new Date(base);
export default {
  data() {
    return {
      chart: null,
      option: {},
      a: null,
      datas: [Math.random() * 150],
    };
  },
  methods: {
    init() {
      this.chart = markRaw(echarts.init(this.$refs.dynamic));
      for (var i = 1; i < 100; i++) {
        this.addData();
      }
      this.option = {
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: date,
        },
        yAxis: {
          boundaryGap: [0, "50%"],
          type: "value",
        },
        series: [
          {
            name: "成交",
            type: "line",
            smooth: true,
            symbol: "none",
            stack: "a",
            areaStyle: {
              normal: {},
            },
            data: this.datas,
          },
        ],
      };
      this.chart.setOption(this.option);
    },
    addData(shift) {
      now = [now.getFullYear(), now.getMonth() + 1, now.getDate()].join("/");
      date.push(now);
      this.datas.push(
        (Math.random() - 0.4) * 10 + this.datas[this.datas.length - 1]
      );

      if (shift) {
        date.shift();
        this.datas.shift();
      }
      now = new Date(+new Date(now) + oneDay);
    },
    timer() {
      this.addData(true);
      this.chart.setOption({
        xAxis: {
          data: date,
        },
        series: [
          {
            name: "成交",
            data: this.datas,
          },
        ],
      });
    },
  },
  mounted() {
    this.init();
    this.a = setInterval(this.timer, 500);
  },
  beforeDestroy() {
    clearInterval(this.a);
  },
};
</script>

<style>
.dynamic {
  /* style="width: 400px; height:400px" */
  width: 400px;
  height: 400px;
  float: left;
}
</style>