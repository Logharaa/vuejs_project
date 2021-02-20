<template>
  <nav class="navbar navbar-dark bg-dark">
    <div class="container">
      <a class="navbar-brand" href="index.html"><img src="d&d.png" alt="D&D" width="60" height="60" class="d-inline-block align-top"></a>
      <a class="nav-link" href="#"><i class="nav-icon fas fa-cog"></i>Configuration</a>
      <a class="nav-link" href="#"><i class="nav-icon fas fa-search"></i>Recherche</a>
      <a class="nav-link" href="#"><i class="nav-icon fas fa-chart-pie"></i>Statistiques</a>
    </div>
  </nav>
</template>

<script>
export default {
  name: "Navbar"
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
  color: #EC2127;
}
</style>
