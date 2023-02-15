<template>
  <div class="wrapper">
    <div class="todo-form">
      <h1> TO-DO LIST </h1>
      <form class="inputFiled" >
        <input placeholder="enter" v-model="newTodo" autocomplete="off">
        <button @click.prevent="create"> ADD </button>
      </form>
      <ul class="todo-list">
        <li v-for="item in todos" :key="item.id">
          <h3 :class="{done: item.completed}" @click="completed(item)">{{ item.content }}</h3>
          <button @click="remove(item)" class="remove"> Delete </button>
        </li>
      </ul>
      <div class="footer">
        <button @click="markAll"> Select All </button>
      </div>
    </div>
  </div>
</template>

<script>
//استراد ref لانشاء الخصائص التفاعلية 
import {ref } from 'vue';
export default{
  setup(){
    ///يمثل عناصر قائمه المهام وهي عبارة عن مصفوفه
    const todos=ref([])
    //المهمه التي يضيفها المستخدم 
    const newTodo= ref("")
    //make function to create input
    function create(){
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        completed: false
      })
      newTodo.value=""
    }
    //make function to delet item
    function remove(item){
      todos.value.splice(todos.value.indexOf(item),1)
    }
    //completed function
    function completed (item){
      item.completed = !item.completed
    }
    //select All
    function markAll(){
      todos.value.forEach((todo)=> todo.completed = true)
    }
    //use return to make return all function to template
    return{
      todos,
      newTodo,
      create,
      remove,
      completed,
      markAll
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  width: 100%;
  height: 100vh;
  padding: 10px;
  background: #f8f1f150;
}
.wrapper{
  width: 100%;
  max-width:500px;
  background: #fff;
  margin: 120px auto;
  padding:30px;
  border-radius:5px;
  box-shadow: 0px 5px 5px rgb(0,0,0,0.1);
}
.todo-form{
  text-align: center;
}
form{
  margin: 15px auto;
}
input{
  width: 80%;
  margin: 10px;
  height: 100%;
  padding: 5px 5px ;
  border-radius: 3px;
  border: 2px solid #ccc;
  font-size: 15px;
  transition: all 0.3s ease;
}
form button{
  width: 80%;
  background-color: rgba(0, 0, 0, 0.215);
  color: #fff;
  padding: 5px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  font-size: 17px;
  transition: all 0.3s ease;
}
.todo-list{
  text-align: start;
  margin-left: 10px auto;
  max-height: 250px;
  overflow-y: auto;
}
li{
  position: relative;
  list-style: none;
  margin-bottom: 10px;
  background: #faf6f6;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
  font-size:18px;
  display: flex;
  justify-content: space-between;
}
.remove{
  background: #295538;
  color: #fff;
  padding: 8px;
  border: none;
  border-radius: 2px;
}
.footer{
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button{
  padding: 6px 10px;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: #295538;
  cursor: pointer;
}
.done{
  text-decoration: line-through;
}
</style>



<!-- <template>
  <div class="wrapper">
    <h1> To-Do List</h1>
    <div>
      <form class="inputField" @submit.prevent="create">
        <input autocomplete="off" v-model="newTodo">
        <button> Add </button>
      </form>
    </div>
    <ul class="todoList">
      <li v-for="item in todos" :key="item.id">
        <h3 :class="{ done : item.completed}">{{ item.content }}</h3>
        <button @click="remove(item)"> delete </button>
      </li>
    </ul>
    <div class="footer">
      <button> select all </button>
    </div>
  </div>
</template>

<script>
//استراد ref لانشاء الخصائص التفاعلية 
import {ref } from 'vue';
export default{
  setup(){
    ///يمثل عناصر قائمه المهام وهي عبارة عن مصفوفه
    const todos=ref([])
    //المهمه التي يضيفها المستخدم 
    const newTodo= ref("")
    //make function to create input
    function create(){
      todos.value.push({
        id: Date.now(),
        content: newTodo.value,
        completed: false
      })
      newTodo.value=""
    }
    //make function to delet item
    function remove(item){
      todos.value.splice(todos.value.indexOf(item),1)
    }
    //use return to make return all function to template
    return{
      todos,
      newTodo,
      create,
      remove
    }
  }
}

</script>

<style>
*{
  margin: 0;
  padding: 0;
  font-family: 'Poppins',sans-serif;
}
body{
  width: 100%;
  height: 100vh;
  padding: 10px;
  background: #a9a9a9;
}
.wrapper{
  background: #fff;
  max-width: 400px;
  width: 100%;
  margin: 120px auto;
  padding: 25px;
  border-radius: 5px;
  box-shadow: 0px 10px 15px rgba(0,0,0,0.1);
}
input{
  width: 90%;
  margin: 20px 0;
  height: 100%;
  border-radius: 3px;
  border: 3px solid #ccc;
  font-size: 17px;
  padding: 5px 5px;
  transition: all 0.3s ease;
}
form button{
  width: 90%;
  height: 100%;
  border: none;
  color: #fff;
  margin-left: 5px;
  font-size: 21px;
  outline: none;
  background: #454545;
  cursor: pointer;
  border-radius: 3px;
  pointer-events: none;
  transition: all 0.3s ease;
}
.wrapper .todoList{
  margin-top: 20px;
  max-height: 250px;
  overflow-y: auto;
}
li{
  position: relative;
  list-style: none;
  margin-bottom: 8px;
  background: #d3d3d3;
  border-radius: 3px;
  padding: 10px 15px;
  cursor: default;
  overflow: hidden;
  word-wrap: break-word;
}
.footer{
  display: flex;
  width: 100%;
  margin-top: 20px;
  align-items: center;
  justify-content: space-between;
}
.footer button{
  padding: 6px 10px;
  border-radius: 3px;
  border: none;
  color: #fff;
  background: #295538;
  cursor: pointer;
}
.done{
  text-decoration: line-through;
}
</style> -->
