<template>
  <div>
    <v-card>
      <v-card-title primary-title>
        <v-container>
          <v-row
            class="d-flex flex-row align-center pa-0"
            v-for="(item, index) in todos"
            :key="index"
          >
            <v-col cols="12" class="d-flex flex-row align-center">
              <v-checkbox v-model="item.completed" class="mr-2 py-0"></v-checkbox>
              <span>{{ item.title }}</span>
              <v-spacer></v-spacer>
              <v-btn @click="$emit('onRemove',item.id)" color="error">X</v-btn>
            </v-col>
            <v-col cols="12">
              <v-divider></v-divider>
            </v-col>
          </v-row>
        </v-container>
      </v-card-title>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "TodoList",
  created() {},
  data() {
    return {};
  },
  props:["todos"],
  methods: {},
};
</script>

<style lang="scss" scoped></style>
