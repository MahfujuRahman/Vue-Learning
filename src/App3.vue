<!-- Composition Api Long -->

<script>
import {ref} from 'vue';

  export default {
    setup() {
      const name = ref("John doe");
      const status = ref('active');
      const tasks = ref(['Tast 1','Task 2', 'Task 3']);
      
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

      return {
        name, 
        status,
        tasks,
        toogleStatus,
      }
    },
  };
</script>

<template>

  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>

  <button @click="toogleStatus">Change Status</button>
 
</template>
