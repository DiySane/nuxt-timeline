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
    <v-card class="px-3" ref="form" style="grid-row: 2/5; grid-column: 1/3;">
      <v-card color="#607D8B">
        <v-col>
          <v-row justify="center">
            <v-text-field
              label="Row Name"
              v-model="rowName"
              prepend-icon="mdi-pencil"
            ></v-text-field>
          </v-row>
          <v-row justify="center" style="padding-bottom: 10px;">
            <v-menu offset-y>
              <template v-slot:activator="{ on }">
                <v-btn :color="rowColor" dark v-on="on">
                  Row Color
                </v-btn>
              </template>
              <v-color-picker
                v-model="rowColor"
                hide-inputs
                class="mx-auto"
              ></v-color-picker>
            </v-menu>
          </v-row>
          <v-row justify="center" style="padding-bottom: 10px;">
            <v-btn @click="emitRow"> Submit</v-btn></v-row
          >
        </v-col>
        <v-spacer></v-spacer>
      </v-card>
      <v-divider></v-divider>
      <v-divider></v-divider>
      <v-divider></v-divider>
      <v-card color="#607D8B" hover>
        <v-col>
          <DateRangePicker @emitDateRange="acceptDateRange" />
          <v-btn @click="emitColumn"> Submit</v-btn>
        </v-col>
      </v-card>
    </v-card>
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
      rowColor: "#00000",
      rowId: 0,
      startDate: "",
      endDate: "",
      columnSpan: 7,
      showColPicker: false,
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
      this.rowColor = "#00000";
    },
    emitColumn() {
      this.$emit("addColumn", {
        startDate: this.startDate,
        endDate: this.endDate,
        columnSpan: this.columnSpan
      });
    },
    acceptDateRange(dateRange) {
      this.startDate = dateRange.startDate;
      this.endDate = dateRange.endDate;
      this.columnSpan = dateRange.columnSpan;
    }
  }
};
</script>
