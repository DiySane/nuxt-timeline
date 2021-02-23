<template>
  <!-- <label> -->
  <div
    class="task"
    :style="cssVars"
    @mouseover="showText = true"
    @mouseleave="showText = false"
  >
    <progress
      v-show="!showText"
      :style="cssVars"
      class="task"
      :value="complete"
    ></progress>
    <div
      v-show="showText"
      style="text-align: center; opacity: 0.5; background: var(--color);"
    >
      {{ name }}
    </div>
  </div>
</template>

<style scoped>
.task {
  background: var(--pending-color);
  padding: 1em;
  grid-column: var(--start) / var(--end);
  padding: 0em;
  margin: 0px;
  width: 100%;
  height: 100%;
}
progress::-webkit-progress-value {
  background-color: var(--color) !important;
  /* width: 100%; */
}
progress::-moz-progress-bar {
  background-color: var(--color) !important;
  /* width: 100%; */
}
progress {
  color: var(--color);
  /* width: 100%; */
}
</style>

<script>
// import SubTask from "@/components/SubTask"
export default {
  data() {
    return {
      showText: false
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
        "--complete": this.complete,
        "--pending-color": this.pendingColor
      };
    },
    pendingColor() {
      return this.LightenDarkenColor(this.color, 20);
    },
    computedComplete() {
      return 10 * this.complete + 1;
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
