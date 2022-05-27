<template>
  <div id="app">  
    <header>
      <h1>Minhas Tarefas</h1>
      <img src="../src/assets/logo.png"/>
    </header>
    
    <Task />
  </div>
</template>

<script>
import Task from './components/Task.vue';

export default {
    name: "App",
    components: { 
      Task 
    }
}
</script>

<style scoped>
  #app{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;  
    height: 100vh;  
  }

  header{
    display: flex;
    align-items: center; 
    gap: 25px; 
  }

  header h1{
    color: rgb(34, 33, 33)  
  }

  header img{
    width: 48px;    
  }
</style>
