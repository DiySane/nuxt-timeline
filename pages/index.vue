<template>
  <!-- <div style="display: grid; grid-template-columns: repeat(2, 1fr);">
    <Timeline style="grid-column: 1/2"/>
    <TaskManager style="grid-column: 2/3"/>
  </div> -->
  <v-container>
    <v-row>
      <v-col> <Timeline /></v-col>
      <v-col>
        <TaskManager />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Timeline from "@/components/Timeline";
import TaskManager from "@/components/TaskManager";

export default {
  components: {
    Timeline,
    TaskManager
  }
};
</script>
