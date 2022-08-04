<template>
  <form @submit.prevent="addTodo()">
    <label>Todo Form</label>
    <input
      v-model="newTodo"
      name="newTodo"
      autocomplete="off"
    />
    <button>Add Todo</button>
  </form>
</template>

<script>
import { ref, toRefs } from 'vue'

export default {
  name: 'TodoForm',
  props: {
    todos: Array,
    saveData: Function
  },
  setup(props) {
    const newTodo = ref('')
    const { todos } = toRefs(props)

    function addTodo() {
      const { saveData } = props

      if (newTodo.value) {
        todos.value.push({
          done: false,
          content: newTodo.value
        })
        newTodo.value = ''
      }

      saveData(todos.value)
    }
    return {
      addTodo,
      newTodo,
    }
  }
}
</script>
