<template>
  <div id="task">
    <form @submit.prevent="incluirTarefas">
      <input 
        type="text"
        placeholder="Digite sua tarefa" 
        v-model="tarefa"
      />
      <button type="submit">Adicionar</button>
    </form>    

    <List :list="tarefas" :concluido="concluirItem"/>

    <footer v-show="tarefas.length > 0">
      <span class="mensagem">
        Você tem 
          <strong :class="{pend: pendente}">{{tarefas.length}}</strong> 
        tarefa pendente(s)
      </span>
      <button @click="tarefas = []">Limpar agenda</button>
    </footer>   

  </div>
   
</template>

<script>
import List from "./List.vue";
  
  export default{
  name: "taskComponent",
  data() {
    return {
      tarefa: "",
      tarefas: [],
      pendente: false
    };
  },
  components:{
    List,
  },
  methods: {
    incluirTarefas() {
      if (this.tarefa !== "") {
        this.tarefas.push({
          text: this.tarefa,
          key: Date.now()
        }),

        this.tarefa = "";
      }
      else {
        alert("Não há tarefas a serem registradas!");
      }
    },
    concluirItem(key){
      let filter = this.tarefas.filter((item) => {
        return (item.key !== key);
      })      
      return this.tarefas = filter
    }
  },
  watch:{
    tarefas:{
      deep: true,
      handler(){
        localStorage.setItem("@minha-agenda", JSON.stringify(this.tarefas))
        this.tarefas.length > 4 ? this.pendente = true : this.pendente = false
        ;
      }
    }       
  },
  created(){
    let retornoLocalStorage = localStorage.getItem("@minha-agenda");

    this.tarefas = JSON.parse(retornoLocalStorage) || [];    
  }
}  
</script>

<style scoped>
  #task{
    background-color: #fff;   
    margin: 2rem auto;   
    max-width: 700px; 
    max-height: 50%;  
    overflow-y: scroll;
    padding: 20px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);     
  }  

  form{
    margin-top: 1.2rem;
    margin-bottom: -1rem;
    display: flex;
    flex-direction: row;
    gap: 1rem;
    align-items: center;
  }

  form button{
    border: 0;
    padding: 5px 15px;
    cursor: pointer;    
    align-items: center;  
    background-color: rgb(48, 255, 220);
    font: 500 13px "poppins";
    border-radius: 25px;
  }

  form input{
    flex: 1;
    border: 1px solid rgba(72, 71, 71, 0.229);
    padding: 6px 10px;
    font: 400 13px "Poppins";
    outline: none;    
    border-radius: 8px;
  }

  form input:focus::placeholder{
    color: rgb(177, 175, 175);
  }

  .mensagem{
    font: 400 10px "Poppins";
  }

  .mensagem .pend{
    color: #ff0000;
  }

  footer{
    display: flex;
    justify-content: space-between;
    align-items:center;
    margin-top: 1rem;     
  }

  footer button{
    border: none;
    background: transparent;  
    color: rgb(196, 195, 195);
    font: 500 11px "poppins";
    cursor: pointer;
  }

  footer button:hover{
    color: red;
  }

</style>