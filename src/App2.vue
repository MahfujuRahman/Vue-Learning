<!-- options Api -->
<script>
  export default {
    data() {
      return {
        name: "John doe",
        status: 'active',
        tasks:['Tast 1','Task 2', 'Task 3'],
        link: 'https://google.com',
      };
    },
    methods:{
      toogleStatus() {
        if (this.status === "active") {
          this.status = 'pending';   
        } 
        else if( this.status === 'pending'){
          this.status = 'inactive';
        }
        else{
          this.status = 'active';
        }
      }
    }
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
  <a :href="link">google</a> <br>

  <button @click="toogleStatus">Change Status</button>
 
</template>
