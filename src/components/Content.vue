<template>
  <div id="content">
    <Configuration v-show="getContent() === 'configuration'"></Configuration>
    <Recherche ref="recherche" v-show="getContent() === 'recherche'"></Recherche>
    <Statistiques ref="statistiques" v-show="getContent() === 'statistiques'"></Statistiques>
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
    //Récupération du contenu de la page
    getContent() {
      return this.$parent.content;
    }
  }
};
</script>

<style scoped>
#content {
  flex: 1 1 auto;
  background-color: #20262c;
}
</style>
