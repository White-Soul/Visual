<template>
  <div class="apps">
    <bar />
    <pie />
    <!-- <Dynamic /> -->
    <discount />
    <map />
    <dataset />
    <visual-map />
    <data-zoom />
  </div>
</template>

<script>
import Bar from "./components/bar.vue";
import Pie from "./components/pie.vue";
import Dynamic from "./components/dynamic.vue";
import Discount from "./components/Discount.vue";
import Map from "./components/map.vue";
import Dataset from "./components/dataset.vue";
import VisualMap from "./components/visualMap.vue";
import DataZoom from "./components/dataZoom.vue";

export default {
  name: "App",
  components: {
    Bar,
    Pie,
    Dynamic,
    Discount,
    Map,
    Dataset,
    VisualMap,
    DataZoom,
  },
};
</script>

<style>
.apps > div {
  margin-top: 20px;
}
</style>
