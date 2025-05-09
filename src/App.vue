<script setup>
import { ref } from 'vue'

const listTask = ref([
  {
    id: 1,
    title: 'Task 1',
    completed: false
  },
  {
    id: 2,
    title: 'Task 2',
    completed: false
  },
  {
    id: 3,
    title: 'Task 3',
    completed: false
  },
  {
    id: 4,
    title: 'Task 4',
    completed: false
  },
  {
    id: 5,
    title: 'Task 5',
    completed: false
  },
])
</script>

<template>
  <div>
    <ul>
      <li v-for="task in listTask" :key="task.id">
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<style scoped></style>
