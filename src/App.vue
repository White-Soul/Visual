<template>
  <div class="apps">
    <Bar />
    <Pie />
    <!-- <Dynamic /> -->
    <Discount />
    <Map />
    <Dataset />
  </div>
</template>

<script>
import Bar from "./components/bar.vue";
import Pie from './components/pie.vue';
import Dynamic from './components/dynamic.vue';
import Discount from './components/Discount.vue';
import Map from './components/map.vue';
import Dataset from './components/dataset.vue';

export default {
  name: 'App',
  components: {
    Bar,
    Pie,
    Dynamic,
    Discount,
    Map,
    Dataset
  }
}
</script>

<style>
  .apps > div{
    margin-top: 20px;
  }
</style>
