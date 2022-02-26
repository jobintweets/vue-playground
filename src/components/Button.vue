<template>
    <button @click="addTask()" class="btn" :style="{background:color}">{{text}}</button>
   
</template>

<script>
export default {
   
    'name':'ButtonComponent',
    props:['text','color'],
    methods: {

     addTask() {
         console.log('Task added');
         this.$emit('show-task',true);
     }

    }
    }
</script>

<style scoped>

</style>