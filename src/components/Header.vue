<template>
    <header >
        <h1>{{ title }}</h1>
        <Button v-show="homePage" @btn-click="$emit('toggle-addTask')" :text="showAddTask ? 'Close' : 'Add Task'" :color="showAddTask ? 'red' : 'green'" />
         <!-- <Button text="Update Task" color="blue" />
          <Button text="Delete Task" color="red" /> -->
    </header>
</template>

<script>
import Button from './Button.vue'

    export default {
        name: 'Header',
        //props can be passed as array also "props: ['title']".
        props: {
            title: String,
            showAddTask: Boolean
        },
        components: {
            Button,
        },
        //computed property used for reactivity
        computed: {
            //is the path is on the home page then return true else return false 
            homePage() {
                if(this.$route.path === '/') {
                    return true
                } else {
                    return false
                }
            }
        }
    }

</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>
