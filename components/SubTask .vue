<template>
  <progress class="sub-task" :style="cssVars"></progress>
</template>

<style scoped>
.sub-task {
  background: var(--color);
  grid-column: var(--start) / var(--end);
}
</style>

<script>
export default {
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
        "--color": this.color,
        "--start": this.start,
        "--end": this.end,
      };
    },
  },
};
</script>
