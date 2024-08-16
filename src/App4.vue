<!-- Composition Api short -->
<script setup>
import {ref, onMounted} from 'vue';

const name = ref("John doe");
const status = ref('active');
const tasks = ref(['Tast 1','Task 2', 'Task 3']);
const newTask = ref('');

const toogleStatus = () => {
  if (status.value === "active") {
    status.value = 'pending';   
  } 
  else if( status.value === 'pending'){
    status.value = 'inactive';
  }
  else{
    status.value = 'active';
  }
};

const addTask = () =>{
  if (newTask.value.trim() !== ''){
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deteleTask = (index) =>{
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log('Error Feting data.')
  }
});
</script>

<template>

  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" name="newTask" id="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deteleTask(index)">x</button>  
    </li>
  </ul>

  <button @click="toogleStatus">Change Status</button>
 
</template>
