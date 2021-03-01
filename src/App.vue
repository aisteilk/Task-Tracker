<template>
<div class="container">
  <Header @toggle-add-task="toggleAddTask" 
  title="Task Tracker" :showAddTask="showAddTask" />
  <div v-show="showAddTask">
  <AddTask @add-task="addTask"/>
  </div>
  <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  
</div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
  name: 'App',
  components: {
    Header, 
    Tasks,
    AddTask,
  },
  data(){
    return{
      tasks: [], 
      showAddTask: false,
    }
  }, 
  methods: {
     toggleAddTask(){
       this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id){
      if(confirm('Are You sure? ')){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }    
    },
    // map through an array, manipulate the array and return an array with updated tasks
    //for each task if task.id is equal to id that is passed in we return an array of Objects 
    // where we have the initial task property and we want to change a reminder to the opposite
    //of the current task.reminder, else if it doesnt match the id, we want just return the task object
    toggleReminder(id){
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder} : task)
    },
  },
  // one of life-cycle methods
  created(){

    this.tasks = [
      {
        id: 1, 
        text: 'Doctors Appointment',
        day: 'March 1st at 16:30', 
        reminder: true,
      },
      {
        id: 2,
        text: 'Meeting at School', 
        day: 'March 3rd at 13:30',
        reminder: true,
      },
      {
        id: 3, 
        text: 'Food Shopping',
        day: 'March 3rd at 11:00',
        reminder: false,
      },  
    ]
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0; 
}

body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px; 
  margin: 30px auto; 
  overflow: auto;
  min-height: 300px; 
  border: 1px solid steelblue; 
  padding: 30px; 
  border-radius: 5px; 
}
.btn {
  display: inline-block; 
  background: #000; 
  color: #fff;
  border: none; 
  padding: 10px 20px; 
  margin: 5px; 
  border-radius: 5px; 
  cursor: pointer; 
  text-decoration: none; 
  font-size: 15px; 
  font-family: inherit; 
}
.btn:focus {
  outline: none; 
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block; 
  width: 100%;
}
</style>
