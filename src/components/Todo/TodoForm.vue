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

<style lang="scss">
$border: 2px solid
	rgba(
		$color: white,
		$alpha: 0.35,
	);
$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;

form {
  display: flex;
  flex-direction: column;
  width: 100%;
  label {
    font-size: 14px;
    font-weight: bold;
  }
  input,
  button {
    height: $size5;
    box-shadow: none;
    outline: none;
    padding-left: $size2;
    padding-right: $size2;
    border-radius: $size1;
    font-size: 18px;
    margin-top: $size1;
    margin-bottom: $size2;
  }
  input {
    background-color: transparent;
    border: $border;
    color: inherit;
  }
}
</style>
