<template>
  <input id="rechercheInput" class="col-sm-1 form-control" type="text" placeholder="Sort" v-model="inputValue" v-on:input="onInput()"/>
</template>

<script>
import { sortTable } from "../assets/data.min.js";

export default {
  name: "RechercheInput",
  data () {
    return {
      inputValue: "",
      match: ""
    }
  },
  methods : {
    getSortByMatch(match) {
      let matchedSorts = []
      sortTable.forEach(sort => {
        if (sort[1].includes(match)) {
          matchedSorts.push(sort);
        }
      });
      console.log(matchedSorts);
      return matchedSorts;
    },
    onInput() {
      if (this.inputValue.length > 0) {
        this.$parent.sorts = this.getSortByMatch(this.inputValue);
      }
    }
  },
  computed: {
    updateSortList() {
      if (this.inputValue.length > 0) {
        this.$parent.sorts = "tmp";
      }
    }
  }
}
</script>

<style scoped>
  input {
    margin: 2em;
  }
</style>