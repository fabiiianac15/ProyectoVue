<script setup>
import { ref } from 'vue';

let newTask = ref('')
let taskList = ref([
  {
   text: 'Estudiar', done: false 
  },
{
   text: 'Jugar Play', done: true 
   }
   ])

   function setDone(index){
    taskList.value[index].done = !taskList.value[index].done
   }

   function deleteTask(index){
    taskList.value.splice(index, 1)
   }

   function addTask(){
    if(newTask.value.trim()== '')return
    taskList.value.push({
      text: newTask.value,
      done: false
    })
    newTask.value = ''
   }
</script>

<template>
  <div class="card">
    <h1>Lista de cosas</h1>
    <p class="subtittle">{{ newTask }}</p>
    <div>
      <div v-for="(task, index) in taskList" :key="index" class="task" :class="{ done: task.done }">{{ task.text }} <span @dblclick="deleteTask(index)" @click="setDone(index)" class="button">x</span></div>
      <div>
        <input v-model="newTask" @keypress.enter="addTask" type="text" placeholder="Escribe tu Tarea">
        <p class="help" v-show="newTask != ''">Presiona enter para Configurar</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}

.help {
  margin: 0;
  font-size: 10px;
  opacity: 0.4;
}

.task {
  display: flex;
  justify-content: space-between;
  background-color: #D8E2DC;
  border-radius: 4px;
  padding: 2px 8px;
  padding-right: 2px;
  margin-bottom: 2px;
}

.subtittle {
  padding: 0;
  margin: 0;
  text-align: center;
  opacity: 0.6;
  margin-bottom: 16px;
}

h1 {
  text-transform: uppercase;
  text-align: center;
  padding: 0;
  margin: 0;
  font-size: 24px;
}

input {
  width: 100%;
  box-sizing: border-box;
  border: none;
  outline: none;
  padding: 3px 6px;
  border-radius: 4px;
}

.card {
  font-family: 'Roboto', sans-serif;
  background-color: #F8EDEB;
  max-width: 520px;
  border-radius: 8px;
  padding: 18px 16px;
  margin: 0 auto;
}

.task:hover {
  background-color: #CDB2AB;
}

.button {
  display: inline-flex;
  align-items: center;
  background-color: #FCD5CE;
  padding: 0 5px;
  border-radius: 2px;
  color: white;
}

.button:hover {
  cursor: pointer;
  background-color: orange;
}
</style>
