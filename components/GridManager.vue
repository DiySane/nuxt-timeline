<template>
  <v-card
    color="blue-grey darken-4"
    class="service-item"
    style="grid-row: 1/2; grid-column: 4/5; display: grid; grid-template-columns: repeat(2, 1fr); grid-template-rows: repeat(4, 1fr); grid-gap: 5px; background-color: #f2f4f7;"
  >
    <v-card-title
      style="grid-row: 1/2; grid-column: 1/3; color: white; text-align: center;"
    >
      GRID MANAGER
    </v-card-title>
    <v-form class="px-3" ref="form" style="grid-row: 2/5; grid-column: 1/3;">
      <v-text-field
        label="Row Name"
        v-model="rowName"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-text-field
        label="Row Color"
        v-model="rowColor"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-row>
        <DateRangePicker @emitDateRange="acceptDateRange" />
      </v-row>
      <v-btn @click="emitRow"> Submit</v-btn>
    </v-form>
  </v-card>
</template>

<style lang="css" scoped>
.service-item {
  padding: 5px;
  text-align: center;
  border-top: 1px solid #3e2723;
  border-bottom: 1px solid #3e2723;
  border-left: 1px solid #3e2723;
  border-right: 1px solid #3e2723;
  min-width: 20px;
  min-height: 30px;
  color: black;
}
</style>

<script>
import DateRangePicker from "@/components/DateRangePicker";
export default {
  data() {
    return {
      rowName: "",
      rowColor: "",
      rowId: 0,
      startDate: "",
      endDate: "",
      columnSpan: 7
    };
  },
  methods: {
    emitRow() {
      this.$emit("addRow", {
        name: this.rowName,
        color: this.rowColor,
        id: this.rowId++
      });
      this.rowName = "";
      this.rowColor = "";
    },
    acceptDateRange(dateRange) {
      this.startDate = dateRange.startDate;
      this.endDate = dateRange.endDate;
      this.columnSpan = dateRange.columnSpan;
      this.$emit("emitDateRange", {
        startDate: dateRange.startDate,
        endDate: dateRange.endDate,
        columnSpan: dateRange.columnSpan
      });
    }
  }
};
</script>
