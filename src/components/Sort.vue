<template>
  <div>
    <h2>{{ getPropertyById(1) }}</h2>
    <h3 v-on:click="showDescription()">Description</h3>
    <p v-if="description">{{ getPropertyById(12) }}</p>
  </div>
</template>

<script>

export default {
  name: "Sort",
  props: {
    id: {
      type: String,
      required: true
    }
  },
  data () {
    return {
      sort: this.getSortByName(this.id),
      description: false
    }
  },
  methods : {
    getSortByName(id) {
      return this.$parent.sorts.filter(sort => sort[1] === id)[0];
    },
    getPropertyById(id) {
      return this.sort[id];
    },
    showDescription() {
      this.description = !this.description;
    }
  }
};
</script>

<style scoped>
  h2 {
    color: green;
  }
  h3, p {
    color: white;
  }
</style>
