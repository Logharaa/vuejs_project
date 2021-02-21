<template>
  <div id="content">
    <Configuration v-show="getContent() === 'configuration'"></Configuration>
    <Recherche v-show="getContent() === 'recherche'"></Recherche>
    <Statistiques v-show="getContent() === 'statistiques'"></Statistiques>
  </div>
</template>

<script>
import Configuration from "./Configuration.vue";
import Recherche from "./Recherche.vue";
import Statistiques from "./Statistiques.vue";

export default {
  name: "Content",
  components: {
    Configuration,
    Recherche,
    Statistiques
  },
  methods : {
    getContent() {
      return this.$parent.content;
    }
  }
};
</script>

<style scoped>
#content {
  background-color: #20262c;
}
</style>
