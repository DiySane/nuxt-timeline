<template>
  <div class="row" :style="cssVars"
   >
    <div class="row-label">{{ name }}</div>
    <Task
      v-for="node in nodes"
      :key="node.name"
      :name="node.name"
      :start="node.start"
      :end="node.end"
      :color="getNodeColor(node)"
      :complete="node.complete"
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
    nodes: {
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
  methods: {
    getNodeColor(node) {
      if(node.color == undefined || node.color == null) {
        return this.color;
      } else {
        return node.color;
      }
    }
  }
};
</script>
