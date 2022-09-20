<template>
  <div>
    <div style="width: 400px; height:400px" ref="pie" ></div>
  </div>
</template>

<script>
import * as echarts from 'echarts'
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
export default {
    data() {
        return {
            chart: null
        }
    },
    methods: {
        init(){
            this.chart = markRaw(echarts.init(this.$refs.pie, 'dark'))
            // 开启 loading 效果
            this.chart.showLoading()
            // 可以通过设置参数 roseType: 'angle' 把饼图显示成南丁格尔图。
            let option = {
                title:{text:"访问来源"},
                series: [
                    {
                        name: '访问来源',
                        type: 'pie',    // 设置图表类型为饼图
                        radius: '55%',  // 饼图的半径，外半径为可视区尺寸（容器高宽中较小一项）的 55% 长度。
                        data:[          // 数据数组，name 为数据项名称，value 为数据项值
                            {value:235, name:'视频广告'},
                            {value:274, name:'联盟广告'},
                            {value:310, name:'邮件营销'},
                            {value:335, name:'直接访问'},
                            {value:400, name:'搜索引擎'}
                        ],
                        // itemStyle 参数可以设置诸如阴影、透明度、颜色、边框颜色、边框宽度等：
                        // itemStyle: {
                        //     normal: {
                        //         shadowBlur: 200,
                        //         shadowColor: 'rgba(0, 0, 0, 0.5)'
                        //     }
                        // }
                    }
                ],
                // 高亮样式。
                emphasis: {
                    itemStyle: {
                        // 高亮时点的颜色
                        color: 'red'
                    },
                    label: {
                        show: false,
                        // 高亮时标签的文字
                        // formatter: '高亮时显示的标签内容'
                    }
                },
            }
            this.chart.setOption(option)
            // 隐藏 loading 效果
            this.chart.hideLoading()
        }
    },
    mounted() {
        this.init()  
    },
}
</script>

<style>

</style>