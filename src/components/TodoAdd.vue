<template>
  <div>
    <v-row>
      <v-col cols="10">
        <v-text-field
          name="name"
          label="Task"
          id="id"
          @keyup.enter="addTask"
          v-model="taskTextField"
        ></v-text-field>
      </v-col>
      <v-col cols="2">
        <v-btn block @click="addTask" color="success">ADD</v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>

function create_UUID(){
    var dt = new Date().getTime();
    var uuid = 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function(c) {
        var r = (dt + Math.random()*16)%16 | 0;
        dt = Math.floor(dt/16);
        return (c=='x' ? r :(r&0x3|0x8)).toString(16);
    });
    return uuid;
}

export default {
  name: "TodoAdd",
  created() {},
  methods: {
    addTask() {
      let task = {
        id: create_UUID(),
        title: this.taskTextField,
        completed: false,
      };

      this.$emit("onAdd", task);
      this.taskTextField = "";
    },
  },
  data() {
    return {
      taskTextField: "",
    };
  },
  props: {},
};
</script>

<style lang="scss" scoped></style>
