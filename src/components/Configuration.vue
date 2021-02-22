<template>
  <form id="config">
    <Select id="livresDispo" label="Livres disponibles :" v-bind:values="livresDisponibles" buttonName="Ajouter" onClickMethod="addBook"></Select>
    <Select multiple="true" id="livresAjoutes" label="Livres ajoutés :" v-bind:values="livresAjoutes" buttonName="Retirer" onClickMethod="removeBook"></Select>
    <Select id="ecoles" label="École :" v-bind:values="ecoles" onChangeMethod="storeSchool"></Select>
    <TextInput id="niveauMin" label="Niveau minimum :" v-bind:value="niveauMinimum" placeholder="0" onInputMethod="storeMinimumLevel"></TextInput>
    <TextInput id="niveauMax" label="Niveau maximum :" v-bind:value="niveauMaximum" placeholder="9" onInputMethod="storeMaximumLevel"></TextInput>
  </form>
</template>

<script>
import { sortTable } from '../assets/data.min.js'
import Select from "./Select.vue";
import TextInput from "./TextInput.vue";

export default {
  name: "Configuration",
  components: {
    Select,
    TextInput
  },
  data() {
    return {
      livresDisponibles: this.initAvailableBooks(),
      livresAjoutes: this.initAddedBooks(),
      ecoles: this.initSchools(),
      niveauMinimum: this.initMinimumLevel(),
      niveauMaximum: this.initMaximumLevel()
    }
  },
  methods: {
    getAvailableBooks() {
      let books = []; // Tableau contenant le nom des livres disponibles
      sortTable.forEach(sort => {
        if (!books.includes(sort[0])) // Si le livre n'a pas déjà été enregistré (évite les doublons)
          books.push(sort[0]);
      });
      return books;
    },
    initAvailableBooks() {
      let availableBooks = JSON.parse(localStorage.getItem("livresDisponibles"));
      if (!availableBooks) {
        availableBooks = this.getAvailableBooks();
        localStorage.setItem("livresDisponibles", JSON.stringify(availableBooks));
      }
      return availableBooks;
    },
    initAddedBooks() {
      let addedBooks = JSON.parse(localStorage.getItem("livresAjoutes"));
      if (!addedBooks) {
        addedBooks = [];
      }
      return addedBooks;
    },
    addBook(bookName) {
      if (this.livresDisponibles.includes(bookName) && !this.livresAjoutes.includes(bookName)) { // Si le livre est disponible et n'a pas été ajouté
        this.livresDisponibles.splice(this.livresDisponibles.indexOf(bookName), 1); // On le retire du tableau des livres disponibles
        this.livresAjoutes.push(bookName); // On l'ajoute dans le tableau des livres ajoutés
        localStorage.setItem("livresDisponibles", JSON.stringify(this.livresDisponibles));
        localStorage.setItem("livresAjoutes", JSON.stringify(this.livresAjoutes));
      }
    },
    removeBook(bookName) {
      if (this.livresAjoutes.includes(bookName) && !this.livresDisponibles.includes(bookName)) { // Si le livre a été ajouté et n'est pas disponible
        this.livresAjoutes.splice(this.livresAjoutes.indexOf(bookName), 1); // On le retire du tableau des livres ajoutés
        this.livresDisponibles.push(bookName); // On l'ajoute dans le tableau des livres disponibles
        localStorage.setItem("livresAjoutes", JSON.stringify(this.livresAjoutes));
        localStorage.setItem("livresDisponibles", JSON.stringify(this.livresDisponibles));
      }
    },
    getSchools() {
      let schools = []; // Tableau contenant le nom des différentes écoles
      sortTable.forEach(sort => {
        if (!schools.includes(sort[2])) // Si l'école n'a pas déjà été enregistrée (évite les doublons)
          schools.push(sort[2]);
      });
      return schools;
    },
    initSchools() {
      let schools = JSON.parse(localStorage.getItem("ecoles"));
      if (!schools) {
        schools = this.getSchools();
        localStorage.setItem("ecoles", JSON.stringify(schools));
      }
      return schools;
    },
    storeSchool(selectedSchool) {
      this.ecoles.splice(this.ecoles.indexOf(selectedSchool), 1);
      this.ecoles.unshift(selectedSchool);
      localStorage.setItem("ecoles", JSON.stringify(this.ecoles));
    },
    initMinimumLevel() {
      return localStorage.getItem("niveauMin") || 0;
    },
    storeMinimumLevel(level) {
      this.niveauMinimum = level;
      localStorage.setItem("niveauMin", this.niveauMinimum);
    },
    initMaximumLevel() {
      return localStorage.getItem("niveauMax") || 9;
    },
    storeMaximumLevel(level) {
      this.niveauMaximum = level;
      localStorage.setItem("niveauMax", this.niveauMaximum);
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
