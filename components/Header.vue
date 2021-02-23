<template>
  <div class="row" :style="cssVars">
    <div class="row-label">Columns</div>
    <div v-for="i in columnSpan" :key="i">
      <ColumnHeader :name="i" :gridColumn="i+1"/>
    </div> 
    <!-- <ColumnHeader :name="'Sun'" :gridColumn="2" />
    <ColumnHeader :name="'Mon'" :gridColumn="3" />
    <ColumnHeader :name="'Tue'" :gridColumn="4" />
    <ColumnHeader :name="'Wed'" :gridColumn="5" />
    <ColumnHeader :name="'Thu'" :gridColumn="6" />
    <ColumnHeader :name="'Fri'" :gridColumn="7" />
    <ColumnHeader :name="'Sat'" :gridColumn="8" /> -->
  </div>
</template>

<style scoped>
.row {
  display: grid;
  grid-template-columns: 100px repeat(var(--grid-column-span), 1fr);
  grid-gap: 0.1em;
  padding: 0em;
  margin: 0px;
  color: #fff;
  background-color: #0a3444 !important;
  border-bottom: 1px solid rgba(0, 0, 0, 0.1);
  text-align: center;
  /* grid-template-columns: 150px repeat(12, 1fr); */
}
.row-label {
  grid-column: 1/2;
  /*   border:#333 1px solid; */
  padding: 0em;
  margin: 0px;
}
</style>

<script>
import ColumnHeader from "@/components/ColumnHeader";
export default {
  props: {
    columnSpan: {
      type: Number
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column-span": this.columnSpan
      };
    }
  }
};
</script>
