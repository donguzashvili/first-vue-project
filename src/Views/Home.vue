<template>
    <addTask
        v-show="showAddTask"
        @add-task="addTask" />
  <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask" :tasks="task" />
</template>

<script>
import Tasks from "../components/Tasks"
import addTask from "../addTask"
export default {
  name: "Home",
  props: {
    showAddTask: Boolean,
  },
  components:{
    Tasks,
    addTask,
  },
  data() {
      return{
        task: [],
      }
  },
  methods: {
    async addTask(task){
      const res = await fetch('api/task', {
        method: 'POST',
        headers: {
          'Content-type' : 'application/json',

        },
        body: JSON.stringify(task)
      })
      const data = await res.json()
      this.task = [...this.task, data]
    },
    async deleteTask(id){
      if(confirm('are you sure?')){
        const res = await fetch(`api/task/${id}`, {
          method:'DELETE'
        })
        res.status === 200 ? this.task = this.task.filter((task) => task.id !== id) : alert('Error deleting task')

      }
    },
    async toggleReminder(id){
      const taskToToggle = await this.fetchTask(id)
      const updateTask = {...taskToToggle, reminder: !taskToToggle.reminder}

      const res = await fetch(`api/task/${id}`, {
        method: 'PUT',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(updateTask),
      })

      const data = await res.json();

      this.task = this.task.map((task) =>
          task.id === id ? {...task, reminder: data.reminder}
              : task )
    },
    async fetchTasks(){
      const res = await fetch('api/task')
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`api/task/${id}`)
      const data = await res.json()
      return data
    },
  },
  async created(){
    this.task = await this.fetchTasks()
  }
}
</script>

<style scoped>

</style>