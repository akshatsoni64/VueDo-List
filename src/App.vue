<template>
  <div id="app" class="container-fluid text-center">
    <h1 class="text-info">{{ title }}</h1>
    <p>{{ msg }}</p>

    <div class="col">
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
        <li v-for="task_name in tasks" :key="task_name" @click="delTask" class="list-group-item list-group-item-info">{{ task_name }}</li>
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
      tasks: ['First', 'Second', 'Third']
    }
  },
  methods: {
    addTask: function(){
      this.tasks.push(this.taskName)
      this.taskName = ''
    },
    delTask: function(event){
      this.tasks = this.tasks.filter((task)=>{
        return task != event.target.innerHTML
      })
    }
  }
}
</script>

<style>
</style>
