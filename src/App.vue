<template>

  <h1> To-Do app</h1>  

  <form @submit.prevent= 'addNewTodo'>
    <label> New Todo </label>
    <input v-model='newTodo' name="newTodo">
    <button> Add new todo </button>
  </form>
  
  <button @click="markAllDone"> All done</button>
  <button @click="removeAll"> Remove all</button>
  <ul>
  <li v-for="(todo,index) in todos" :key="todo.id" :class="todo">
    <h2 :class="{done: todo.done }" @click="toggleDone(todo)">{{todo.content}}</h2>
  <button @click="removeTodo(index)"> Remove Todo </button>
  </li>
  </ul>

</template>

<script>
import { ref } from 'vue';

const newTodo = ref('');
const todos = ref([]);

export default{
  setup(){
    function addNewTodo(){
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = ''
  }

    function toggleDone(todo){
      todo.done =!todo.done
    }

    function removeTodo(index){
      todos.value.splice(index,1)
    }

    function markAllDone(){
      todos.value.forEach((todo) => todo.done =true);
    }

    function removeAll(){
      todos.value = [];
    }

    return{
      newTodo,
      addNewTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAll,
    }
  }
}

</script>


<style scoped>
.done{
  text-decoration: line-through;
}
.todo{
  cursor: pointer;
}
</style>
