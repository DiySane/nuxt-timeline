<template>
  <li class="sub-task" :style="cssVars"></li>
  <!-- <ul class="sub-task" :style="cssVars"></ul> -->
<!-- <dt class="sub-task" :style="cssVars"></dt> -->
</template>

<style scoped>
li::before {
  list-style-type: none;
 }
li::after {
  list-style-type: none;
 }
.sub-task {
  /* list-style-type: circle; */
  background: var(--color);
  grid-column: var(--start) / var(--end);
  /* display: overlay; */
  /* overflow: hidden; */
}
</style>

<script>
export default {
  // data() {
  //   return {
  //     pendingColor: this.LightenDarkenColor(this.color, -20),
  //   };
  // },
  props: {
    start: {
      type: Number
    },
    end: {
      type: Number
    },
    color: {
      type: String
    }
  },
  computed: {
    cssVars() {
      return {
        /* variables you want to pass to css */
        // "--grid-column-span": this.gridColumnSpan,
        "--color": this.color,
        "--start": this.start,
        "--end": this.end,
        // "--complete": this.start + this.complete,
        // "--pending-color": this.pendingColor,
      };
    },
    // pendingColor() {
    //     return this.LightenDarkenColor(this.color, -20);
    // }
  },
  methods: {
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
