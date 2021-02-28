<template>
    <div class="form-group row">
      <label v-bind:for="id" class="col-sm-2 col-form-label">{{ label }}</label>
      <input type="text" class="col-sm-1 form-control" v-bind:id="id" v-bind:value="value" v-bind:placeholder="placeholder" v-on:input="onInput()" />
    </div>
</template>

<script>
export default {
  name: "TextInput",
  props: {
    id: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    value: {
      type: [Number, String],
      required: false
    },
    placeholder: {
      type: String,
      required: false
    },
    onInputMethod: {
      type: String,
      required: false
    }
  },
  methods: {
    // Méthode qui va appeler la méthode du composant parent dont le nom est passé en props lorsque l'input HTML est édité
    onInput() {
      if (this.onInputMethod) {
        this.$parent[this.onInputMethod](document.getElementById(this.id).value);
      }
    }
  }
};
</script>

<style scoped></style>