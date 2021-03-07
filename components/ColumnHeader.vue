<template>
  <div class="columnName" :style="cssVars">{{ name }}</div>
</template>

<style scoped>
.columnName {
  border: #FFFF 1px solid;
  padding: 0em;
  margin: 0px;
  grid-column: var(--grid-column);
}
</style>

<script>
export default {
  props: {
    gridColumn: {
      type: Number
    },
    name: {
      type: String
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column": this.gridColumn
      };
    }
  }
};
</script>
