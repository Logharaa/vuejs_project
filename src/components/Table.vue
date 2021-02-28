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
      sorts: [],
    }
  },
  methods: {
    getSortArrayByConf() {
      let sorts = [];
      let booksName = JSON.parse(localStorage.getItem("livresAjoutes"));
      //Livres
      if (booksName.length > 0) {
        booksName.forEach(book => {
          sorts = sorts.concat(sortTable.filter( sort => sort[0] === book ));
        });
      }
      //École
      sorts = sorts.filter(sort => sort[2] === JSON.parse(localStorage.getItem("ecoles"))[0]);
      
      //Niveau Min
      if (localStorage.getItem("niveauMin")) {
        let niveauMin = 9;
        sorts.forEach(sort => {
          let classes = sort[4];
          classes.forEach(classe => {
            let niveau = classe[1];
            if (niveau < niveauMin) niveauMin = niveau;
          });
        });
          sorts = sorts.filter(sort => niveauMin >= localStorage.getItem("niveauMin"));
      }
      console.log(sorts);

      //Niveau Max
      if (localStorage.getItem("niveauMax")) {
        let niveauMax = 0;
        sorts.forEach(sort => {
          let classes = sort[4];
          classes.forEach(classe => {
            let niveau = classe[1];
            if (niveau > niveauMax) niveauMax = niveau;
          });
        });
          console.log("localStorage : " + localStorage.getItem("niveauMax") + " | niveauMax : " + niveauMax);
          sorts = sorts.filter(sort => niveauMax <= localStorage.getItem("niveauMax"));
      }

      console.log(sorts);

      this.sorts = sorts;
    }
  }
};
</script>

<style scoped>
  h1 {
    color: white;
  }
</style>
