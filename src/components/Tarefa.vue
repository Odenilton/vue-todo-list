<template>
    <div @click="alterStatus(task)" class="tarefa" :class="task.status ? 'done' : 'undone'">
        <button type="button" @click="removeTask(task)">x</button>        
            <p>
              {{ task.message }}
            </p>             
    </div>
  
</template>

<script>
export default {
  props: ['task', 'alterStatus', 'removeTask']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
    .tarefa {    
        display: inline-block;
        padding: 10px 10px;
        width: 200px;        
        height: 70px;
        border-radius: 5px;      
        cursor: pointer;                
        margin: 0 20px 20px 0;
        align-self: baseline; 
    }
    
    .tarefa button {
        z-index: 100000;
        position: relative;
        float: right;
        border-radius: 10px;
        border: none;
        background-color: #808080;
        color: #fff;
        opacity:0.65;
	   -moz-opacity: 0.65;
	   filter: alpha(opacity=65);
    }
    
    .tarefa button:hover {
        background-color: #000;
        color: #fff;
    }
    
    .tarefa p {
        max-width:300px;
        max-height: 80px;
        color: #fff;
        word-wrap: break-word;
    }
    
    .done {
        border-left: 8px solid #006400;
        background-color: #32CD32;
        text-decoration: line-through;
        color: #fff;
    }
    .undone {
        border-left: 8px solid #A52A2A;
        background-color: #FF6347;
    }
</style>