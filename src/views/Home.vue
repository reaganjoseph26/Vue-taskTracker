<template>
<div>
    <AddTask v-show="showAddTask" @add-task="addTask" />
    <!-- passing in dynamic array so if changes we want it to get sent down to tasks data -->
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</div>
</template>

<script>
import Tasks from '../components/Tasks'
import AddTask from '../components/AddTask'
export default {
    name: 'Home',
    props: {
        showAddTask: Boolean,
    },
    components: {
        Tasks,
        AddTask
    },
    data() {
        return {
            tasks: [],
        }
    },
    methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method:'POST',
        //sending data so headers need to be set
        headers: {
          'Content-type': 'application/json',
          //body is the data that is being sent. It is being wrapped in json.stringify. The data we are sending is the task coming in. 
        },
        body: JSON.stringify(task),
      })

      const data = await res.json()

      this.tasks = [...this.tasks, data]
    },
    async deleteTask(id) {
      if(confirm('Are you sure?')) {

        const res  = await fetch(`api/tasks/${id}`, {
          method: 'DELETE'
        })
        //check status to make sure it is deleted off of the server
        res.status === 200 ? 
        (//return everything back except the task with the id being passed through
        this.tasks = this.tasks.filter((task) => task.id !==id)) : alert('Error deleting task')
      }
    },
    async toggleReminder(id) {
      //gets the actual taks we want to toggle from the fetchTasks method above
      const taskToToggle = await this.fetchTask(id)
      //the task that we get back, change the reminder to the opposite 
      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json'
        },
        body: JSON.stringify(updateTask)
      })

      const data = await res.json()
      //map through enitre array and return an array of updated task
      //for each task if task.id is equal to the task being passed in return an array of object where the initial task properties and then change the reminder to the opposite of the current task reminder else do nothing
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder } : task)
    },
    async fetchTasks() {
      const res = await fetch('api/tasks')

      const data = await res.json()

      return data
    },
    //fetching a single task
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`)

      const data = await res.json()

      return data
    }
  },
  //created lifecycle will return a promise from fetchTaks() so wait for it
  async created() {
    this.tasks = await this.fetchTasks()
  },
}
</script>
