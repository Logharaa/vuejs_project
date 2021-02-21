<template>
  <form id="config">
    <Select id="livresDispo" name="Livres disponibles :" v-bind:values="livresDisponibles" buttonName="Ajouter" onClickMethod="addBook"></Select>
    <Select id="livresAjoutes" name="Livres ajoutés :" v-bind:values="livresAjoutes" buttonName="Retirer" onClickMethod="removeBook"></Select>
    <Select id="ecole" name="École :" v-bind:values="ecole"></Select>
    <div class="form-group row">
      <label for="niveauMin" class="col-sm-2 col-form-label">Niveau minimum :</label>
      <input type="text" class="col-sm-1 form-control" id="niveauMin" placeholder="0" />
    </div>
    <div class="form-group row">
      <label for="niveauMax" class="col-sm-2 col-form-label">Niveau maximum :</label>
      <input type="text" class="col-sm-1 form-control" id="niveauMax" placeholder="9" />
    </div>
  </form>
</template>

<script>
import Select from "./Select.vue";
import { sortTable } from '../assets/data.min.js'

export default {
  name: "Configuration",
  components: {
    Select
  },
  data() {
    return {
      livresDisponibles: this.initAvailableBooks(),
      livresAjoutes: [],
      ecole: this.initSchools(),
      niveauMinimum: 2
    }
  },
  methods: {
    initAvailableBooks() {
      let books = []; // Tableau contenant le nom des livres disponibles
      sortTable.forEach(sort => {
        if (!books.includes(sort[0])) // Si le livre n'a pas déjà été enregistré (évite les doublons)
          books.push(sort[0]);
      });
      return books;
    },
    addBook(bookName) {
      if (this.livresDisponibles.includes(bookName) && !this.livresAjoutes.includes(bookName)) { // Si le livre est disponible et n'a pas été ajouté
        this.livresDisponibles.splice(this.livresDisponibles.indexOf(bookName), 1); // On le retire du tableau des livres disponibles
        this.livresAjoutes.push(bookName); // On l'ajoute dans le tableau des livres ajoutés
      }
    },
    removeBook(bookName) {
      if (this.livresAjoutes.includes(bookName) && !this.livresDisponibles.includes(bookName)) { // Si le livre a été ajouté et n'est pas disponible
        this.livresAjoutes.splice(this.livresAjoutes.indexOf(bookName), 1); // On le retire du tableau des livres ajoutés
        this.livresDisponibles.push(bookName); // On l'ajoute dans le tableau des livres disponibles
      }
    },
    initSchools() {
      let schools = []; // Tableau contenant le nom des différentes écoles
      sortTable.forEach(sort => {
        if (!schools.includes(sort[2])) // Si l'école n'a pas déjà été enregistrée (évite les doublons)
          schools.push(sort[2]);
      });
      return schools;
    }
  }
};
</script>

<style scoped>
#config {
  padding: 4em;
  font-size: 1.1em;
  color: white;
}
</style>
