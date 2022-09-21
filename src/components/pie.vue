<template>
  <div>
    <div class="pie" ref="pie"></div>
    <div class="pie" ref="carousel"></div>
  </div>
</template>

<script>
import * as echarts from "echarts";
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
let app = { currentIndex: -1 };
export default {
  data() {
    return {
      chart: null,
      chartpie: null,
      option: {},
      datas: [
        // 数据数组，name 为数据项名称，value 为数据项值
        { value: 235, name: "视频广告" },
        { value: 274, name: "联盟广告" },
        { value: 310, name: "邮件营销" },
        { value: 335, name: "直接访问" },
        { value: 400, name: "搜索引擎" },
      ],
      a: null,
    };
  },
  methods: {
    init() {
      console.log("this :>> ", this);
      // 'dark' 主题颜色
      this.chart = markRaw(echarts.init(this.$refs.pie, "dark"));
      // 开启 loading 效果
      this.chart.showLoading();
      // 可以通过设置参数 roseType: 'angle' 把饼图显示成南丁格尔图。
      this.option = {
        title: { text: "访问来源" },
        series: [
          {
            name: "访问来源", // 标识
            type: "pie", // 设置图表类型为饼图
            radius: "55%", // 饼图的半径，外半径为可视区尺寸（容器高宽中较小一项）的 55% 长度。
            roseType: "angle",
            data: this.datas,
            // itemStyle 参数可以设置诸如阴影、透明度、颜色、边框颜色、边框宽度等：
            // itemStyle: {
            //     normal: {
            //         shadowBlur: 200,
            //         shadowColor: 'rgba(0, 0, 0, 0.5)'
            //     }
            // }
          },
        ],
        // 高亮样式。
        emphasis: {
          itemStyle: {
            // 高亮时点的颜色
            color: "red",
          },
          label: {
            show: false,
            // 高亮时标签的文字
            // formatter: '高亮时显示的标签内容'
          },
        },
      };
      this.chart.setOption(this.option);
      // 隐藏 loading 效果
      this.chart.hideLoading();
    },
    initPie() {
      this.chartpie = markRaw(echarts.init(this.$refs.carousel));
      this.option = {
        title: {
          text: "饼图程序调用高亮示例",
          x: "center",
        },
        tooltip: {
          trigger: "item",
          formatter: "{a} <br/>{b} : {c} ({d}%)",
        },
        legend: {
          orient: "vertical",
          left: "left",
          data: ["直接访问", "邮件营销", "联盟广告", "视频广告", "搜索引擎"],
        },
        series: [
          {
            name: "访问来源",
            type: "pie",
            radius: "55%",
            center: ["50%", "60%"],
            data: this.datas,
            emphasis: {
              shadowBlur: 10,
              shadowOffsetX: 0,
              shadowColor: "rgba(0, 0, 0, 0.5)",
            },
          },
        ],
      };
      this.chartpie.setOption(this.option);
    },
    // 定时器执行函数
    timer() {
      var datalen = this.datas.length;
      // 取消之前高亮的图形
      this.chartpie.dispatchAction({
        type: "downplay",
        seriesIndex: 0,
        dataIndex: app.currentIndex,
      });
      app.currentIndex = (app.currentIndex + 1) % datalen;
      // 高亮当前图形
      this.chartpie.dispatchAction({
        type: "highlight",
        seriesIndex: 0,
        dataIndex: app.currentIndex,
      });
      // 显示 tooltip
      this.chartpie.dispatchAction({
        type: "showTip",
        seriesIndex: 0,
        dataIndex: app.currentIndex,
      });
    },
  },
  mounted() {
    this.init();
    this.chart.on("click", function (params) {
      alert(params.name);
    });
    this.initPie();
    this.a = setInterval(this.timer, 1000);
  },
  beforeDestroy() {
    clearInterval(this.a);
  },
};
</script>

<style>
.pie {
  width: 500px;
  height: 400px;
  float: left;
}
</style>