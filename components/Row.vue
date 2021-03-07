<template>
  <div class="row" :style="cssVars"
   >
    <div class="row-label">{{ name }}</div>
    <Task
      v-for="task in tasks"
      :key="task.name"
      :name="task.name"
      :start="task.start"
      :end="task.end"
      :color="color"
      :complete="task.complete"
    />
  </div>
</template>

<style lang="css" scoped>
.row {
  display: grid;
  grid-template-columns: 100px repeat(var(--grid-column-span), 1fr);
  grid-gap: 0.1em;
  padding: 0em;
  margin: 0px;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
}
.row-label {
  grid-column: 1/2;
  grid-row: auto;
  margin: 0px;
}
</style>

<script>
import Task from "@/components/Task";
export default {
  props: {
    gridColumnSpan: {
      type: Number
    },
    name: {
      type: String
    },
    color: {
      type: String
    },
    tasks: {
      type: Array
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column-span": this.gridColumnSpan
      };
    }
  },
};
</script>
