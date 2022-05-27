<template>
  <div id="list">
    <ul li>
      <li v-for="task in list" :key="task.key">
        <span>{{task.text}}</span>
        <button @click="concluirTarefa(task.key)">Concluir</button>
      </li>
    </ul>
  </div>
</template>

<script>

export default{
  name: "ListComponent",
  props:['list', 'concluido'],
  methods:{
    concluirTarefa(key){   
      this.concluido(key)   
    }
  }
}
</script>

<style scoped>
  #list{
    white-space: pre-wrap;
    word-wrap: break-word;   
    padding: 0px 8px 0px 0px; 
  }

  ul{
    list-style: none;
    padding: 0;
    margin-top: 20px;
  }

  ul li{
    padding: 15px;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
    font: 400 0.85rem "Poppins";
    position: relative;  
  }

  li:not(:first-child){
    border-top: 1px solid #eee;
  }

  span{
    color: #0D2636;         
  }

  li::before{
    content:"";
    width: 5px;
    height: 5px;
    clip-path: circle();
    position: absolute;
    background: rgb(39, 167, 145);
    left: 0;
  }

  button{
    cursor: pointer;
    background: transparent;
    color: #000;
    border: 0;    
    outline: none;
    border-radius: 4px;
    font: 400 0.7rem "Poppins";
    transition: 0.1s;
  }
  
  button:hover{
    color: rgb(6, 150, 126);
    opacity: .6;
  }

</style>