<template>
  <div>
    <h1>Recherche</h1>
    <RechercheInput></RechercheInput>
    <div class="row" id="maRecherche">
      <Sort class="col-2 sort" v-for="item in sorts" :key="item[1]" v-bind:id="item[1]">
      </Sort>
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
  .sort {
    border: thick ridge #32a1ce;
    margin: 1rem;
  }
</style>
