<template>
  <todo-form v-on:task-created="addTask"></todo-form>
  <h1>To-do:</h1>
  <ul>
    <li v-for="todo in toDoItems" v-bind:key="todo.id">
      <todo-list-item v-bind:label="todo.label" v-bind:done="todo.done" v-bind:id="todo.id"></todo-list-item>
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
        { id: uniqueId('task-'), label: 'learn vue', done: false },
        { id: uniqueId('task-'), label: 'drink coffee', done: true },
        { id: uniqueId('task-'), label: 'my taxes', done: false },
      ],
    };
  },
  methods: {
    addTask(text) {
      this.toDoItems.push({ id: uniqueId('task-'), label: text, done: false });
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
