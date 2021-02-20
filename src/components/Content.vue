<template>
  <div id="content">
    <Configuration></Configuration>
  </div>
  <!--<div id="content" class="container" v-bind:is="readContent">
    {{ content }}
  </div>-->
</template>

<script>
import Configuration from "./Configuration.vue";

export default {
  name: "Content",
  /*props: ['content'],
  computed: {
    readContent() {
      let data = this.canvas.split('/')[2];
      return () => import(`./components/${data}`);
    }
  },*/
  components: {
    Configuration
  }
};
</script>

<style scoped>
#content {
  background-color: #20262c;
}
</style>
