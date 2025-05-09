<script setup>
import { ref, computed } from 'vue'

const listTask = ref([])
const newTask = ref('')
const filter = ref('all')

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

const removeTask = (id) => {
  listTask.value = listTask.value.filter(task => task.id !== id)
}

const filteredList = computed(() => {
  if (filter.value === 'all') {
    return listTask.value
  } else if (filter.value === 'completed') {
    return listTask.value.filter(task => task.completed)
  } else {
    return listTask.value.filter(task => !task.completed)
  }
})

</script>

<template>
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">Add</button>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="active">Active</option>
    </select>
    <ul>
      <li v-for="task in filteredList" :key="task.id">
        <input type="checkbox" v-model="task.completed">
        {{ task.title }}
        <button @click="removeTask(task.id)">Remove</button>
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
