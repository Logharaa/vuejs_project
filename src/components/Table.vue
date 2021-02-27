<template>
  <div>
    <RechercheInput></RechercheInput>
    <div class="row" id="maRecherche">
      <Sort v-for="item in sorts" v-bind:key="item[1]" v-bind:id="item[1]"></Sort>
    </div>
  </div>
</template>

<script>
import Sort from "./Sort.vue";
import RechercheInput from "./RechercheInput.vue";
import { sortTable } from '../assets/data.min.js'

export default {
  name: "Table",
  components: {
    Sort,
    RechercheInput
  },
  data () {
    return {
      sorts: sortTable,
    }
  }
};
</script>

<style scoped>
  h1 {
    color: white;
  }
</style>
