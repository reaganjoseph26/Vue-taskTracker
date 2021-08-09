<!-- html output -->
<template>
  <div class="container">
    <Header @toggle-addTask="toggleAddTask" title="Task Tracker" :showAddTask= 'showAddTask'/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <!-- passing in dynamic array so if changes we want it to get sent down to tasks data -->
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<!-- javascript logic-->
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
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm('Are you sure?')) {
         //return everything back except the task with the id being passed through
      this.tasks = this.tasks.filter((task) => task.id !==id)
      }
    },
    toggleReminder(id) {
      //map through enitre array and return an array of updated task
      //for each task if task.id is equal to the task being passed in return an array of object where the initial task properties and then change the reminder to the opposite of the current task reminder else do nothing
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder } : task)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Dentist Appointment',
        day: 'August 2nd at 9:30am',
        reminder: true,
      },
       {
        id: 2,
        text: 'Date',
        day: 'September 4th at 7:30pm',
        reminder: true,
      },
       {
        id: 3,
        text: 'Eye Exam',
        day: 'September 22nd at 11:30am',
        reminder: false,
      }
    ]
  }
}
</script>

<!-- styling-->
<style>
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

