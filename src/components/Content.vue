<template>
  <div id="content">
    <Recherche v-if="getContent() === 'recherche'"></Recherche>
    <Statistiques v-else-if="getContent() === 'statistiques'"></Statistiques>
    <Configuration v-else></Configuration>
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
