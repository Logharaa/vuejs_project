<template>
    <div class="form-group row">
      <label v-bind:for="id" class="col-sm-2 col-form-label">{{ name }}</label>
      <select class="col-sm-2 custom-select mr-sm-2" v-bind:id="id">
        <option v-for="value in values" v-bind:key="value" v-bind:value="value">{{ value }}</option>
      </select>
      <input v-if="buttonName" type="button" class="btn btn-info my-1" v-bind:value="buttonName" v-on:click="onClick()">
    </div>
</template>

<script>
export default {
  name: "Select",
  props: {
    id: {
      type: String,
      required: true
    },
    name: {
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
    onClickMethod: {
      type: String,
      required: false
    }
  },
  methods: {
    onClick() {
      this.$parent[this.onClickMethod](document.getElementById(this.id).value);
    }
  }
};
</script>

<style scoped></style>