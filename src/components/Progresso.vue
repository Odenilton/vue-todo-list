<template>
  <div class="progresso">
    <h2>{{ title }}</h2>
    <div class="barra">
        <div :style="{width: percent + '%'}"  class="conteudo-barra">
            
        </div>  
        <div class="conteudo-barra-percent">
                {{ percent }}% concluidas
            </div>
    </div>
      
  </div>
</template>

<script>
export default {
    props: ['percent'],
    data() {
        return {
            title: 'Tarefas',
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .progresso {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .barra {
        display: flex;
        flex-direction: column;        
        align-items: center;
        border: 1px solid gray;
        width: 80%;
        height: 20px;
        border-radius: 5px;
    }
   
    .conteudo-barra {
        align-self: baseline;        
        height: 100%;   
        background-color: #32CD32;
        border-radius: 5px;
    }
    
    .conteudo-barra-percent {
        position: absolute;
        margin: 0 auto;
        color: #fff;  
        display: flex;
        align-items: center;
    }
    
    h2 {
        color: #fff;
    }
</style>
