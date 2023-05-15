<script setup>
import {ref, watch} from 'vue'

let todos = ref (JSON.parse(window.localStorage.getItem('todos',)))
let newTodo = ref('')


function TodoButton () {
  todos.value.push({
       text: newTodo.value, 
       complete: false 
       
      })

  newTodo.value =''
}

function deleteTodo (index) {
     todos.value.splice(index, 1)
  

}

watch(todos, function (value)
{
  window.localStorage.setItem('todos', JSON.stringify(value))
 
}, {deep:true})

</script>

<template>
  <h1> My Todo application</h1>
 <div class="stylediv">
  <ul>
    
 <li v-for="(todo, index) in todos">
  <button @click="deleteTodo(index)">X</button>
  {{ index + 1 }}
  <input type="checkbox" v-model="todo.complete" id="check">
  {{ todo.text }}

     
 </li>
</ul>
</div>

<input v-model="newTodo" @keydown.enter="TodoButton">
<button @click="TodoButton"> Add Todo</button>

  

  </template>


<style>
.stylediv  {
  background-color: rgb(38, 193, 204);
  background-size: 10px;
}

#check {
  margin: 50px;
            width: 15px;
            height: 15px;
            border: 12px solid rgb(0, 0, 0);
            padding: 10px;
            accent-color: rgb(20, 146, 28);
       
            opacity: 1;
            cursor: pointer;
            
}

#check:hover
 {
     
       color:rgb(2, 104, 119);
        }

</style>

