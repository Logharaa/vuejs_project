<template>
  <div class="form-group row">
    <label for="nomSort" class="col-form-label">Sort :</label>
    <input class="col-sm-2 form-control" id="nomSort" type="text" placeholder="Abri" v-model="sortInput" v-on:input="updateSortsListSortName()" />

    <label for="nomLivre" class="col-form-label">Livre :</label>
    <input class="col-sm-2 form-control" id="nomLivre" type="text" placeholder="Libris Mortis" v-model="livreInput" v-on:input="updateSortsListBookName()" />

    <label for="nomClasse" class="col-form-label">Classe :</label>
    <input class="col-sm-2 form-control" id="nomClasse" type="text" placeholder="Magicien" v-model="classeInput" v-on:input="updateSortsListClasseName()" />
  </div>
</template>

<script>
export default {
  name: "FiltersInput",
  data() {
    return {
      sortInput: "",
      livreInput: "",
      classeInput: "",
    }
  },
  methods: {
    updateSortsListSortName() {
      if (this.sortInput.length > 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts.filter(sort => {
        return sort[1].toLowerCase().includes(this.sortInput.toLowerCase())
        });
      }
      else if (this.livreInput.length == 0 && this.classeInput.length == 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts;
      }
    },
    updateSortsListBookName() {
      if (this.livreInput.length > 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts.filter(sort => {
          return sort[0].toLowerCase().includes(this.livreInput.toLowerCase())
        });
      }
      else if (this.sortInput.length == 0 && this.classeInput.length == 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts;
      }
    },
    updateSortsListClasseName() {
      if (this.classeInput.length > 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts.filter(sort => {
          let match = false;
          sort[4].forEach(classe => {
            if (classe[0].toLowerCase().includes(this.classeInput.toLowerCase())) match = true;
          });
          return match;
        });
      }
      else if (this.sortInput.length == 0 && this.livreInput.length == 0) {
        this.$parent.sortsAfterFiltering = this.$parent.sorts;
      }
    }
  }
};
</script>

<style scoped>
  .form-group {
    margin: 2em;
  }
  label {
    color: white;
    margin-left: 4em;
    margin-right: 0.5em;
  }
  
</style>