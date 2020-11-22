<template>
  <div>
    <ul>
      <TodoItem 
      v-for="(title, i) in szTodos" 
      :key="title.id" 
      v-bind:todoItem="title" 
      v-bind:index="i"
      v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem";
export default {
  props: ["szTodos"],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      this.$emit("remove-todo", id);
    }
  }
};
</script>

<style scoped>
  ul{
    list-style: none;
    margin: 0;
    padding: 0;
  }
</style>