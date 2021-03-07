<template>
  <v-card
    color="blue-grey darken-4"
    class="service-item"
    style="grid-row: 1/2; grid-column: 4/5; display: grid; grid-template-columns: repeat(2, 1fr); grid-template-rows: repeat(4, 1fr); grid-gap: 5px; background-color: #f2f4f7;"
  >
    <v-card-title
      style="grid-row: 1/2; grid-column: 1/3; color: white; text-align: center;"
    >
      TASK MANAGER
    </v-card-title>
    <v-card class="px-3" ref="form" style="grid-row: 2/5; grid-column: 1/3;">
      <v-card color="#607D8B">
        <v-col>
          <v-text-field
            text-color="black"
            label="Task Name"
            v-model="name"
            prepend-icon="mdi-pencil"
            style="caret-color: black;"
          ></v-text-field>
          <DateRangePicker @emitDateRange="acceptDateRange" />
          <v-text-field
            label="Row"
            v-model="rowName"
            prepend-icon="mdi-pencil"
          ></v-text-field>
          <v-text-field
            label="Color"
            v-model="color"
            prepend-icon="mdi-pencil"
          ></v-text-field>
          <v-btn @click="emitNode" :disabled="submitDisabled"> Submit</v-btn>
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
      title: "",
      name: "",
      startDate: "",
      endDate: "",
      row: "",
      color: "",
      subRow: "",
      due: null,
      menu: false,
      loading: false,
      id: 0
    };
  },
  methods: {
    emitNode() {
      this.$emit("addNode", {
        name: this.name,
        startDate: this.startDate,
        endDate: this.endDate,
        color: this.color,
        id: this.id++
      });
    },
    acceptDateRange(dateRange) {
      this.startDate = dateRange.startDate;
      this.endDate = dateRange.endDate;
    }
  },
  props: {
    selectedRow: {
      type: Object
    }
  },
  computed: {
    rowName() {
      return this.selectedRow != null ? this.selectedRow.name : "";
    },
    submitDisabled() {
      return this.selectedRow == null;
    }
  }
};
</script>
