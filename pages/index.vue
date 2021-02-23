<template>
  <!-- <div style="display: grid; grid-template-columns: repeat(2, 1fr);">
    <Timeline style="grid-column: 1/2"/>
    <TaskManager style="grid-column: 2/3"/>
  </div> -->
  <v-container>
    <v-row>
      <v-col> <Timeline :columnSpan="columnSpan" :rows="rows" @emitDateRange="acceptDateRange"/></v-col>
    </v-row>
    <v-row>
      <v-col>
        <TaskManager />
      </v-col>
      <v-col>
        <GridManager @addRow="acceptRow"  @emitDateRange="acceptDateRange"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Timeline from "@/components/Timeline";
import TaskManager from "@/components/TaskManager";
import GridManager from "@/components/GridManager";

export default {
  data() {
    return {
      rows: [
        { name: "row1", color: "#ffa07a" },
        { name: "row2", color: "#fbec5d" },
        { name: "row3", color: "#33a8a5" }
      ],
      startDate: "",
      endDate: "",
      columnSpan: 7
    };
  },
  components: {
    Timeline,
    TaskManager
  },
  methods: {
    acceptRow(row) {
      this.rows.push(row);
    },
    acceptDateRange(dateRange) {
      this.startDate = dateRange.startDate;
      this.endDate = dateRange.endDate;
      this.columnSpan = parseInt(dateRange.columnSpan);
    }
  }
};
</script>
