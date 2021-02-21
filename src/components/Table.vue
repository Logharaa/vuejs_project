<template>
  <div id="maRecherche">
    <h1>Recherche</h1>
    <Sort v-for="item in sorts" :key="item[1]" v-bind:id="item[1]">
    </Sort>
  </div>
</template>

<script>
import Sort from "./Sort.vue";
import { sortTable } from '../assets/data.min.js'

export default {
  name: "Table",
  components: {
    Sort
  },
  data () {
    return {
      sorts: sortTable
    }
  }
};
</script>

<style scoped>
  h1 {
    color: white;
  }
</style>
