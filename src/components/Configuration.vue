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
          books.push(sort[0]); // On ajoute son nom dans le tableau
      });
      return books;
    },
    initAvailableBooks() {
      let availableBooks = JSON.parse(localStorage.getItem("livresDisponibles")); // On essaye de récupérer le tableau des livres disponibles sauvegardé dans le storage
      if (!availableBooks) { // Si ce tableau n'a pas encore été sauvegardé
        availableBooks = this.getAvailableBooks(); // On le récupère via le fichier data.min.js
        localStorage.setItem("livresDisponibles", JSON.stringify(availableBooks)); // Et on l'enregistre dans le storage
      }
      return availableBooks;
    },
    initAddedBooks() {
      return JSON.parse(localStorage.getItem("livresAjoutes")) || []; // On renvoie le tableau des livres ajoutés sauvegardé dans le storage, ou un tableau vide s'il n'a pas encore été sauvegardé
    },
    addBook(bookName) {
      if (this.livresDisponibles.includes(bookName) && !this.livresAjoutes.includes(bookName)) { // Si le livre est disponible et n'a pas été ajouté
        this.livresDisponibles.splice(this.livresDisponibles.indexOf(bookName), 1); // On le retire du tableau des livres disponibles
        this.livresAjoutes.push(bookName); // On l'ajoute dans le tableau des livres ajoutés
        localStorage.setItem("livresDisponibles", JSON.stringify(this.livresDisponibles)); // On sauvegarde le nouveau tableau des livres disponibles dans le storage
        localStorage.setItem("livresAjoutes", JSON.stringify(this.livresAjoutes)); // On sauvegarde le nouveau tableau des livres ajoutés dans le storage
      }
    },
    removeBook(bookName) {
      if (this.livresAjoutes.includes(bookName) && !this.livresDisponibles.includes(bookName)) { // Si le livre a été ajouté et n'est pas disponible
        this.livresAjoutes.splice(this.livresAjoutes.indexOf(bookName), 1); // On le retire du tableau des livres ajoutés
        this.livresDisponibles.push(bookName); // On l'ajoute dans le tableau des livres disponibles
        localStorage.setItem("livresAjoutes", JSON.stringify(this.livresAjoutes)); // On sauvegarde le nouveau tableau des livres ajoutés dans le storage
        localStorage.setItem("livresDisponibles", JSON.stringify(this.livresDisponibles)); // On sauvegarde le nouveau tableau des livres disponibles dans le storage
      }
    },
    getSchools() {
      let schools = []; // Tableau contenant le nom des différentes écoles
      sortTable.forEach(sort => {
        if (!schools.includes(sort[2])) // Si l'école n'a pas déjà été enregistrée (évite les doublons)
          schools.push(sort[2]); // On ajoute son nom dans le tableau
      });
      return schools;
    },
    initSchools() {
      let schools = JSON.parse(localStorage.getItem("ecoles")); // On essaye de récupérer le tableau des écoles sauvegardé dans le storage
      if (!schools) { // Si ce tableau n'a pas encore été sauvegardé
        schools = this.getSchools(); // On le récupère via le fichier data.min.js
        localStorage.setItem("ecoles", JSON.stringify(schools)); // Et on l'enregistre dans le storage
      }
      return schools;
    },
    storeSchool(selectedSchool) {
      this.ecoles.splice(this.ecoles.indexOf(selectedSchool), 1); // On retire l'école du tableau
      this.ecoles.unshift(selectedSchool); // Et on la remet à la première place du tableau (pour que ce soit celle séléctionnée)
      localStorage.setItem("ecoles", JSON.stringify(this.ecoles)); // On sauvegarde le nouveau tableau des écoles dans le storage
    },
    initMinimumLevel() {
      return localStorage.getItem("niveauMin") || 0; // On renvoie le niveau minimum sauvegardé dans le storage, ou 0 s'il n'a pas encore été sauvegardé
    },
    storeMinimumLevel(level) {
      this.niveauMinimum = level; // On met à jour le niveau minimum
      localStorage.setItem("niveauMin", this.niveauMinimum); // On sauvegarde le nouveau niveau minimum
    },
    initMaximumLevel() {
      return localStorage.getItem("niveauMax") || 9; // On renvoie le niveau maximum sauvegardé dans le storage, ou 9 s'il n'a pas encore été sauvegardé
    },
    storeMaximumLevel(level) {
      this.niveauMaximum = level; // On met à jour le niveau maximum
      localStorage.setItem("niveauMax", this.niveauMaximum); // On sauvegarde le nouveau niveau maximum
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
