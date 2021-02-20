<template>
  <div id="maRecherche">
    <h1>Recherche</h1>
    <Element></Element>
  </div>
</template>

<script>
import Element from "./Element.vue";
import { sortTable } from '../assets/data.min.js'

export default {
  name: "Table",
  components: {
    Element
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
