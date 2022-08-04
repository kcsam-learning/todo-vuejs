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
$backgroundColor: #27292d;
$textColor: white;
$primaryColor: #a0a4d9;
$secondTextColor: #1f2023;

body {
	margin: 0;
	padding: 0;
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	background-color: $backgroundColor;
	color: $textColor;
	#app {
		max-width: 600px;
		margin-left: auto;
		margin-right: auto;
		padding: 20px;
		h1 {
			font-weight: bold;
			font-size: 28px;
			text-align: center;
		}
		button {
			cursor: pointer;
			background-color: $primaryColor;
			border: 1px solid $primaryColor;
			color: $secondTextColor;
			font-weight: bold;
			outline: none;
			border-radius: $size1;
		}
		h2 {
			font-size: 22px;
			border-bottom: $border;
			padding-bottom: $size1;
		}
		h4 {
			text-align: center;
			opacity: 0.5;
			margin: 0;
		}
	}
}
</style>
