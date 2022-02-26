<template>
    <header>
        <h1>Task Tracker {{titles}} </h1>
  
   <ButtonVue 
   :text="buttonColor?'Close':'Add Task'"
    :color="buttonColor?'red':'blue'" 
    @show-task="$emit('show-task',true)" 
    v-show="homePage"
    />
    </header>
</template> 
<script>
import ButtonVue from "./Button.vue";
export default {
name: 'HeaderVue',
props : ['titles','buttonColor'],
components:{
    ButtonVue
},
computed: {
    homePage() {
        if(this.$route.path === '/') {
            return true;
        }
        else{return false} 
    }
 }
    
}
</script>

<style scoped>
header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    }
    p {
        color:red
    }
</style>