<template>
  <div class="form-group row">
    <label for="nomSort" class="col-form-label">Sort :</label>
    <input class="col-sm-2 form-control" id="nomSort" type="text" placeholder="Abri" v-model="sortInput" v-on:input="updateSortsList()" />

    <label for="nomLivre" class="col-form-label">Livre :</label>
    <input class="col-sm-2 form-control" id="nomLivre" type="text" placeholder="Libris Mortis" v-model="livreInput" v-on:input="" />

    <label for="nomClasse" class="col-form-label">Classe :</label>
    <input class="col-sm-2 form-control" id="nomClasse" type="text" placeholder="Magicien" v-model="classeInput" v-on:input="" />
  </div>
</template>

<script>
export default {
  name: "FiltersInput",
  data() {
    return {
      sortInput: "",
      livreInput: "",
      classeInput: ""
    }
  },
  methods: {
    updateSortsList() {
      if (this.sortInput.length > 0) {
        this.$parent.sorts = this.$parent.sorts.filter(sort => {
          return sort[1].toLowerCase().includes(this.sortInput.toLowerCase())
        });
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