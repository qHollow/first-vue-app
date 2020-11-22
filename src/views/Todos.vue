<template>
  <div>
    <router-link to="/">Home</router-link>
    <Create @add-todo="createElem" />
    <select v-model="filtre">
      <option value="all">All</option>
      <option value="completed">completed</option>
      <option value="not-completed">not-completed</option>
    </select>
    <Loader v-if="loading" />
    <TodoList 
    v-else-if="filteredTodos.length"
    v-bind:szTodos="filteredTodos"
    @remove-todo="removeTodo"
    />
    <p v-else>No todos!</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
import Create from "@/components/AddTodo";
import Loader from "@/components/Loader";

export default {
  name: "app",
  data() {
    return {
      szTodos: [],
      loading: true,
      filtre: "all"
    };
  },
  components: {
    TodoList,
    Create,
    Loader
  },
  mounted() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=3')
    .then(response => response.json())
    .then(json => {
      //setTimeout(() => {
        this.szTodos = json;
        this.loading = false;
      //}, 1000);
    });
  },
  // watch: {
  //   filter(value) {
      
  //   }
  // },
  computed: {
    filteredTodos() {
      if(this.filtre === "all"){
        return this.szTodos;
      }

      if(this.filtre === "completed"){
        return this.szTodos.filter(t => t.completed);
      }

      if(this.filtre === "not-completed"){
        return this.szTodos.filter(t => !t.completed);
      }
      return 0;
    }
  },
  methods: {
    removeTodo(id) {
      this.szTodos = this.szTodos.filter(t => t.id !== id);
    },
    createElem(obj) {
      console.log(obj);
      this.szTodos.push(obj);
    }
  }
};
</script>