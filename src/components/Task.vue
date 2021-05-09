<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder': '', 'task']">
    <h3>{{task.text}}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{task.day}}</p>
  </div>
</template>

<script>
export default {
name: "Task",
  props: {
  task: Object,
  },
}
</script>

<style scoped>
.task{
  background-color: gray;
  padding: 5px 12px;
  border-radius: 5px;
  margin: 5px;
  width: 100%;
}
.task.reminder{
  border-left: 5px solid green;
  width: calc(100% - 5px);
}
h3{
  display: flex;
  justify-content: space-between;
}
.fas{
  color: red;
  cursor: pointer;
}
</style>