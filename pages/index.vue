<template>
  <v-container>
    <v-row>
      <v-col>
        <Timeline
          :columnSpan="columnSpan"
          :rows="rows"
          @emitDateRange="acceptDateRange"
          @emitSelectedRow="acceptSelectedRow"
      /></v-col>
    </v-row>
    <v-row>
      <v-col>
        <TaskManager :selectedRow="selectedRow" @addNode="acceptNode" />
      </v-col>
      <v-col>
        <GridManager @addRow="acceptRow" @addColumn="acceptDateRange" />
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
        {
          name: "row1",
          color: "#ffa07a",
          tasks: [
            { name: "task1", start: 2, end: 3, complete: 0.3 },
            { name: "task2", start: 4, end: 5, complete: 0.5 },
            { name: "task3", start: 3, end: 6, complete: 0.5 },
            { name: "task4", start: 7, end: 8, complete: 0.5 }
          ]
        },
        { name: "row2", color: "#fbec5d", tasks: [] },
        { name: "row3", color: "#33a8a5", tasks: [] }
      ],
      tasks: [
        { name: "task1", start: 2, end: 3, complete: 0.3 },
        { name: "task2", start: 4, end: 5, complete: 0.5 },
        { name: "task3", start: 3, end: 6, complete: 0.5 },
        { name: "task4", start: 7, end: 8, complete: 0.5 }
      ],
      startDate: "",
      endDate: "",
      columnSpan: 7,
      selectedRow: null
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
    },
    acceptSelectedRow(row) {
      this.selectedRow = row;
      console.log(row.name);
    },
    acceptNode(node) {
      this.selectedRow.name = "name";
      this.selectedRow.tasks.push(node);
      console.log(node.name);
    }
  }
};
</script>
