<template>
  <div class="card">
    <div class="card-header text-center">{{ getPropertyById(1) }}</div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item"><b>Livre :</b> {{ getPropertyById(0) }}</li>
      <li class="list-group-item"><b>École :</b> {{ getPropertyById(2) }}</li>
      <li class="list-group-item"><b>Branches :</b> {{ getPropertyById(3).join(", ") || "∅" }}</li>
      <li class="list-group-item"><b>Classes :</b> {{ getPropertyById(4).join(" / ") || "∅" }}</li>
      <li class="list-group-item"><b>Composantes :</b> {{ getPropertyById(5).join(", ") || "∅" }}</li>
      <li class="list-group-item description" v-on:click="showDescription()"><b>Description</b><br>
        <span v-if="description" v-html="getPropertyById(12)"></span>
      </li>
    </ul>
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
    //Récupération du sort par son identifiant
    getSortByName(id) {
      return this.$parent.sorts.filter(sort => sort[1] === id)[0];
    },
    //Récupération d'une propriété d'un sort
    getPropertyById(id) {
      return this.sort[id];
    },
    //Autorisation de l'affichage de la description
    showDescription() {
      this.description = !this.description;
    }
  }
};
</script>

<style scoped>
  .card {
    width: 28em;
    margin: 1em;
  }
  .card-header {
    color: green;
    font-weight: 700;
    font-size: 1.4em;
  }
  .description {
    color: green;
    cursor: pointer;
  }
  span {
    color: #000;
  }
</style>
