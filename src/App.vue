<template>
  <div>
    <div class="head">
      <h1>ketik sesuatu</h1>
    </div>

    <div class="body">
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" required placeholder="ketik disini!">
        <button>Add</button>
      </form>
    </div>

    <div class="foot">
      <ul>
        <li v-for="todo in filteredTodos" :key="todo.id">
          <span :class="{ done: todo.done }">{{ todo.text }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([])

const filteredTodos = computed(() => {
  return hideCompleted.value
    ? todos.value.filter((t) => !t.done)
    : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<style>

body {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0;
  padding: 0;
  background-color: darkgrey; 
}

.head {
  text-align: center;
  margin-bottom: 50px;
  margin-top: -100px;
}

.head h1 {
  color: #4b4f52;
  margin: 0;
  font-size: 36px; 
  font-weight: bold; 
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
  transition: color 0.3s ease; 
}

.head h1:hover {
  color: #007bff; 
}

.body form {
  display: flex;
  align-items: center;
}

.body input[type="text"] {
  flex-grow: 1;
  padding: 15px;
  font-size: 16px;
  border: 2px solid #ced4da; 
  border-radius: 5px;
}

.body button {
  background-color: #007bff; 
  color: #fff; 
  border: none;
  border-radius: 5px;
  padding: 4px;
  font-size: 16px;
  cursor: pointer;
  margin-left: 10px;
}

.body button:hover {
  background-color: #0056b3; 
}

.foot ul {
  list-style-type: none;
  padding: 0;
  color: whitesmoke
}

.foot li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
  margin: autos;
  color: black; 
}

.foot input[type="checkbox"] {
  margin-right: 10px;
}

.foot .done {
  text-decoration: line-through; 
}

.foot button {
  margin-left: 30px;
  background-color: #dc3545;
  color: #fff; 
  border: 1px;
  border-radius: 50%;
  width: 30px;
  height: 30px;
  font-size: 14px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.foot button:hover {
  background-color: #bd2130;
}

div button {
  color: white;
  background-color: #007bff;
  cursor: pointer;
  border: none;
  border-radius: 5px;
  font-size: 15px;
  padding: 5px 10px;
}

div button:hover {
  background-color: #0056b3;
  color: black;
}

</style>