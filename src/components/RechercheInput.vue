<template>
  <input id="rechercheInput" type="text" v-on:input="onInput()"/>
</template>

<script>
import { sortTable } from '../assets/data.min.js'

export default {
  name: "RechercheInput",
  data () {
    return {
      match: "",
    }
  },
  methods : {
    getSortByMatch(match) {
      let matchedSorts = []
      sortTable.forEach(sort => {
        if (sort[0].includes(match)) {
          matchedSorts.push(sort);
        }
      });
      console.log(matchedSorts);
      return matchedSorts;
    },
    onInput() {
      let inputValue = document.getElementById("rechercheInput").value;
      if (inputValue.length > 0) {
        this.$parent.sorts = this.getSortByMatch(inputValue);
      }
    }
  }
}
</script>

<style scoped>
</style>