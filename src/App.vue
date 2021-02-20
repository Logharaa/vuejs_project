<template>
  <div id="app">
    <Navbar></Navbar>
    <Content canvas="./components/navbar"></Content>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Content from "./components/Content.vue"

export default {
  name: "App",
  components: {
    Navbar,
    Content
  }
};
</script>

<style>
#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
