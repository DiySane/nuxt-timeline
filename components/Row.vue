<template>
  <div class="row" :style="cssVars">
    <div class="row-label">{{ name }}</div>
    <!-- <Task :name="'task1'" :start="2" :end="3" :color="color" :complete="0.3" />
    <Task :name="'task2'" :start="4" :end="5" :color="color" :complete="0.5" />
    <Task :name="'task3'" :start="3" :end="6" :color="color" :complete="0.5" />
    <Task :name="'task4'" :start="7" :end="8" :color="color" :complete="0.5" /> -->
    <Task :name="'task1'" :start="2" :end="3" :color="color" :complete="0.3" />
    <Task :name="'task2'" :start="4" :end="5" :color="color" :complete="0.5" />
    <Task :name="'task3'" :start="3" :end="6" :color="color" :complete="0.5" />
    <Task :name="'task4'" :start="7" :end="8" :color="color" :complete="0.5" />
  </div>
</template>

<style lang="css" scoped>
/* ul {
  list-style-type: none;
 } */
.row {
  display: grid;
  grid-template-columns: 100px repeat(var(--grid-column-span), 1fr);
  grid-gap: 0.1em;
  padding: 0em;
  margin: 0px;
  border-top: 1px solid black;
  border-bottom: 1px solid black;
  /* list-style: none; */
}
.row-label {
  grid-column: 1/2;
  /* border: #333 1px solid; */
  /* padding: 0em; */
  grid-row: auto;
  /* padding: 30px 0; */
  margin: 0px;

  /* border-width: 1px 0 0 0;
  border-color: rgba(0, 0, 0, 0.1);
  border-style: solid;
  padding: 15px 0;
  font-size: 13px;
  font-weight: bold;
  text-align: center;
  background-color: #f5f5f5; */
  /* column-rule-style: solid;
  column-rule-color: #ff0000; */
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
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column-span": this.gridColumnSpan
      };
    }
  }
};
</script>
