<template>
  <input id="rechercheInput" class="col-sm-1 form-control" type="text" placeholder="Sort" v-model="inputValue" v-on:input="updateSortsList()"/>
</template>

<script>
export default {
  name: "RechercheInput",
  data() {
    return {
      inputValue: ""
    }
  },
  methods: {
    updateSortsList() {
      if (this.inputValue.length > 0) {
        this.$parent.sorts = this.$parent.sorts.filter(sort => {
          return sort[1].toLowerCase().includes(this.inputValue.toLowerCase())
        });
      }
    }
  }
};
</script>

<style scoped>
  input {
    margin: 2em;
  }
</style>