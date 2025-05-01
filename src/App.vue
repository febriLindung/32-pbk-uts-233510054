<script setup>
import { ref, computed } from 'vue'

const items = ref([])
const newItem = ref('')
const filter = ref('all')

const addItem = () => {
  items.value.push({
    id: items.value.length + 1,
    text: newItem.value,
    done: false
  })
  newItem.value = ''
}

const removeItem = (item) => {
  items.value = items.value.filter(i => i.id !== item.id)
}

const toggleDone = (item) => {
  item.done = !item.done
}

const filteredItems = computed(() => {
  if (filter.value === 'all') {
    return items.value
  } else if (filter.value === 'done') {
    return items.value.filter(item => item.done)
  } else {
    return items.value.filter(item => !item.done)
  }
})

</script>

<template>
  <div class="h-screen w-screen flex flex-col bg-gradient-to-br from-blue-100 to-indigo-100 font-sans">
    <!-- Header -->
    <header class="bg-gradient-to-r from-indigo-600 to-blue-600 py-5 px-6 shadow-md">
      <h1 class="text-2xl md:text-3xl font-extrabold text-white text-center tracking-wide">Task Manager</h1>
    </header>

    <!-- Main -->
    <main class="flex-1 p-5 overflow-hidden flex flex-col">
      <div class="max-w-3xl mx-auto w-full flex flex-col h-full">

        <!-- Input + Filter -->
        <div class="bg-white rounded-xl shadow p-5 mb-4">
          <div class="flex flex-col sm:flex-row gap-4 items-center">
            <input 
              v-model="newItem"
              @keyup.enter="addItem"
              placeholder="Tambah tugas baru..."
              class="flex-1 border border-gray-300 rounded-lg p-3 shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-400 transition focus:scale-105"
            />

            <button 
              @click="addItem"
              class="bg-gradient-to-r from-indigo-500 to-blue-600 text-white py-3 px-6 rounded-lg shadow-md hover:shadow-lg transition-all hover:scale-105 focus:outline-none focus:ring-2 focus:ring-indigo-400">
              Tambah
            </button>

            <select v-model="filter"
              class="border border-gray-300 rounded-lg py-2 px-3 shadow-sm focus:outline-none focus:ring-2 focus:ring-indigo-400 transition text-sm">
              <option value="all">Semua</option>
              <option value="done">Selesai</option>
              <option value="not done">Belum Selesai</option>
            </select>
          </div>
        </div>

        <!-- List -->
        <div class="flex-1 bg-white rounded-xl shadow p-5 overflow-hidden flex flex-col">
          <h2 class="text-xl font-bold text-gray-800 mb-3">Daftar Tugas</h2>

          <!-- List Scrollable -->
          <div class="flex-1 overflow-y-auto pr-2 space-y-3">
            <div v-if="filteredItems.length === 0"
              class="flex items-center justify-center h-full text-gray-500 italic">
              Tidak ada tugas.
            </div>

            <ul class="space-y-3">
              <li v-for="item in filteredItems" :key="item.id"
                class="flex items-center justify-between bg-white border border-gray-100 rounded-lg p-3 shadow-sm hover:shadow-md transition-transform hover:translate-x-2">
                
                <div class="flex items-center gap-3 truncate">
                  <input 
                    type="checkbox" 
                    :checked="item.done" 
                    @change="toggleDone(item)"
                    class="w-5 h-5 text-indigo-500 focus:ring-indigo-400 rounded"
                  />
                  <span :class="item.done ? 'line-through text-gray-400' : 'text-gray-800'">
                    {{ item.text }}
                  </span>
                </div>

                <button @click="removeItem(item)"
                  class="text-sm px-3 py-1 rounded-lg bg-red-100 text-red-700 hover:bg-red-200">
                  Hapus
                </button>
              </li>
            </ul>

          </div>
        </div>

      </div>
    </main>
  </div>
</template>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap');

* {
  font-family: 'Inter', sans-serif;
}

/* List Animation */
li {
  animation: fadeSlide 0.5s ease forwards;
}

@keyframes fadeSlide {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Custom Scrollbar */
::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: #f3f4f6;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: #a5b4fc;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: #818cf8;
}

/* Small input animation */
input[type="checkbox"]:focus {
  outline: none;
  box-shadow: 0 0 0 2px #818cf8;
}
</style>
