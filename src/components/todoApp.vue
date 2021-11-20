<template>
  <div class="container">
<h2 class="text-center mt-5">My Todo App</h2>
<div class="d-flex">
<input v-model="task" type="text" placeholder="Enter task" class="form-control"/>
<button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
</div>
<table class="mt-5 table table-bordered">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col">#</th>
      <th scope="col">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task,index) in tasks" :key="index">
      <td scope="row">
      <span :class="{'finished':task.status==='finished'}">
      {{task.name}}
      </span>
      </td>
      <td>
      <span @click="changesStatus(index)" :class="{'text-danger': task.status==='todo',
      'text-warning': task.status==='in-progress',
      'text-success': task.status==='finished'
      }" class="pointer">{{firstCharUpper(task.status)}}</span>
      </td>
      <td>
      <div class="text-center" @click="editTask(index)">
      <span class="fa fa-pen"></span>
      </div>
      </td>
      <td>
      <div class="text-center"  @click="deleteTask(index)">
      <span class="fas fa-trash"></span>
      </div>
      </td>
    </tr>
 
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'todoApp',
  props: {
    msg: String
  },

data(){
return {
task:'',
editedTask:null,
availableStatuses:['todo','in-progress','finished'],
tasks:[
{
name:'Steal banans from the store',
status:'to-do'

},
{
name:'Eat 1kg chocolate in hour',
status:'in-progress'

}


]
}
},
  


  methods:{
  submitTask(){
 if(this.task.length===0) return 0;
 if(this.editedTask ===null){
 
 
 this.tasks.push({
 name:this.task,
 status:'todo'
 });
 }else{
 this.tasks[this.editedTask].name = this.task;
 this.editedTask=null;
 }
  this.task = '';
    },

  deleteTask(index){
  this.tasks.splice(index,1);
  },
  editTask(index){

this.task =  this.tasks[index].name;
this.editedTask=index;
  },

  changesStatus(index){
  let newIndex =  this.availableStatuses.indexOf(this.tasks[index].status);
  if(++newIndex >2) newIndex=0;
  this.tasks[index].status = this.availableStatuses[newIndex];
  },
  firstCharUpper(str){
  return str.charAt(0).toUpperCase()+str.slice(1);
  
  }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pointer{
cursor:pointer
}


.finished{
text-decoration: line-through;
}
</style>
