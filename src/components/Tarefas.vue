<template>
<div>
    <Progresso :percent="percent" />
    <div class="formData">
        <div>
            <input type="text" 
                   v-on:keyup.enter="addTask" 
                   v-model="taskData.message" 
                   placeholder="Nova tarefa?">
            <button @click="addTask" type="button">+</button>
        </div>
        
    </div>    
    <center>
    <div class="tarefas">
        <center>
            <Tarefa 
                :alterStatus="alterStatus" 
                :removeTask="removeTask"
                v-for="task in tasks" :task="task" />
        </center>
  </div></center>
</div>
</template>

<script>
import Progresso from './Progresso.vue'    
import Tarefa from './Tarefa.vue'
    
export default {
    components: {
        Progresso,
        Tarefa
    },
    data() {
        return {
            taskData: {
                id: this.unicId(),
                message: null,
                status: false
            },
            tasks: [
                     
            ]
        }
    },
    methods: {
        alterStatus(task) {
            this.tasks ? this.tasks.map(e => {                
                if (task.id === e.id) {
                    e.status = !e.status
                    this.alterStorage(e)
                }
            }) : null            
        },
        unicId() {
            var n = Math.floor(Math.random() * 11);
            var k = Math.floor(Math.random() * 1000000);
            return String.fromCharCode(n) + k;
        },
        addTask() {
            if (!this.taskData.message) {
                alert('Campo obrigatório')
            } else if (this.tasks.includes(this.taskData)) {
                alert('Tarefa ja existe')    
            } else {
                this.tasks.unshift(this.taskData)
                this.saveStorage(this.taskData)
                this.taskData = {id: this.unicId(), message: null, status: false}
            }               
        },
        removeTask(task) {
            this.tasks ? this.tasks.map((e, i) => {                
                if (task === e) {                    
                    this.tasks.splice(i, 1)
                    this.deleteStorage(task)
                    return {...this.tasks}
                }
            }) : null
        },
        saveStorage(task) { 
            let parseTasks = JSON.parse(localStorage.getItem('tasks')) || []
            parseTasks.unshift(task) 
            
            console.log(parseTasks)
            localStorage.setItem('tasks', JSON.stringify(parseTasks))
        },
        alterStorage(task) { 
            let parseTasks = JSON.parse(localStorage.getItem('tasks')) || []
       
            parseTasks.length !== 0 ? parseTasks.map(e => {
                 console.log(task.id === e.id)
                if (task.id === e.id) {
                    e.status = task.status
                } 
            }) : null 
            
            console.log(parseTasks)
            localStorage.setItem('tasks', JSON.stringify(parseTasks))
        },
        deleteStorage(task) {
            let parseTasks = JSON.parse(localStorage.getItem('tasks')) || []
       
            parseTasks.length !== 0 ? parseTasks.map((e,i) => {
                 console.log(task.id === e.id)
                if (task.id === e.id) {
                    parseTasks.splice(i, 1)
                } 
            }) : null 
            
            console.log(parseTasks)
            localStorage.setItem('tasks', JSON.stringify(parseTasks))
        }
    },
    computed: {
        percent() {
            let totalTasks = this.tasks.length || 0
            let doneTasks = 0
            if (totalTasks > 0){
                this.tasks.map(e => {
                    if (e.status) {
                        doneTasks += 1
                    }
                })
            }
            return totalTasks !== 0 ? Math.trunc((doneTasks * 100) / totalTasks) : 0
        }
    },
    created() {
        this.tasks = JSON.parse(localStorage.getItem('tasks'))
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    
    .tarefas {
        margin-top: 40px;
        width: 80%;
        margin-left: auto;
        margin-right: auto;
         display: inline-block;
    }
    
    
    .formData {           
        margin-top: 20px;
        display: flex;
        flex-direction: row;
        align-items: center; 
        justify-content: center;
    }
    
    .formData div {    
        display: flex;
        flex-direction: row;
        width: 50%;  
    }
    
    .formData div input {
        padding: 5px;
        background: linear-gradient(to right, #0f2027, #203a43, #2c5364);
        border: 1px solid gray;
        border-radius: 4px 0 0 4px;
        width: 90%;
        height: 20px;
        border-right: 0;
        color: #fff;
    }
    
    .formData div button {
        background-color: #4169E1;
        border: 1px solid gray;
        border-radius: 0 4px 4px 0;
        width: 30px;
        color: #fff;
    }
 
</style>
