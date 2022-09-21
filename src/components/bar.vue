<template>
  <div class="bar" ref="chart"></div>
</template>

<script>
// echats5以后不能使用这个引入
// import echarts from 'echarts';
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
      this.chart = markRaw(echarts.init(this.$refs.chart));
      // 配置属性
      this.option = {
        // 标题
        title: { text: "第一个Echarts实例" },
        // 配置提示信息
        tooltip: {},
        // 图例组件
        legend: {
          data: [
            {
              name: "系列1",
              // 强制设置图形为圆。
              icon: "circle",
              // 设置文本为红色
              textStyle: {
                color: "red",
              },
            },
          ],
        },
        // x轴
        xAxis: {
          data: ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"],
        },
        // y轴
        yAxis: {},
        // 系列列表 每个系列通过 type 决定自己的图表类型:
        series: [
          {
            name: "系列1",
            type: "bar",
            data: [120, 200, 150, 80, 70, 110, 130],
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
.bar {
  width: 600px;
  height: 400px;
  float: left;
}
</style>
/*
type: 'bar'：柱状/条形图
type: 'line'：折线/面积图
type: 'pie'：饼图
type: 'scatter'：散点（气泡）图
type: 'effectScatter'：带有涟漪特效动画的散点（气泡）
type: 'radar'：雷达图
type: 'tree'：树型图
type: 'treemap'：树型图
type: 'sunburst'：旭日图
type: 'boxplot'：箱形图
type: 'candlestick':K线图
type: 'heatmap'：热力图
type: 'map'：地图
type: 'parallel'：平行坐标系的系列
type: 'lines'：线图
type: 'graph'：关系图
type: 'sankey'：桑基图
type: 'funnel'：漏斗图
type: 'gauge'：仪表盘
type: 'pictorialBar'：象形柱图
type: 'themeRiver'：主题河流
type: 'custom'：自定义系列
*/