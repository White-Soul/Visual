<template>
  <div>
    <div style="width: 400px; height:400px" ref="dynamic" ></div>
  </div>
</template>

<script>
import * as echarts from 'echarts'
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
var base = +new Date(2014, 9, 3);
var oneDay = 24 * 3600 * 1000;
var date = [];

var data = [Math.random() * 150];
var now = new Date(base);

function addData(shift) {
    now = [now.getFullYear(), now.getMonth() + 1, now.getDate()].join('/');
    date.push(now);
    data.push((Math.random() - 0.4) * 10 + data[data.length - 1]);

    if (shift) {
        date.shift();
        data.shift();
    }

    now = new Date(+new Date(now) + oneDay);
}

for (var i = 1; i < 100; i++) {
    addData();
}
const dynamic = {
    data() {
        return {
            chart: null,
            timer: null
        }
    },
    methods: {
        times(){
            addData(true);
            this.chart.setOption({
                xAxis: {
                    data: date
                },
                series: [{
                    name:'成交',
                    data: data
                }]
            });        
        },
        init(){
            this.chart = markRaw(echarts.init(this.$refs.dynamic))
            this.timer = setInterval(this.times(), 500);
        }
    },
    mounted() {
        this.init()
    },
    beforeDestroy() {
        clearInterval(this.timer)
    },
}
export default dynamic
</script>

<style>

</style>