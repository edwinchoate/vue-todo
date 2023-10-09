<template>
  <todo-form v-on:task-created="addTask"></todo-form>
  <h1>To-do:</h1>
  <p id="summary" ref="summary" tabindex="-1">{{summary}}</p>
  <ul aria-labelledby="#summary">
    <li v-for="todo in todoItems" v-bind:key="todo.id">
      <todo-item v-bind:label="todo.label" v-bind:done="todo.done" v-bind:id="todo.id" v-on:checkbox-changed="updateCheckbox(todo.id)" 
        v-on:task-edit-save="updateTaskLabel(todo.id, $event)" v-on:task-deleted="deleteTask(todo.id)"></todo-item>
    </li>
  </ul>
</template>

<script>
import TodoItem from './components/TodoItem.vue';
import TodoForm from './components/TodoForm.vue';
import uniqueId from 'lodash.uniqueid';


export default {
  name: 'App',
  components: {
    TodoItem, 
    TodoForm,
  },
  data() {
    return {
      todoItems: [
        { id: uniqueId('task-'), label: 'learn vue', done: true },
        { id: uniqueId('task-'), label: 'make todo app', done: true },
        { id: uniqueId('task-'), label: 'master vue', done: false },
      ],  
    };
  },
  methods: {
    addTask(text) {
      this.todoItems.push({ id: uniqueId('task-'), label: text, done: false });
    },
    updateCheckbox(taskID) {
      const todoItem = this.todoItems.find((item) => item.id === taskID);
      todoItem.done = !todoItem.done;
    },
    updateTaskLabel(taskID, newLabel) {
      const todoItem = this.todoItems.find((item) => item.id === taskID);
      todoItem.label = newLabel;
    },
    deleteTask(taskID) {
      const i = this.todoItems.findIndex((item) => item.id === taskID);
      this.todoItems.splice(i, 1);
      this.$refs.summary.focus();
    }
  },
  computed: {
    summary() {
      const completed = this.todoItems.filter((item) => item.done).length;
      return `${completed}/${this.todoItems.length} tasks complete`;
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
