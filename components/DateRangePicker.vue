<template>
  <v-row>
    <v-col cols="12" sm="6">
      <v-menu
        ref="menu"
        v-model="menu"
        :close-on-content-click="false"
        :return-value.sync="date"
        transition="scale-transition"
        offset-y
        min-width="auto"
      >
        <template v-slot:activator="{ on, attrs }">
          <v-text-field
            v-model="dateRangeText"
            prepend-icon="mdi-calendar"
            readonly
            v-bind="attrs"
            v-on="on"
          ></v-text-field>
        </template>
        <v-date-picker v-model="dates" range>
          <v-spacer></v-spacer>
          <v-btn text color="primary" @click="menu = false">
            Cancel
          </v-btn>
          <v-btn text color="primary" @click="$refs.menu.save(date)">
            OK
          </v-btn>
        </v-date-picker>
      </v-menu>
    </v-col>
  </v-row>
</template>

<script>
import moment from "moment";
export default {
  //   props: {
  //     startDate: {
  //       type: String
  //     },
  //     endDate: {
  //       type: String
  //     },
  //     columnSpan: {
  //       type: Number
  //     }
  //   },
  data: () => ({
    // dates: ["2019-09-10", "2019-09-20"],
    dates: [],
    date: new Date().toISOString().substr(0, 10),
    menu: false,
    modal: false,
    menu2: false
  }),
  computed: {
    dateRangeText() {
      if (this.dates.length == 0) {
        return "Date Range";
      }
      var a = moment(this.dates[0]);
      var b = moment(this.dates[1]);
      let startDate = a.format("DD-MM-YYYY");
      let endDate = b.format("DD-MM-YYYY");
      let columnSpan = Math.abs(a.diff(b, "days"));
      console.log(columnSpan);
      this.$emit("emitDateRange", {
        startDate,
        endDate,
        columnSpan
      });
      return this.dates.join(" ~ ");
    }
  }
};
</script>
