<template>
  <h1>ToDo App</h1>
	<form @submit.prevent="addTodo()">
		<label>New ToDo </label>
		<input
			v-model="newTodo"
			name="newTodo"
			autocomplete="off"
		>
		<button>Add ToDo</button>
	</form>
	<h2>ToDo List</h2>
	<ul>
		<li
			v-for="(todo, index) in todos"
			:key="index"
		>
			<span
				:class="{ done: todo.done }"
				@click="doneTodo(todo)"
			>{{ todo.content }}</span>
			<button @click="removeTodo(index)">Remove</button>
		</li>
	</ul>
	<h4 v-if="todos.length === 0">Empty list.</h4>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import HelloWorld from "./components/HelloWorld.vue";
import { DefineComponent } from "vue";

import { ref } from 'vue';
		name: 'App';
		
		setup() {
			const newTodo = ref('');
			const defaultData = [{
				done: false,
				content: 'Write a blog post'
			}]
			const todosData = JSON.parse(localStorage.getItem('todos')) || defaultData;
			const todos = ref(todosData);
			function addTodo(): void {
				if (newTodo.value) {
					todos.value.push({
						done: false,
						content: newTodo.value
					});
					newTodo.value = '';
				}
				saveData();
			}

			function doneTodo (todo) {
				todo.done = !todo.done
				saveData();
			}

			function removeTodo (index) {
				todos.value.splice(index, 1);
				saveData();
			}

			function saveData () {
				const storageData = JSON.stringify(todos.value);
				localStorage.setItem('todos', storageData);
			}

			return {
				todos,
				newTodo,
				addTodo,
				doneTodo,
				removeTodo,
				saveData
			}
		}
	}



export default class App extends Vue {}
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
body {
	 margin: 0;
	 padding: 0;
	 font-family: Avenir, Helvetica, Arial, sans-serif;
	 -webkit-font-smoothing: antialiased;
	 -moz-osx-font-smoothing: grayscale;
	 background-color: #978d30;
	 color: #070202;
}
 body #app {
	 max-width: 600px;
	 margin-left: auto;
	 margin-right: auto;
	 padding: 20px;
}
 body #app h1 {
	 font-weight: bold;
	 font-size: 28px;
	 text-align: center;
}
 body #app form {
	 display: flex;
	 flex-direction: column;
	 width: 100%;
}
 body #app form label {
	 font-size: 14px;
	 font-weight: bold;
}
 body #app form input, body #app form button {
	 height: 48px;
	 box-shadow: none;
	 outline: none;
	 padding-left: 12px;
	 padding-right: 12px;
	 border-radius: 6px;
	 font-size: 18px;
	 margin-top: 6px;
	 margin-bottom: 12px;
}
 body #app form input {
	 background-color: transparent;
	 border: 2px solid rgba(255, 255, 255, 0.35);
	 color: inherit;
}
 body #app button {
	 cursor: pointer;
	 background-color: #5f51df;
	 border: 1px solid #5f51df;
	 color: #1f2023;
	 font-weight: bold;
	 outline: none;
	 border-radius: 6px;
}
 body #app h2 {
	 font-size: 22px;
	 border-bottom: 2px solid rgba(255, 255, 255, 0.35);
	 padding-bottom: 6px;
}
 body #app ul {
	 padding: 10px;
}
 body #app ul li {
	 display: flex;
	 justify-content: space-between;
	 align-items: center;
	 border: 2px solid rgba(255, 255, 255, 0.35);
	 padding: 12px 24px;
	 border-radius: 6px;
	 margin-bottom: 12px;
}
 body #app ul li span {
	 cursor: pointer;
}
 body #app ul li .done {
	 text-decoration: line-through;
}
 body #app ul li button {
	 font-size: 12px;
	 padding: 6px;
}
 body #app h4 {
	 text-align: center;
	 opacity: 0.5;
	 margin: 0;
}
 
</style>
