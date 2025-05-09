<script setup>
import { ref, computed } from 'vue'
import { TrashIcon, PencilSquareIcon } from '@heroicons/vue/24/solid'

const listTask = ref([])
const newTask = ref('')
const filter = ref('all')

const addTask = () => {
  if (newTask.value === '') return
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
  if (filter.value === 'all') return listTask.value
  else if (filter.value === 'completed') return listTask.value.filter(task => task.completed)
  else return listTask.value.filter(task => !task.completed)
})
</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-green-50 to-teal-100 flex justify-center items-start p-6">
    <div class="w-full max-w-lg bg-white shadow-xl rounded-2xl p-6 space-y-6 font-mono">
      <h1 class="text-2xl font-bold text-center text-emerald-700 flex items-center justify-center gap-2">
        <PencilSquareIcon class="w-6 h-6 text-emerald-600" />
        Task Tracker
      </h1>

      <div class="flex items-center gap-2">
        <input
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="Type a new task"
          class="flex-1 px-4 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-emerald-400"
        />
        <button
          @click="addTask"
          class="bg-emerald-600 text-white px-4 py-2 rounded-lg hover:bg-emerald-700 transition"
        >
          Add
        </button>
      </div>

      <select
        v-model="filter"
        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-emerald-400"
      >
        <option value="all">All Tasks</option>
        <option value="completed">Completed</option>
        <option value="active">Active</option>
      </select>

      <ul class="space-y-3 h-75 overflow-y-auto pr-1">
        <li
          v-for="task in filteredList"
          :key="task.id"
          class="flex justify-between items-center bg-gray-50 border border-gray-200 rounded-lg px-4 py-2 hover:bg-gray-100 transition"
        >
          <div class="flex items-center gap-3">
            <input
              type="checkbox"
              v-model="task.completed"
              class="w-4 h-4 text-emerald-600"
            />
            <span
              :class="task.completed ? 'line-through text-gray-400' : 'text-gray-700'"
              class="text-sm"
            >
              {{ task.title }}
            </span>
          </div>
          <button @click="removeTask(task.id)" class="text-red-500 hover:text-red-700">
            <TrashIcon class="w-5 h-5" />
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>
