<!-- Take in a prop of task/array then loop through and output a single task for each one -->

<!-- loop through the tasks -->
<!-- v-for creates a list or loop through and ouput something -->
<template>
    <div>
        <div :key="task.id" v-for="task in tasks">
        <Task @toggle-reminder="$emit('toggle-reminder', task.id)" @delete-task="$emit('delete-task', task.id)" :task="task" />
    </div>
    </div>
</template>

<script>
import Task from './Task'

 export default {
     name: 'Tasks',
     props: {
         tasks: Array
     },
     components: {
         Task,
     },
     emits: ['delete-task', 'toggle-reminder'],
 }

</script>
