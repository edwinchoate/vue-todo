<template>
  <todo-form v-on:task-created="addTask"></todo-form>
  <h1>To-do:</h1>
  <p id="summary">{{summary}}</p>
  <ul aria-labelledby="#summary">
    <li v-for="todo in toDoItems" v-bind:key="todo.id">
      <todo-list-item v-bind:label="todo.label" v-bind:done="todo.done" v-bind:id="todo.id" v-on:checkbox-changed="updateCheckbox(todo.id)"></todo-list-item>
    </li>
  </ul>
</template>

<script>
import TodoListItem from './components/TodoListItem.vue';
import TodoForm from './components/TodoForm.vue';
import uniqueId from 'lodash.uniqueid';


export default {
  name: 'App',
  components: {
    TodoListItem, 
    TodoForm,
  },
  data() {
    return {
      toDoItems: [
        { id: uniqueId('task-'), label: 'receive $200', done: false },
        { id: uniqueId('task-'), label: 'code', done: true },
        { id: uniqueId('task-'), label: 'win', done: true },
        { id: uniqueId('task-'), label: 'drink', done: false },
        { id: uniqueId('task-'), label: 'get naked', done: false },
      ],  
    };
  },
  methods: {
    addTask(text) {
      this.toDoItems.push({ id: uniqueId('task-'), label: text, done: false });
    },
    updateCheckbox(taskID) {
      const todoItem = this.toDoItems.find((item) => (item.id === taskID));
      todoItem.done = !todoItem.done;
    },
  },
  computed: {
    summary() {
      const completed = this.toDoItems.filter((item) => item.done).length;
      return `${completed}/${this.toDoItems.length} tasks complete`;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>
