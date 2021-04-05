<template>
  <div class="row" :style="cssVars">
    <div class="row-label">Columns</div>
    <div v-for="i in headerDates.length - 1" :key="i">
      <ColumnHeader :date="headerDates[i]" :gridColumn="i" />
    </div>
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
import moment from "moment";
export default {
  props: {
    startDate: {
      type: Date
    },
    endDate: {
      type: Date
    },
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
    },
    headerDates() {
      return this.getDaysBetweenDates(this.startDate, this.endDate);
    }
  },
  methods: {
    getDaysBetweenDates(startDate, endDate) {
      let now = moment(startDate);
      let dates = [];
      dates.push(new Date(now.format("MM/DD/YYYY")));
      while (now.isSameOrBefore(moment(endDate))) {
        dates.push(new Date(now.format("MM/DD/YYYY")));
        now.add(1, "days");
      }
      return dates;
    }
  }
};
</script>
