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
              <input type="checkbox" :checked="task_name['check']" @change="changeCheck" :id="task_name['index']" class="form-control">
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
        {"index": 0, "task": 'Download VueJS', "check": false},
        {"index": 1, "task": 'Install Node Modules', "check": false},
        {"index": 2, "task": 'Run NodeJS Server', "check": false},
        {"index": 3, "task": 'Open App', "check": false},
        {"index": 4, "task": 'Add Task', "check": false},
        {"index": 5, "task": 'Update Task', "check": false},
        {"index": 6, "task": 'Delete Task', "check": false}
      ],
      error: false,
      update: false,
      updateIndex: null,
      ids: [],
      deleteMultiple: false
    }
  },
  updated: function(){
    console.log("UPDATED----");
    this.tasks.forEach((task) => {
      console.log(task.task,  "--", task.check);
    });
    console.log("----");
  },
  methods: {
    deleteMulti: function(e){
      this.tasks.forEach((task) => {
        console.log(task.task, task.check);
      });
      console.log("----");
      var ids = [];
      this.tasks.forEach((task) => {
        if(task.check == true){
          ids.push(task.index)
        }
      });
      ids.forEach(id => {
        this.tasks = this.tasks.filter(function(task) {
          return task['index'] != id;
        });
      });
      this.deleteMultiple = false;
      this.tasks.forEach((task) => {
        console.log("DELETE:", task.task, task.check);
      });
    },

    changeCheck: function(e){
      this.tasks[e.target.id]['check'] = e.target.checked
      var count = 0
      this.tasks.forEach((task) => {
        if(task.check == true){
          count = count + 1
        }
      })
      this.deleteMultiple = (count > 0) ? true : false
      console.log("changeCheck");
      this.tasks.forEach((task) => {
        console.log(task.task, task.check);
      });
    },

    loadData: function(index){
      console.log(this.tasks)
      this.taskName = this.tasks[index]['task']
      this.updateIndex = index
      this.update=true
    },

    addTask: function(){
      if(this.update == true){

        this.update = false
        this.tasks[this.updateIndex]['task'] = this.taskName

      }
      else{
        var theIndex = this.tasks.length;
        if(this.taskName != ''){
          this.tasks.push({
            "index": theIndex,
            "task": this.taskName,
            "check": false
            })
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
