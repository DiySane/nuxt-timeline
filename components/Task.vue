<template>
<!-- <li> -->
  <ul
    class="task"
    :style="cssVars"
    @mouseover="showText = true"
    @mouseleave="showText = false"
  >
    <!-- {{ name }} -->
    <!-- <div class="task" :style="cssVars"> -->
    <SubTask
    v-show="!showText"
    :start="1" :end="computedComplete" :color="color" />
    <SubTask
    v-show="!showText"
     :end="11" :start="computedComplete" :color="pendingColor" />
    <!-- <div style="text-align: center; background-color: transparent; grid-column: 1 / 11;">{{ name }}</div> -->
    <li
      v-show="showText"
      style="grid-column: 1/11; text-align: center; opacity: 0.5; background: var(--color);"
    >
      {{ name }}
    </li>

    <!-- <SubTask :start="1" :end="computedComplete" :color="pendingColor"/>
      <SubTask :end="11" :start="computedComplete" :color="color"/> -->
  </ul>
<!-- </li> -->
</template>

<style scoped>
/* ul {
  list-style-type: none;
 } */
.task {
  /* background: transparent; */
  background: var(--color);
  /* opacity: 0.0; */
  padding: 1em;
  grid-column: var(--start) / var(--end);
  padding: 0em;
  margin: 0px;
  /* text-align: center; */
  display: grid;
  grid-template-columns: repeat(10, 1fr);
  width: 100%;
  /* list-style-type: none; */
  /* overflow: hidden; */
}
/* .complete {
  background: var(--color);
  grid-column: var(--start) / var(--complete);
}
.pending {
  background: var(--pending-color);
  grid-column: var(--start) / var(--end);
} */
</style>

<script>
// import SubTask from "@/components/SubTask"
export default {
  data() {
    return {
      showText: false
      //   pendingColor: this.LightenDarkenColor(this.color, -20),
    };
  },
  props: {
    start: {
      type: Number
    },
    end: {
      type: Number
    },
    complete: {
      type: Number
    },
    name: {
      type: String
    },
    color: {
      type: String
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        "--grid-column-span": this.gridColumnSpan,
        "--color": this.color,
        "--start": this.start,
        "--end": this.end,
        "--complete": this.computedComplete,
        "--pending-color": this.pendingColor
      };
    },
    pendingColor() {
      return this.LightenDarkenColor(this.color, 20);
    },
    computedComplete() {
      return 10 * this.complete+1;
    }
  },
  methods: {
    toggleText: function() {
      this.showText = !this.showText;
    },
    LightenDarkenColor: function(col, amt) {
      var usePound = false;

      if (col[0] == "#") {
        col = col.slice(1);
        usePound = true;
      }

      var num = parseInt(col, 16);

      var r = (num >> 16) + amt;

      if (r > 255) r = 255;
      else if (r < 0) r = 0;

      var b = ((num >> 8) & 0x00ff) + amt;

      if (b > 255) b = 255;
      else if (b < 0) b = 0;

      var g = (num & 0x0000ff) + amt;

      if (g > 255) g = 255;
      else if (g < 0) g = 0;

      return (usePound ? "#" : "") + (g | (b << 8) | (r << 16)).toString(16);
    }
  }
};
</script>
