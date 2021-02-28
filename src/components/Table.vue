<template>
  <div>
    <FiltersInput></FiltersInput>
    <div class="row" id="maRecherche">
      <div v-show="sorts.length === 0" class="alert alert-danger" role="alert">Aucun sort n'a été trouvé</div>
      <Sort v-for="item in sortsAfterFiltering" v-bind:key="item[1]" v-bind:id="item[1]"></Sort>
    </div>
  </div>
</template>

<script>
import { sortTable } from "../assets/data.min.js";
import Sort from "./Sort.vue";
import FiltersInput from "./FiltersInput.vue";

export default {
  name: "Table",
  components: {
    Sort,
    FiltersInput
  },
  data() {
    return {
      sorts: [],
      sortsAfterFiltering: []
    }
  },
  methods: {
    getSortsByConf() {
      let sorts = [];
      
      // Filtrage des sorts ayant un nom donné
      let booksName = JSON.parse(localStorage.getItem("livresAjoutes"));

      if (booksName && booksName.length > 0) {
        booksName.forEach(book => {
          sorts = sorts.concat(sortTable.filter( sort => sort[0] === book ));
        });
      }

      // Filtrage des sorts appartenant à une école donnée
      sorts = sorts.filter(sort => sort[2] === JSON.parse(localStorage.getItem("ecoles"))[0]);
      
      // Filtrage de tous les sorts ayant un niveau supérieur au niveau minimum
      if (localStorage.getItem("niveauMin")) {
        sorts = sorts.filter(sort => {
          let sortLevels = [];
          let classes = sort[4];
          classes.forEach(classe => sortLevels.push(classe[1]));
          return Math.min(sortLevels) >= localStorage.getItem("niveauMin");
        });
      }

      // Filtrage de tous les sorts ayant un niveau inférieur au niveau maximum
      if (localStorage.getItem("niveauMax")) {
        sorts = sorts.filter(sort => {
          let sortLevels = [];
          let classes = sort[4];
          classes.forEach(classe => sortLevels.push(classe[1]));
          return Math.max(sortLevels) <= localStorage.getItem("niveauMax");
        });
      }

      this.sortsAfterFiltering = sorts;
      this.sorts = sorts;
    }
  }
};
</script>

<style scoped>
  .alert {
    margin: 0 auto;
  }
</style>
