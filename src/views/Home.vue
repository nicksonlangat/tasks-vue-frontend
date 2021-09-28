<template>
   <!-- component -->
<div class="h-100 w-full flex items-center justify-center bg-red-100 font-sans">
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
        <div>
            <div class="flex mb-4 items-center">
                <p class="w-full text-grey-darkest">Add another component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-green border-green hover:bg-green-800">Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
          	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
            	<div class="flex mb-4 items-center">
                <p class="w-full line-through text-green">Submit Todo App Component to Tailwind Components</p>
                <button class="flex-no-shrink p-2 ml-4 mr-2 border-2 rounded hover:text-white text-grey border-grey hover:bg-red-700">Not Done</button>
                <button class="flex-no-shrink p-2 ml-2 border-2 rounded text-red border-red hover:text-white hover:bg-red-900">Remove</button>
            </div>
        </div>
    </div>
</div>
</template>
<script>
import TaskService from '../services/TaskService'
export default {
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
    saveTask(){
      let data={
        title:this.task.title,
        description:this.task.description
      };
      // console.log(data)
      TaskService.create(data).then(response=>{
        this.task.id=response.data.id;
        console.log(response.data);
        this.is_submitted=true;
      }).catch(error=>{
        console.log(error)
      });
    },

    
  }
}
</script>
