<!-- html output -->
<template>
  <div class="container">
    <Header title="Task Tracker"></Header>
    <!-- passing in dynamic array so if changes we want it to get sent down to tasks data -->
    <Tasks :tasks="tasks" />
  </div>
</template>

<!-- javascript logic-->
<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
  },
  data() {
    return {
      tasks: []
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

