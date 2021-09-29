<template>
    <div>
            <div class="flex mb-4 items-center"
            :class="{active: index == currentIndex }"
             v-for="(task, index) in tasks" :key="index"
             @click="setActiveTask(task, index)"
             >
                
                 <p  v-if="task.is_complete" class="w-full line-through text-green-900">{{task.title}}</p>
                 <p   v-else  class="w-full text-grey-darkest">{{task.title}}</p>
                <button 
                v-if="!task.is_complete" 
                @click="markDone(task, index)"
                class="flex-no-shrink p-2 ml-4 mr-2 border-2
                 rounded hover:text-white text-green-500 border-green-600 hover:bg-green-800">Done</button>
                
                <button 
                v-if="task.is_complete" 
                @click="markUnDone(task, index)"
                class="flex-no-shrink p-2 ml-4 mr-2 border-2
                 rounded hover:text-white text-red-500 border-red-600 hover:bg-red-800">Undo</button>
                <button 
                  @click="deleteTask(task, index)"
                class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
    </div>
</template>
<script>
import TaskService from '../services/TaskService'
export default {
    data(){
        return{
            tasks:[],
            currentTask:null,
            currentIndex:-1,
            title:'',
        };
    },
    methods:{
         retrieveTasks(){
            TaskService.getAll().then(response=>{
                this.tasks=response.data
                console.log(response.data)
            }).catch(error=>{
                // console.log(error)
            });
            },

            refreshList(){
                this.retrieveTasks();
                this.currentTask=null;
                this.currentIndex=-1;
            },

            setActiveTask(task, index){
                this.currentTask=task;
                this.currentIndex=index;
                // console.log(this.currentTask.title)
            },

        
        markDone(task, index){
            this.currentTask=task;
            this.currentIndex=index;
            let data={
                id:this.currentTask.id,
                title:this.currentTask.title,
                description:this.currentTask.description,
                is_complete:true,
            }
            // console.log(data)
            TaskService.update(this.currentTask.id, data).then(response=>{
                // console.log(response.data);
                this.retrieveTasks();
            }
            )
        },

        markUnDone(task, index){
            this.currentTask=task;
            this.currentIndex=index;
            let data={
                id:this.currentTask.id,
                title:this.currentTask.title,
                description:this.currentTask.description,
                is_complete:false,
            }
            // console.log(data)
            TaskService.update(this.currentTask.id, data).then(response=>{
                // console.log(response.data);
                this.retrieveTasks();
            }
            )
        },
        deleteTask(task, index){
            this.currentTask=task;
            this.currentIndex=index;
            TaskService.delete(this.currentTask.id).then(response=>{
                this.retrieveTasks();
            }
            )
        }
    },
    mounted(){
               this.retrieveTasks()
            },
    created(){
        this.$root.$refs.Tasks=this;
    }
}
</script>