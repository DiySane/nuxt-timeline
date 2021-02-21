<template>
  <div class="row">
    <div class="row-label">Columns</div>
    <ColumnHeader :name="'Sun'" :gridColumn="2" />
    <ColumnHeader :name="'Mon'" :gridColumn="3" />
    <ColumnHeader :name="'Tue'" :gridColumn="4" />
    <ColumnHeader :name="'Wed'" :gridColumn="5" />
    <ColumnHeader :name="'Thu'" :gridColumn="6" />
    <ColumnHeader :name="'Fri'" :gridColumn="7" />
    <ColumnHeader :name="'Sat'" :gridColumn="8" />
  </div>
</template>

<style scoped>
.row {
  display: grid;
  grid-template-columns: 100px repeat(7, 1fr);
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
export default {};
</script>
