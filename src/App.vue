<template >
<label class="label">Todo List</label>
<input v-on:keyup.enter="addNewTodo" v-model="newTodo" name="newTodo">
  <form class="form" @submit.prevent ="addNewTodo">
    <button class="button">Add a Todo</button>
   
  </form>
  <div class="buttonForm">
   <button class="button" @click="markAllDone">Mark all done</button>
    <button class="button " @click="removeAllTodos">Remove all todos</button>
  </div>
  <ul class="todos">
    <li v-for="(todo,index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button class="buttonRemove" @click="removeTodo(index)">X</button>
    </li>
  </ul>
  
  
</template>

<script>
import { ref } from 'vue';
//import HelloWorld from './components/HelloWorld.vue'

export default {
  setup() {
    const newTodo = ref('');
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,   
      });
      newTodo.value = '';
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index,1);
    }

    function markAllDone() {
      todos.value.forEach((todo)=> todo.done = true);
    }

    function removeAllTodos() {
      todos.value = [];
    }


    return{
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
    };
  }

  
};
</script>

<style>

form {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
 
}
body {
  font-family: sans-serif;
  padding-bottom: 1em;
  font-size: 2em;
  width: 90%;
  margin: 0 auto ;
  background: rgb(2,0,36);
background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(2,69,18,1) 35%, rgba(0,212,255,1) 100%);
}
input {
  display: block;
  width: 70%;
  font-family: sans-serif;
  font-size: 0.7em;
  margin: 0.5em ;
  margin-right: auto;
  margin-left: auto;
  border: 1px solid #6cf89b; /*цвет рамки*/
   border-radius: 3px; /*закругление углов (общее)*/
   -webkit-border-radius: 3px; /*закругление углов (Google Chrome)*/
   -moz-border-radius: 3px; /*закругление углов (FireFox)*/
   -khtml-border-radius: 3px; /*закругление углов (Safari)*/
   background: #d6e4e0 !important; /* желательно прописывать, так как в Chrome при сохранных данных оно может быть желтым*/
   outline: none; /* удаляет обводку в браузерах хром(желтая) и сафари(синяя)*/
   height: 24px; /* высота на свое усмотрение*/
   width: 400px; /* ширина на свое усмотрение*/
   color: #049423; /*цвет шрифта в обычном состоянии*/
   font-size: 11px; /* Размер шрифта*/
   font-family: Tahoma; /* Стиль шрифта*/
  
}
.label {
  display: block;
  font-size: 40px;
  width: 100%;
  text-align: center;
  font-family: Snell Roundhand, cursive;
  color: #03310d65;
}

.todo {
  display: flex;
  cursor: pointer;
  border: 1px solid #6cf89b;
  font-family: Snell Roundhand, cursive;
  align-items: center;
  justify-content: center;
  
}
.todos {
  display: inline;
  color: #2bfa58;
    
}
.done {
  text-decoration: line-through;

}
.button {
  background-color: #42a102; 
  /* border: 3px; */
  color: rgb(0, 83, 38);
  padding: 10px 20px;
  text-decoration: none;
  font-size: 16px;
  -webkit-transition-duration: 0.4s; 
  transition-duration: 0.4s;
  cursor: pointer;  
  display: block;
  float: left; 
  font-family: Snell Roundhand, cursive;

}
.button:hover {
    background-color: #7bce2d; /* Green */
    color: white;
}
.buttonForm {
  display: flex;
  width: 100%;
  height: 48px;
  align-items: center;
  justify-content: center;
}
.buttonRemove {
  color: rgb(81, 253, 75);
  cursor: pointer;
  background: rgba(205, 214, 219, 0);
  border-radius: 3px;

}
</style>
