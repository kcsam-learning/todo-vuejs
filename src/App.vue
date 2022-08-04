<template>
  <h1>Todo App</h1>
  <TodoForm :saveData="saveData" :todos="todos"/>
  <TodoList :saveData="saveData" :todos="todos"/>
</template>

<script>
import TodoForm from './components/Todo/TodoForm.vue'
import TodoList from './components/Todo/TodoList.vue'
import { ref } from 'vue'

export default {
  name: 'App',
  components: {
    TodoForm,
    TodoList,
  },
  setup() {
    const todosData = JSON.parse(localStorage.getItem('todo')) || []
    const todos = ref(todosData)

    function saveData(data) {
      const storageData = JSON.stringify(data)
      localStorage.setItem('todo', storageData)
    }
    return {
      saveData,
      todos
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
