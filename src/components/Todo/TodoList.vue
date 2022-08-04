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
    },
    saveData: Function
  },
  setup(props) {
    const { todos } = toRefs(props)

    function removeTodo(idx) {
      const { saveData } = props

      todos.value.splice(idx, 1)
      saveData(todos.value)
    }
    function doneTodo(todo) {
      const { saveData } = props

      todo.done = !todo.done
      saveData(todos.value)
    }
    return {
      removeTodo,
      doneTodo
    }
  },
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

ul {
  padding: 10px;
  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    border: $border;
    padding: $size2 $size4;
    border-radius: $size1;
    margin-bottom: $size2;
    span {
      cursor: pointer;
    }
    .done {
      text-decoration: line-through;
    }
    button {
      font-size: $size2;
      padding: $size1;
    }
  }
}
</style>
