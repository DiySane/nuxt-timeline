<template>
  <v-card
    color="blue-grey darken-4"
    class="service-item"
    style="grid-row: 1/2; grid-column: 4/5; display: grid; grid-template-columns: repeat(2, 1fr); grid-template-rows: repeat(4, 1fr); grid-gap: 5px; background-color: #f2f4f7;"
  >
    <v-card-title
      style="grid-row: 1/2; grid-column: 1/3; color: white; text-align: center;"
    >
      TASK MANAGER
    </v-card-title>
    <v-form class="px-3" ref="form" style="grid-row: 2/5; grid-column: 1/3;">
      <v-text-field
        text-color="black"
        label="Task Name"
        v-model="name"
        prepend-icon="mdi-pencil"
        style="caret-color: black;"
      ></v-text-field>
      <v-text-field
        label="Start Day"
        v-model="start"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-text-field
        v-if="false"
        label="Task End"
        v-model="end"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-text-field
        label="Row"
        v-model="row"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-text-field
        label="Color"
        v-model="color"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-text-field
        label="Sub-row"
        v-model="subRow"
        prepend-icon="mdi-pencil"
      ></v-text-field>
      <v-btn @click="emitNode"> Submit</v-btn>
    </v-form>
  </v-card>
</template>

<style lang="css" scoped>
.service-item {
  padding: 5px;
  text-align: center;
  border-top: 1px solid #3e2723;
  border-bottom: 1px solid #3e2723;
  border-left: 1px solid #3e2723;
  border-right: 1px solid #3e2723;
  min-width: 20px;
  min-height: 30px;
  color: black;
}
</style>

<script>
export default {
  data() {
    return {
      title: "",
      name: "",
      start: "",
      end: "",
      row: "",
      color: "",
      subRow: "",
      due: null,
      menu: false,
      loading: false,
      id: 0
    };
  },
  methods: {
    emitNode() {
      this.$emit("addNode", {
        name: this.name,
        start: parseInt(this.start),
        row: parseInt(this.row),
        color: this.color,
        subRow: parseInt(this.subRow),
        id: this.id++
      });
    }
  }
};
</script>
