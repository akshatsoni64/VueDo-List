<template>
  <div id="app" class="container-fluid text-center">
    <h1 class="text-info">{{ title }}</h1>
    <p>{{ msg }}</p>

    <div class="col">
      <div v-if="error" class="alert alert-danger" @click="error = !error">
        <strong>Error:</strong> Please add the task name first!
      </div>
      <form @submit.prevent="addTask">
        <div class="input-group mb-3">
          <input type="text" class="form-control" placeholder="Task Name" v-model="taskName">
          <div class="input-group-append">
            <button v-if="update" class="btn btn-warning" type="submit">
              <i class="fa fa-pencil" aria-hidden="true"></i>
            </button>
            <button v-else class="btn btn-success" type="submit">
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
          </div>
        </div>
      </form>

      <button v-if="deleteMultiple" class="btn btn-danger mb-3" @click="deleteMulti">Delete Selected</button>

      <ul class="list-group">
        <li v-for="(task_name,index) in tasks" :key="index" class="list-group-item list-group-item-info">
          <div class="row">
            <div class="col-2">
              <input type="checkbox" @change="changeCheck" :id="task_name['index']" class="form-control">
            </div>
            <div class="col" @click="loadData(index)">{{ task_name['task'] }}</div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      title: 'VueDo List',
      msg: 'Welcome to Your First ToDo List App with Vue.js',
      taskName: "",
      tasks: [
        {"index": 0, "task": 'Download VueJS'},
        {"index": 1, "task": 'Install Node Modules'},
        {"index": 2, "task": 'Run NodeJS Server'}
      ],
      error: false,
      update: false,
      updateIndex: null,
      ids: [],
      deleteMultiple: false
    }
  },
  methods: {
    deleteMulti: function(e){
      console.log("Deleting Multiple tasks");
      this.ids.forEach(id => {
        console.log(id);
        this.tasks = this.tasks.filter(function(task) {
          return task['index'] != id;
        });
        console.log(this.tasks);
      });
      this.deleteMultiple = false;
      this.ids = [];
    },
    changeCheck: function(e){
      if(e.target.checked){
        this.ids.push(e.target.id);
      }
      else{
        this.ids = this.ids.filter((id) => {
          return id != e.target.id
        })
      }
      this.deleteMultiple = ((this.ids.length >= 1)) ? true : false;

      console.log(this.ids);
    },
    loadData: function(index){
      this.taskName = this.tasks[index]['task']
      this.updateIndex = index
      this.update=true
    },
    addTask: function(){
      if(this.update == true){

        this.update = false
        this.tasks[this.updateIndex][this.updateIndex] = this.taskName

      }
      else{

        if(this.taskName != ''){
          this.tasks.push(this.taskName)
        }
        else{
          this.error = true
        }

      }

      this.taskName = ''
    },
  }
}
</script>

<style>
</style>
