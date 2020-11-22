<template>
  <li>
    <label v-bind:class="{done: todoItem.completed}">
      <input type="checkbox" v-on:change="todoItem.completed = !todoItem.completed" />
      <strong>{{index + 1}}</strong>
      {{todoItem.title | upperCase}}
    </label>
    <button class="rm" v-on:click="$emit('remove-todo', todoItem.id)" >
      &times;
    </button>
  </li>
</template>

<script>

export default {
  props: {
    todoItem: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    upperCase(value) {
      return value.toUpperCase();
    }
  }
}
</script>

<style scoped>
  li {
    border: 1px solid #ccc;
    display: flex;
    justify-content: space-between;
    padding: 0.5rem 2rem;
    margin-bottom: 1rem;
  }
  .rm {
    background-color: red;
    color: #fff;
    border-radius: 50%;
    font-weight: bold;
    border: 1px solid red;
  }
  input{
    margin-right: 1rem;
  }
  .done {
    text-decoration: line-through;
  }
</style>