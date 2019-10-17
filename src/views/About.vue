<template>

  <div class="hello">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Navbar</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
<div>This is Bar {{ this.$route.params.id }}</div>
      <input v-model="ds" id="dsinput" class="form-control" placeholder="this el bar">


  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item ">
        <router-link to="/">Home</router-link> |
      </li>
      <li class="nav-item">
          <router-link :to="{ name: 'about', params: { id: this.variable }}">About</router-link>      </li>
      <li class="nav-item">
         <router-link to="/about2">About2</router-link> |
      </li>
      <li class="nav-item">
 <router-link to="/">Home</router-link> |      </li>
    </ul>
  </div>
</nav>

    <div id="todo-list-example" class="container">
      <div class="row">
        <div class="col-md-6 mx-auto">
          <h1 class="text-center">TODO List App 2</h1>
          <form v-on:submit.prevent="addNewTask">
            <label for="tasknameinput">Task Name</label>
            <input v-model="taskname" id="tasknameinput" class="form-control" placeholder="Add New Task">
            <button v-if="this.isEdit == false" type="submit" class="btn btn-success btn-block  mt-3">
              Submit
            </button>
            <button v-else type="button" v-on:click="updateTask()" class="btn btn-primary btn-block  mt-3">
              Update
            </button>
          </form>

          <table class="table">
            <tr v-for="(todo) in todos" v-bind:key="todo.id" v-bind:title="todo.task_name">
              <td class="text-left">{{todo.task_name}}</td>
              <td class="text-right">
                <button v-on:click="editTask(todo.task_name, todo.id)" class=" btn btn-info ">Edit</button>
                <button v-on:click="deleteTask(todo.id)" class=" btn btn-danger ">Delete</button>
              </td>
            </tr>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from 'axios'
  export default {
    data() {
      return {
        todos: [],
        id: '',
        taskname: '',
        isEdit: false,
        ds: '',
        variable: 'conejo de campo'
        
      }
    },
    
    mounted() {
      this.getTasks(),
      this.ds=this.$route.params.id
      
    },
    methods: {
      getTasks() {
        axios.get('http://173.249.39.9:3000/api/tasks').then(
          result => {
            console.log(result.data)
            this.todos = result.data
          },
          error => {
            console.error(error)
          }
        )
      },
      addNewTask() {
        axios.post('http://173.249.39.9:3000/api/task',
          { task_name: this.taskname }
        ).then((res) => {
          this.taskname = ''
          this.getTasks()
          console.log(res)
        }).catch((err) => {
          console.log(err)
        })
      },
      editTask(title, id) {
        this.id = id
        this.taskname = title
        this.isEdit = true
      },
      updateTask() {
        axios.put(`http://173.249.39.9:3000/api/task/${this.id}`,
          { task_name: this.taskname }
        ).then((res) => {
          this.taskname = ''
          this.isEdit = false
          this.getTasks()
          console.log(res)
        }).catch((err) => {
          console.log(err)
        })
      },
      deleteTask(id) {
        axios.delete(`http://173.249.39.9:3000/api/task/${id}`
        ).then((res) => {
          this.taskname = ''
          this.getTasks()
          console.log(res)
        }).catch((err) => {
          console.log(err)
        })
      }
    }
  }
</script>