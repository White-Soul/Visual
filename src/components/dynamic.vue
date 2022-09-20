<template>
    <div class="dynamic" ref="dynamic" ></div>
</template>

<script>
import * as echarts from 'echarts'
// 标记一个对象，使其永远不会再成为响应式对象。
import { markRaw } from "vue";
export default {
    data() {
        return {
            
        }
    },
}
</script>

<style>
    .dynamic{
        /* style="width: 400px; height:400px" */
        width: 400px;
        height: 400px;
        float: left;
    }
</style>