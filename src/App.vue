<template>
  <div>
    <Bar />
    <Pie />
    <Dynamic />
  </div>
</template>

<script>
import Bar from "./components/bar.vue";
import Pie from './components/pie.vue';
import Dynamic from './components/dynamic.vue';

export default {
  name: 'App',
  components: {
    Bar,
    Pie,
    Dynamic
  }
}
</script>

<style>

</style>
