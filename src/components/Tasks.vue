<template>
    <h1>List of all tasks</h1>
    <div v-for = "task in tasksList"  :key = "task.id" >
        <IndividualTaskVue 
        :taskDetail="task"
    @delete-task="$emit('delete-task',task.id)" 
      @toggle-reminder="$emit('toggle-reminder',task.id)" 
      />
    </div>
    <hr>
  
</template>

<script>
import IndividualTaskVue from "./IndividualTask.vue"
export default {
    name      : 'taskComponent',
    props     : ['tasksList'],
    components: {
       IndividualTaskVue,
    },
    emits :['delete-task','toggle-reminder']

}
</script>

<style scoped>
</style>