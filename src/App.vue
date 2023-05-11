<script setup>
import {ref} from 'vue'
let todos = ref ([])
let newTodo = ref('')


function TodoButton () {
  todos.value.push(newTodo.value)

  newTodo.value =''
}

function deleteTodo (index) {
     todos.value.splice(index, 1)
  

}
</script>

<template>
  <h1> My Todo application</h1>
 
  <ul>
    
 <li v-for="(todo, index) in todos">
  <button @click="deleteTodo(index)">X</button>
  {{ index + 1 }}
  {{ todo }}

     
 </li>
</ul>

<input v-model="newTodo" @keydown.enter="TodoButton">
<button @click="TodoButton"> Add Todo</button>

  
  
  </template>

<style>
todo  {
  background-color: rgb(11, 112, 78);
}


</style>

