<template>
  <div>
    <h2>{{ getPropertyById(1) }}</h2>
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
      sort: this.getSortByName(this.id)
    }
  },
  methods : {
    getSortByName(id) {
      return this.$parent.sorts.filter(sort => sort[1] === id)[0];
    },
    getPropertyById(id) {
      return this.sort[id];
    }
  }
};
</script>

<style scoped>
  div {
    color: green;
  }
</style>
