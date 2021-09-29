<template >
   <!-- component -->
<div class=" w-full flex items-center justify-center bg-gray-300 font-sans">
	<div class="bg-white rounded shadow p-6 m-4 w-full lg:w-3/4 lg:max-w-lg">
        <div class="mb-4">
            <h1 class="text-grey-darkest">Todo List</h1>
            <div class="flex mt-4">
                <input 
                id="title"
                v-model="task.title"
                name="title"
                class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"
                placeholder="Task Title">
                 <input 
                 id="description"
                v-model="task.description"
                name="description"
                 class="shadow appearance-none border rounded w-full py-2 px-3 mr-4 text-grey-darker"
                placeholder="Optional description">
                <button  @click="saveTask" class="flex-no-shrink p-2 border-2 rounded text-blue-800 border-teal 
                hover:text-white hover:bg-green-600">Add</button>
            </div>
        </div>
        <!-- List of tasks -->
        <Tasks/>
    </div>
</div>
</template>
<script>
import TaskService from '../services/TaskService'
import Tasks from './Tasks.vue'
export default {
  components:{
    Tasks
  },
  data(){
    return {
      task:{
        id:null,
        title:'',
        description:'',
      },
      is_submitted:false
    };
  },

  methods:{
    refresh:function(){
      this.$root.$refs.Tasks.retrieveTasks();
    },
    clearForm(){
       this.task.title='';
       this.task.description='';
    }
    ,
    saveTask(){
      let data={
        title:this.task.title,
        description:this.task.description
      };
      console.log(data)
      TaskService.create(data).then(response=>{
        this.task.id=response.data.id;
        // console.log(response.data);
        this.is_submitted=true;
        this.clearForm();
        this.refresh();
      }).catch(error=>{
        console.log(error)
      });
    },
  }
  
}
</script>
