<script setup>
import { ref } from 'vue'

const listTask = ref([])
const newTask = ref('')

const addTask = () => {
  if (newTask.value === '') {
    console.log('Please enter a task')
    return 
  }
  listTask.value.push({
    id: listTask.value.length + 1,
    title: newTask.value,
    completed: false
  })
  newTask.value = ''
}

</script>

<template>
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">Add</button>
    <ul>
      <li v-for="task in listTask" :key="task.id">
        <input type="checkbox" v-model="task.completed">
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
