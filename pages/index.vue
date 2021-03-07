<template>
  <v-container>
    <v-row>
      <v-col>
        <Timeline
          :columnSpan="columnSpan"
          :rows="rows"
          :startDate="startDate"
          :endDate="endDate"
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
import moment from "moment";

export default {
  data() {
    return {
      rows: [
        {
          name: "row1",
          color: "#ffa07a",
          nodes: [
            { name: "task1", start: 2, end: 3, complete: 0.3 },
            { name: "task2", start: 4, end: 5, complete: 0.5 },
            { name: "task3", start: 3, end: 6, complete: 0.5 },
            { name: "task4", start: 7, end: 8, complete: 0.5 }
          ]
        },
        { name: "row2", color: "#fbec5d", nodes: [] },
        { name: "row3", color: "#33a8a5", nodes: [] }
      ],
      nodes: [
        { name: "task1", start: 2, end: 3, complete: 0.3 },
        { name: "task2", start: 4, end: 5, complete: 0.5 },
        { name: "task3", start: 3, end: 6, complete: 0.5 },
        { name: "task4", start: 7, end: 8, complete: 0.5 }
      ],
      startDate: moment().startOf("week"),
      endDate: moment().endOf("week"),
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
      row.nodes = [];
      this.rows.push(row);
    },
    acceptDateRange(dateRange) {
      this.startDate = new Date(dateRange.startDate);
      this.endDate = new Date(dateRange.endDate);
      this.columnSpan = parseInt(dateRange.columnSpan);
      for (let row of this.rows) {
        for (let node of row.nodes) {
          this.setNodeDisplay(node);
        }
      }
    },
    acceptSelectedRow(row) {
      this.selectedRow = row;
      console.log(row.name);
    },
    acceptNode(node) {
      // this.selectedRow.name = "name";
      this.setNodeDisplay(node);
      this.selectedRow.nodes.push(node);
      console.log(node.name);
    },
    setNodeDisplay(node) {
      let nodeStartDate = new Date(node.startDate);
      let nodeEndDate = new Date(node.endDate);
      console.log(nodeStartDate);
      // console.log(this.startDate);
      // console.log(moment(nodeEndDate).format('DD-MM-YYYY'));
      let nodeDisplayStartDate =
        nodeStartDate.getTime() > this.startDate.getTime()
          ? nodeStartDate
          : this.startDate;
      let nodeDisplayEndDate =
        nodeEndDate.getTime() < this.endDate.getTime()
          ? nodeEndDate
          : this.endDate;
      let nodeDisplayStartCol =
        this.getFiniteOrZero(
          (nodeDisplayStartDate.getTime() - this.startDate.getTime()) /
            (1000 * 60 * 60 * 24)
        ) + 2;
      let nodeDisplayEndCol =
        this.columnSpan -
        this.getFiniteOrZero(
          (this.endDate.getTime() - nodeDisplayEndDate.getTime()) /
            (1000 * 60 * 60 * 24)
        ) +
        2;
      node.start = nodeDisplayStartCol;
      node.end = nodeDisplayEndCol;
      node.displayStartDate = moment(nodeDisplayStartDate).format("DD-MM-YYYY");
      node.displayEndDate = moment(nodeDisplayEndDate).format("DD-MM-YYYY");
      return node;
    },
    getFiniteOrZero(x) {
      if (isFinite(x)) {
        return x;
      } else {
        return 0;
      }
    }
  }
  // computed: {
  //   columnSpan() {
  //     let value = 0;
  //     if(this.startDate == undefined || this.startDate == null || this.endDate == undefined || this.endDate == null ) {
  //       value = 7;
  //     } else {
  //       let timeDiff = this.endDate.getTime() - this.startDate.getTime();
  //       let daysDiff = timeDiff / (1000 * 60 * 60 * 24);
  //       value = daysDiff + 1;
  //     }
  //     return value;
  //   }
  // }
};
</script>
