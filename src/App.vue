<script setup>
import {ref, watch} from 'vue'

let todos = ref (JSON.parse(window.localStorage.getItem('todos',)) ??([]))
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
  <div class="container">
  <h1> My Todo application</h1>
 <div class="stylediv">
  <ul>
    
 <li v-for="(todo, index) in todos" :class="{completed: todo.complete}">
  <button @click="deleteTodo(index)">X</button>
  {{ index + 1 }}
  <label class="container">
  <input type="checkbox" v-model="todo.complete">
  <span class="checkmark"></span>
</label>
  {{ todo.text }}


 </li >
</ul>
</div>
</div>

<input v-model="newTodo" @keydown.enter="TodoButton">
<button @click="TodoButton"> Add Todo</button>

  

  </template>


<style>
.stylediv  {
  background-color: rgb(159, 232, 238);
  background-size: 10px;
  border-radius: 30px;
}

.completed {
text-decoration: line-through;
color:darkgrey
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
            text-decoration: line-through;
}

#check:hover
 {
     
       color:rgb(2, 104, 119);
        }
       
       
        .container {
  
  position: relative;
  padding-left: 25px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Hide the browser's default checkbox */
.container input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: rgb(251, 0, 0);
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: rgb(255, 255, 255);
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #00af3d;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.container input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.container .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid rgb(0, 0, 0);
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}




</style>

