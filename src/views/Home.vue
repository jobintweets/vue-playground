<template>
<div class = "container">


<AddTask @add-task= "saveTask" v-if = "showTaskForm"/>
<Tasks :tasksList= "tasks" @delete-task= "deleteMyTask" @toggle-reminder = "toggleReminder" />
 </div>
</template>
<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";
export default {
  name: 'HomeComponent',
  props:['showTaskForm'],
  components : {
     Tasks,
    AddTask,
  },
  data() {
    return {
      tasks : [],
    }
    },
     created() {
     this.fetchTasks().then(res=> {
       this.tasks = res;
     })
      console.log(this.tasks);
    },
     methods: {

      async  saveTask (data) {
        console.log(data);
        const res = await fetch('http://localhost:5000/tasks', {
          method: 'POST',
          headers: {
            'Content-type':'application/json',
            },
            body:JSON.stringify(data),
        });
        const newTask  = await res.json(); 
        this.tasks.push(newTask);
      },

      async deleteMyTask(id) {
        const res = await fetch (`http://localhost:5000/tasks/${id}`, {method:'DELETE'});
        res.status === 200 ?  this.tasks = this.tasks.filter((task)=>task.id!==id) : alert('Unable to delete');
       
        console.log(id);
      },

     async toggleReminder(id) {
        const taskToBeUpdated = await this.fetchSingleTask(id);
      //  const updatedTask ={...taskToBeUpdated,reminder:!taskToBeUpdated.reminder};
    taskToBeUpdated.reminder = !taskToBeUpdated.reminder;
        const res = await fetch (`http://localhost:5000/tasks/${id}`,{
          method:'PUT',
          headers:{
            'Content-type':'application/json'
          },
          body: JSON.stringify(taskToBeUpdated)
          })
const data = await  res.json();
       this.tasks.map((task)=> {
         if(task.id==id) {
            task.reminder = data.reminder;
          }
        })
      },

    
   async fetchTasks () {
const response = await fetch('http://localhost:5000/tasks');
const data     = await response.json();
return data;
    },

    async fetchSingleTask (id) {
      const response = await fetch(`http://localhost:5000/tasks/${id}`)
      const data     = await response.json();
return data;
    },
    },
  inheritAttrs: false, // disable 'non-props' warning
};
</script>