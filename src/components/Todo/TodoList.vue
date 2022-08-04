<template>
<h2>Todo List</h2>
<ul>
  <li
    v-for="(todo, i) in todos"
    :key="i"
  >
    <span :class="{ done: todo.done }" @click="doneTodo(todo)">{{ todo.content }}</span>
    <button @click="removeTodo(i)">Remove</button>
  </li>
</ul>
<h4 v-if="todos.length === 0">Empty list.</h4>
</template>

<script>
import { toRefs } from 'vue'

export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Array,
      default() {
        return []
      }
    }
  },
  setup(props) {
    const { todos } = toRefs(props)

    function removeTodo(idx) {
      todos.value.splice(idx, 1)
      saveData()
    }
    function doneTodo(todo) {
      todo.done = !todo.done
      saveData()
    }
    function saveData() {
      const storageData = JSON.stringify(todos.value)
      localStorage.setItem('todo', storageData)
    }
    return {
      removeTodo,
      saveData,
      doneTodo
    }
  },
}
</script>
<style lang="scss">
body {
  ul {
    li {
      .done {
        text-decoration: line-through;
      }
    }
  }
}

</style>
