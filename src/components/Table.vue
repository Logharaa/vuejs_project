<template>
  <div>
    <RechercheInput></RechercheInput>
    <div class="row" id="maRecherche">
      <Sort v-for="item in sorts" v-bind:key="item[1]" v-bind:id="item[1]"></Sort>
    </div>
  </div>
</template>

<script>
import { sortTable } from "../assets/data.min.js";
import Sort from "./Sort.vue";
import RechercheInput from "./RechercheInput.vue";

export default {
  name: "Table",
  components: {
    Sort,
    RechercheInput
  },
  data() {
    return {
      sorts: this.getSortArrayByConf(),
    }
  },
  methods: {
    getSortArrayByConf() {
      let sorts = sortTable;
      /*if (localStorage.getItem("livresAjoutes") != []) {
      }*/
      return sorts;
    }
  }
};
</script>

<style scoped>
  h1 {
    color: white;
  }
</style>
