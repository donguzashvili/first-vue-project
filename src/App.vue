<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask" />
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header"
import Footer from "./components/Footer"


export default {
  name: 'App',
  components: {
    Header,
    Footer
  },
  data(){
    return{
      task: [],
      showAddTask: false
    }
  },
  methods: {
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
  },
}
</script>

<style>
#app{
  font-family: 'poppins',sans-serif;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn{
  background-color: black;
  color: white;
  padding: 8px 15px;
  margin: 0 5px;
}
.container{
  border: 1px solid black;
  padding: 20px 40px;
  border-radius: 8px;
}
</style>
