<template>
<div 
@click="$emit('toggle-reminder',taskDetail.id)"
:class="[taskDetail.reminder?'reminder':'','task']"
 >
 <h1>{{taskDetail.text}} <i class="fas fa-times" @click="deleteTask(taskDetail.id)"></i></h1>
<h1>{{taskDetail.day}}</h1>
</div>
   
</template>
<script>
export default {
    name:'individualTask',
    props:['taskDetail'],
    methods: {
        deleteTask (id) {
       this.$emit('delete-task',id);
        },
        toggleTask(id) {
            console.log(id);
        }
    }
}
</script>

<style scoped>
.fas {
    color: red;
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.task.reminder {
  border-left: 5px solid green;
}
.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
} 
</style>