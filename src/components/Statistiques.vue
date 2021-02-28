<template>
  <table class="table table-striped table-light text-center mx-auto"><thead><tr>
        <th>Nombre de sorts</th>
        <th>Nombre de branches</th>
        <th>Niveau minimum</th>
        <th>Niveau maximum</th>
        <th>Nombre de composantes</th>
    </tr></thead>
    <tbody><tr>
        <td>{{ numberOfSorts }}</td>
        <td>{{ numberOfBranches }}</td>
        <td>{{ minimumLevel }}</td>
        <td>{{ maximumLevel }}</td>
        <td>{{ numberOfComposantes }}</td>
    </tr></tbody>
  </table>
</template>

<script>
export default {
  name: "Statistiques",
  data() {
    return {
      sorts: []
    }
  },
  methods: {
    getSearchedSorts() {
      this.sorts = this.$parent.$refs.recherche.$refs.table.sorts;
    }
  },
  computed: {
    numberOfSorts() {
      return this.sorts.length;
    },
    numberOfBranches() {
      let allBranches = [];

      this.sorts.forEach(sort => {
        let branches = sort[3];
        branches.forEach(branche => {
          if (!allBranches.includes(branche)) allBranches.push(branche);
        });
      });

      return allBranches.length;
    },
    minimumLevel() {
      let minimumLevel = 9;
      
      this.sorts.forEach(sort => {
        let classes = sort[4];
        classes.forEach(classe => {
          if (classe[1] < minimumLevel) minimumLevel = classe[1];
        });
      });

      return minimumLevel;
    },
    maximumLevel() {
      let maximumLevel = 0;
      
      this.sorts.forEach(sort => {
        let classes = sort[4];
        classes.forEach(classe => {
          if (classe[1] > maximumLevel) maximumLevel = classe[1];
        });
      });

      return maximumLevel;
    },
    numberOfComposantes() {
      let allComposantes = [];

      this.sorts.forEach(sort => {
        let composantes = sort[5];
        composantes.forEach(composant => {
          if (!allComposantes.includes(composant)) allComposantes.push(composant);
        });
      });

      return allComposantes.length;
    }
  }
};
</script>

<style scoped>
  table {
    width: 65em;
    margin-top: 10em;
    font-size: 1.1em;
  }
</style>
