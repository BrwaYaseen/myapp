<template>
  <div class="max-w-md mx-auto p-6 bg-white shadow-md rounded-lg">
    <h1 class="text-2xl font-bold mb-4 text-gray-800">{{ title }}</h1>
    <input 
      v-model="newTodo" 
      @keyup.enter="addTodo" 
      placeholder="Add a new todo"
      class="w-full px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 mb-4"
    >
    <ul class="space-y-2">
      <li v-for="(todo, index) in todos" :key="index" class="flex items-center justify-between bg-gray-100 p-2 rounded-md">
        <span class="text-gray-800">{{ todo.text }}</span>
        <button @click="removeTodo(index)" class="px-2 py-1 bg-red-500 text-white rounded-md hover:bg-red-600 focus:outline-none focus:ring-2 focus:ring-red-500">
          Remove
        </button>
      </li>
    </ul>
    <p class="mt-4 text-gray-600">Total todos: {{ todoCount }}</p>
  </div>
</template>

<script>
import { ref, computed } from 'vue'

export default {
  name: 'App',
  setup() {
    const title = ref('My Todo App')
    const newTodo = ref('')
    const todos = ref([])

    const addTodo = () => {
      if (newTodo.value.trim()) {
        todos.value.push({ text: newTodo.value.trim() })
        newTodo.value = ''
      }
    }

    const removeTodo = (index) => {
      todos.value.splice(index, 1)
    }

    const todoCount = computed(() => todos.value.length)

    return {
      title,
      newTodo,
      todos,
      addTodo,
      removeTodo,
      todoCount
    }
  }
}
</script>