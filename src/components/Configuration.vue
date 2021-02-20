<template>
  <form id="config">
    <div class="form-group row">
      <label for="livresDispo" class="col-sm-2 col-form-label">Livres disponibles :</label>
      <select class="col-sm-2 custom-select mr-sm-2" id="livresDispo">
        <option>Livre 1</option>
        <option>Livre 2</option>
      </select>
      <input type="button" class="btn btn-success my-1" value="Sélectionner">
    </div>

    <div class="form-group row">
      <label for="livresSelect" class="col-sm-2 col-form-label">Livres séléctionnés :</label>
      <select class="col-sm-2 custom-select mr-sm-2" id="livresSelect">
        <option>Livre 1</option>
        <option>Livre 2</option>
      </select>
      <input type="button" class="btn btn-danger my-1" value="Retirer">
    </div>

    <div class="form-group row">
      <label for="ecole" class="col-sm-2 col-form-label">École :</label>
      <select class="col-sm-2 custom-select mr-sm-2" id="ecole">
        <option>École 1</option>
        <option>École 2</option>
      </select>
    </div>

    <div class="form-group row">
      <label for="niveau" class="col-sm-2 col-form-label">Niveau minimum :</label>
    <input type="text" class="col-sm-1 form-control" id="niveau" placeholder="2" />
    </div>
  </form>
</template>

<script>
export default {
  name: "Configuration"
};
</script>

<style scoped>
#config {
  padding: 4em;
  font-size: 1.1em;
  color: white;
}
</style>
