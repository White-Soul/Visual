<template>
    <div class="discount"  ref="discount"></div>
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
            this.chart = markRaw(echarts.init(this.$refs.discount))
            let option = {
                title : {text: '折线图'},
                series: [{
                    name: '折线图',
                    type: 'line',
                    data: [1,3,5,7,5,4,2]
                }],
                xAxis: {
                    data: [
                        'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'
                    ]
                },
                yAxis: {}
            }
            this.chart.setOption(option)
        }  
    },
    mounted() {
        this.init()  
    },
}
</script>

<style scoped>
    .discount{
        width: 400px;
        height: 300px;
        float: left;
    }
</style>