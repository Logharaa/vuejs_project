<template>
  <div id="content" class="container" v-bind:is="readContent">
    {{ content }}
  </div>
</template>

<script>

export default {
  name: "Content",
  props: ['content'],
  computed: {
    readContent() {
      let data = this.canvas.split('/')[2];
      return () => import(`./components/${data}`);
    }
  }
};
</script>

<style scoped>

</style>
