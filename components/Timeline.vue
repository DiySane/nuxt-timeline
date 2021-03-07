<template>
  <div class="timeline">
    <Header :startDate="startDate" :endDate="endDate" :columnSpan="columnSpan" />
    <div v-for="row in rows" :key="row.name" @click="selectRow(row)">
      <Row
        :gridColumnSpan="columnSpan"
        :name="row.name"
        :color="row.color"
        :nodes="row.nodes"
      />
    </div>
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
export default {
  props: {
    rows: {
      type: Array,
      required: true
    },
    startDate: {
      type: String
    },
    endDate: {
      type: String
    },
    columnSpan: {
      type: Number
    }
  },
  methods: {
    selectRow(row) {
      this.$emit("emitSelectedRow", row);
      console.log(row);
    },
    acceptSelectedRow(row) {
      this.selectRow(row);
    }
  }
};
</script>
