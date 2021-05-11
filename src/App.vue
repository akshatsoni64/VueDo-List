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
            <button class="btn btn-success" type="submit">
              <i class="fa fa-plus" aria-hidden="true"></i>
            </button>
          </div>
        </div>
      </form>

      <ul class="list-group">
        <li v-for="task_name in tasks" :key="task_name" class="list-group-item list-group-item-info">
          <div class="row">
            <div class="col">{{ task_name }}</div>
            <div class="col text-right">
              <i class="fa fa-trash" aria-hidden="true" @click="delTask(task_name)"></i>
            </div>
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
      tasks: ['Download VueJS', 'Install Node Modules', 'Run NodeJS Server'],
      error: false
    }
  },
  methods: {
    addTask: function(){
      if(this.taskName != ''){
        this.tasks.push(this.taskName)
      }
      else{
        this.error = true
      }
      this.taskName = ''
    },
    delTask: function(taskname){
      this.tasks = this.tasks.filter((task)=>{
        return task != taskname
      })
    }
  }
}
</script>

<style>
</style>
