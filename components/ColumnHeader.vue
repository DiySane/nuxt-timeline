<template>
  <div class="columnName" :style="cssVars">
    <v-tooltip eager>
      <template v-slot:activator="{ on, attrs }">
        <v-card dark v-bind="attrs" v-on="on">
          {{ getMoment(date).format("DD") }}
        </v-card>
      </template>
      <span>{{ getMoment(date).format("DD-MM-YYYY") }}</span>
    </v-tooltip>
  </div>
</template>

<style scoped>
.columnName {
  border: #ffff 1px solid;
  padding: 0em;
  margin: 0px;
  grid-column: var(--grid-column);
}
</style>

<script>
import moment from "moment";
export default {
  props: {
    gridColumn: {
      type: Number
    },
    date: {
      type: Date
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column": this.gridColumn
      };
    }
  },
  methods: {
    getMoment(date) {
      return moment(date);
    }
  }
};
</script>
