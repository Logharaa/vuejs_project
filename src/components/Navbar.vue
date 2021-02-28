<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container">
      <a class="navbar-brand"><img src="d&d.png" alt="D&D" width="60" height="60" class="d-inline-block align-top"></a>
      <a class="nav-link" v-on:click="changeContent('configuration')"><i class="nav-icon fas fa-cog"></i>Configuration</a>
      <a class="nav-link" v-on:click="changeContent('recherche')"><i class="nav-icon fas fa-search"></i>Recherche</a>
      <a class="nav-link" v-on:click="changeContent('statistiques')"><i class="nav-icon fas fa-chart-pie"></i>Statistiques</a>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar",
  props: {

  },
  methods: {
    changeContent (content) {
      this.$parent.content = content;
      if (content === "recherche" || content === "statistiques") {
        this.$parent.$refs.content.$refs.recherche.$refs.table.getSortsByConf();
        this.$parent.$refs.content.$refs.statistiques.getSearchedSorts();
      }
    }
  }
};
</script>

<style scoped>
a {
  color: white;
  font-size: 1.2em;
}

a i {
  padding: 0.5em;
}

a:hover {
  cursor: pointer;
  color: #EC2127;
}
</style>
