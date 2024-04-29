<template>
  <div class="container">
    <div class="task">
      <!-- title -->
      <div class="title">
        <h1> To Do List</h1>
      </div>
      <!-- form -->
      <div class="form">
        <input
          type="text"
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="add new task"
        />
        <button class="btn -btn-success" @click="addTask()">+ Add</button>
      </div>
      <!-- task lists -->
      <div class="taskItems">
        <ul>
          <li v-for="(list, index) in tasks" :key="list.id">
          <!-- <button :class="itemNoted">- {{ list.title }}</button> -->
          <button >- {{ list.title }}</button>
          <button class="remove" @click="removeTask(index)">Remove</button>
          </li>
        </ul>
      </div>
      <!-- buttons -->
      <div class="clearBtns">
        <button @click="clearCompleted()">Clear completed</button>
        <button @click="clearAll()">Clear all</button>
      </div>
      <!-- pending task -->
      <div class="pendingTasks">
        <span>Pending Tasks: {{ inCompleted }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      newTask: '',
      tasks: [
        {id: 1, title: "Learn Vue JS", completed: true},
        {id: 2, title: "Watch netflix", completed: true},
        {id: 3, title: "Go shopping", completed: false},
        {id: 4, title: "Learn guitar", completed: false},
        {id: 5, title: "Send email", completed: false},
      ],
    }
  },
  computed: {
   inCompleted() {
    return this.tasks.filter(this.isProgress).length;
   },
  //  itemNoted(){
  //   let classes = ['toggle'];
  //   if(this.list.completed){
  //     classes.push('toggle-completed')
  //   }
  //   return classes
  //  }
  },
  methods: {
    addTask(){
    if(this.newTask){
      this.tasks.push({
        title: this.newTask, 
        completed: false
      });
      this.newTask = ""
    }
    },
  clearAll() {
    this.tasks = []
  },
  isProgress(task){
    return !this.isCompleted(task)
  },
  clearCompleted(){
   this.tasks = this.tasks.filter(this.isProgress)
  },
   isCompleted(task){
    return task.completed;
   },
   removeTask(index){
    this.tasks.splice(index, 1)
   },
}
}
</script>
<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font: 15px/1.4 "Poppins", sans-serif;
  background: #4ec5c1;
  color: #333;
}

#app {
  padding: 60px 0;
}

.container {
  max-width: 480px;
  margin: 0 auto;
  padding: 0 15px;
}

input[type="text"] {
  width: 100%;
  height: 50px;
  font: 15px/1.4 "Poppins", sans-serif;
  padding: 15px;
  background: #f3f3f3;
  color: #333;
  border: 1px solid transparent;
  border-radius: 10px;
  transition: border 0.3s linear;
}

input[type="text"]:focus {
  outline: none;
  border: 1px solid #4ec5c1;
}

button {
  cursor: pointer;
  font: 15px/1.4 "Poppins", sans-serif;
  color: #555;
  transition: all 0.3s linear;
}

button:focus {
  outline: none;
}

h1 {
  font-size: 22px;
}

ul {
  list-style: none;
  margin: 0;
  padding: 0;
}

/* 
task 
----
*/
.task {
  background: #fff;
  border-radius: 25px;
  padding: 30px;
  box-shadow: 0px 0px 40px 0px rgba(0,0,0,0.1);
}

.title {
  text-align: center;
  margin: 0 0 20px;
}

.form {
  position: relative;
  margin: 0 0 30px;
}

.form button {
  background: none;
  border: none;
  color: #4ec5c1;
  font-size: 18px;
  position: absolute;
  top: 50%;
  right: 20px;
  transform: translateY(-50%);
}

.clearBtns {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
}

.clearBtns button {
  width: 100%;
  background: #4ec5c1;
  color: #fff;
  border: none;
  border-radius: 10px;
  padding: 10px;
  margin: 0 5px;
}

.clearBtns button:hover {
  background: #333;
}

.pendingTasks {
  padding: 0 6px;
}

/* 
task items
----------
*/
.taskItems {
  padding: 0 10px;
}

.taskItems li {
  display: flex;
  justify-content: space-between;
  margin: 0 0 20px;
}

.taskItems button {
  background: none;
  border: none;
}

.taskItems .remove {
  background: none;
  border: none;
  color: red;
}

.taskItems button:hover {
  color: #4ec5c1;
}

.taskItems .toggle i {
  margin: 0 10px 0 0;
  font-size: 14px;
}

.taskItems .toggle.toggle-completed {
  text-decoration:line-through;
}
</style>
