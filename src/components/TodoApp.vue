<template>
  <div class="container" style:max-width="600px">
    <!-- <heading starts></heading> -->
    <h2 class="text-center mt-5">My Vue Todo app</h2>
    <!-- <--input---> 
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <button v-on:click="submitTask" class="btn btn-warning">SUBMIT</button>
    </div>
    <!-- <---task table---> 
      <table class="table table-bordered mt-5" >
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <th>
       <span :class="{'finished':task.status==='finished'}"> {{task.name}}</span>
        </th>
      <td style="width:120px">
        <span v-on:click="changeStatus(index)" class="pointer"
          :class ="{'text-danger':task.status === 'To-do',
          'text-warning':task.status === 'in-progress',
          'text-success':task.status === 'finished'
          }">
        {{ firstCharUpper(task.status) }}
      </span>
    </td>
      <td>
        <div class="text-center" v-on:click="editTask(index)">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td>
        <div class="text-center" v-on:click="deleteTask(index)">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>  
  </tbody>
</table>
  </div>
</template>

<script>

export default {
  name: 'TodoApp',
  data(){
    return{
      task:'',
      editedTask:'null',
      availableStateses:['To-do','in-Progress','finished'],
      tasks:[
        {
          name: 'Read some books',
          status:'To-do',
        },
        {
          name:'Do some physical activities',
          status:'in progress',
        }  
      ]
      }
    },
    methods:{
      submitTask(){
       if (this.task.length===0)return;
       if (this.editedTask===null){
       this.tasks.push({
        name:this.task,
        status:'To-do'
       });
      }
      else{
        this.tasks[this.editedTask].name=this.task;
        this.editedTask=null;

      }
       this.task='';

      },
      deleteTask(index){
        this.tasks.splice(index,1)
      },
      editTask(index){
        this.task = this.tasks[index].name;
        this.editedTask=index
      },
      changeStatus(index){
        let newIndex=this.availableStateses.indexOf(this.tasks[index].status);
        if(++newIndex >2) newIndex=0;
        this.tasks[index].status=this.availableStateses[newIndex];
    },
    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }};
</script>
<style scoped>
.pointer{
  cursor:pointer;
}
.finished{
  text-decoration:line-through;
}
</style>

