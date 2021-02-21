<template>
  <div class="timeline">
    <Header />
    <Row :gridColumnSpan="7" :name="'row1'" :color="'#ffa07a'" />
    <!-- <Row :gridColumnSpan='7' :name="'row1'" :color="'red'"/> -->
    <Row :gridColumnSpan="7" :name="'row2'" :color="'#fbec5d'" />
    <Row :gridColumnSpan="7" :name="'row3'" :color="'#33a8a5'" />
  </div>
</template>

<style scoped>
.timeline {
  display: grid;
  grid-template-columns: 1fr;
  grid-gap: 5px;
  padding: 0em;
  margin: 0px;
  background-color: #e7feff;
  border: 0;
  border-radius: 12px;
  position: relative;
  overflow: hidden;
  box-sizing: border-box;
  box-shadow: 0 75px 125px -57px #7e8f94;
}
</style>

<script>
import Header from "@/components/Header";
import Row from "@/components/Row";
export default {};
</script>
