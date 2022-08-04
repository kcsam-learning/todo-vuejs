<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addTodo()">
    <label>Todo Form</label>
    <input
      v-model="newTodo"
      name="newTodo"
      autocomplete="off"
    />
    <button>Add Todo</button>
  </form>
  <TodoList :todos="todos"/>
</template>

<script>
import { ref } from 'vue'
import TodoList from './TodoList.vue'

export default {
  name: 'TodoForm',
  components: {
    TodoList
  },
  setup() {
    const newTodo = ref('')
    const defaultData = []
    const todosData = JSON.parse(localStorage.getItem('todo')) || defaultData
    const todos = ref(todosData)

    function addTodo() {
      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value
        })
        newTodo.value = ''
      }
      saveData()
    }
    function saveData() {
      const storageData = JSON.stringify(todos.value)
      localStorage.setItem('todo', storageData)
    }
    return {
      addTodo,
      newTodo,
      saveData,
      todos
    }
  }
}
</script>
