<template>
    <div class="form-group row">
      <label v-bind:for="id" class="col-sm-2 col-form-label">{{ label }}</label>
      <select v-bind:multiple="multiple" class="col-sm-3 custom-select mr-sm-2" v-bind:id="id" v-on:change="onChange()">
        <option v-for="value in values" v-bind:key="value" v-bind:value="value">{{ value }}</option>
      </select>
      <input v-if="buttonName" type="button" class="btn btn-info my-1 h-25" v-bind:value="buttonName" v-on:click="onClick()" />
    </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    multiple: {
      type: [Boolean, String],
      required: false
    },
    id: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    values: {
      type: Array,
      required: false
    },
    buttonName: {
      type: String,
      required: false
    },
    onChangeMethod: {
      type: String,
      required: false
    },
    onClickMethod: {
      type: String,
      required: false
    },
  },
  methods: {
    // Appel de la méthode du composant parent dont le nom est passé en props lorsque la valeur du select HTML est modifiée
    onChange() {
      if (this.onChangeMethod) {
        this.$parent[this.onChangeMethod](document.getElementById(this.id).value);
      }
    },
    // Appel de la méthode du composant parent dont le nom est passé en props lorsque l'on clique sur le bouton HTML
    onClick() {
      if (this.onClickMethod) {
        this.$parent[this.onClickMethod](document.getElementById(this.id).value);
      }
    }
  }
};
</script>

<style scoped></style>