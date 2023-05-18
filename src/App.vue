<script setup>
import {ref, watch} from 'vue'

let todos = ref (JSON.parse(window.localStorage.getItem('todos',)) ??([]))
let newTodo = ref('')
let filter = ref ('all')

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

function todoFilter (todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else if (filter.value == 'complete') {
    return todo.complete == true
  } else {
    return true
  }
}

function activeFilter (todo) {

    return todo.complete == false

}

</script>

<template>
  <div>
  <h1> My Todo application</h1>
  <p v-if="todos.length > 0">
    <input name="filter" type="radio" value="all" v-model="filter">
    <label>All</label>
    <input name="filter" type="radio" value="active" v-model="filter">
    <label>Active</label>
    <input name="filter" type="radio" value="complete" v-model="filter">
    <label>Complete </label>
  </p>
  <p>{{   todos.filter(activeFilter).length}} items left</p>
  <input v-model="newTodo" @keydown.enter="TodoButton" class="input">
<button @click="TodoButton"> Add Todo</button>

 <div class="stylediv">
  

  <ul>
    
 <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{completed: todo.complete}">
  <button @click="deleteTodo(index)" class="Xmark">X</button>
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



  </template>


<style>
.stylediv  {
  color:rgb(153, 184, 211);
  background-color: rgb(255, 255, 255);
  background-size: 10px;
  border-radius: 0px;
  max-width: 1000px;
  max-height:max-content;
  box-shadow: rgba(245, 6, 106, 0.17) 0px -23px 25px 0px inset, rgba(255, 0, 195, 0.15) 0px -36px 30px 0px inset, rgba(101, 1, 32, 0.1) 0px -79px 40px 0px inset, rgba(255, 5, 5, 0.06) 0px 2px 1px, rgba(160, 3, 165, 0.09) 0px 4px 2px, rgba(167, 30, 119, 0.09) 0px 8px 4px, rgba(61, 1, 1, 0.09) 0px 16px 8px, rgba(185, 3, 236, 0.09) 0px 32px 16px;
  
}


.completed {
text-decoration: line-through;
color:rgb(0, 234, 62)
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
  background-color: rgba(181, 190, 183, 0.907);
  border-radius: 360px;
}

/* On mouse-over, add a grey background color */
.container:hover input ~ .checkmark {
  background-color: rgb(135, 0, 0);
}

/* When the checkbox is checked, add a blue background */
.container input:checked ~ .checkmark {
  background-color: #00af3d;
  border-radius: 360px;
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  
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

.Xmark 
  
 {
  appearance: none;
  background-color: #FFFFFF;
  border-radius: 40em;
  border-style: none;
  box-shadow: #ADCFFF 0 -12px 6px inset;
  box-sizing: border-box;
  color: #000000;
  cursor: pointer;
  display: inline-block;
  font-family: -apple-system,sans-serif;
  font-size: 0.4rem;
  font-weight: 700;
  letter-spacing: -.24px;
  margin: 0;
  outline: rgb(0, 0, 0);
  padding: .20rem .50rem;
  quotes: auto;
  text-align: center;
  text-decoration: none;
  transition: all .15s;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  
}

.Xmark:hover {
  background-color: #ff0000;
  box-shadow: #d60047 0 -6px 8px inset;
  transform: scale(1.125);
}

.Xmark:active {
  transform: scale(.5);
}

@media (min-width: 768px) {
  .Xmark {
    font-size: 1.5rem;
    padding: .75rem 2rem;
  }
}


</style>

