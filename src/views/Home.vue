<template>
  <div class="home">
    <v-container>
      <!-- Todo add task -->
      <TodoAdd @onAdd="addTask" />
      <!-- Todo Task -->
      <TodoList @onRemove="removeTask" :todos="todos | reversed" />

      <v-row class="d-flex flex-row justify-center align-center">
        <v-col cols='4'>
          <img block class="mt-10" src="@/assets/MDLogo.png" alt="logo" />
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import TodoAdd from "@/components/TodoAdd.vue";
import axios from 'axios'
export default {
  name: "Home",
  components: {
    TodoList,
    TodoAdd,
  },
  filters:{
    reversed(value){
      return value.slice().reverse()
    }
  },
  computed:{
    reversdTodo(){
      return this.todos.slice().reverse()
    }
  },
  async mounted() {
    let result = await axios.get("https://jsonplaceholder.typicode.com/todos")
    this.todos = result.data
  },
  methods: {
    async addTask(task) {
      let result = await axios.post("https://jsonplaceholder.typicode.com/todos", task)
      this.todos.push(result.data);
    },
    removeTask(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`).then(() => {
        this.todos = this.todos.filter((item) => item.id !== id);
      }).catch((err) => {
        console.log(err);
      });
    },
  },
  data() {
    return {
      todos: [],
      todos_mukup: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
      ],
    };
  },
};
</script>
