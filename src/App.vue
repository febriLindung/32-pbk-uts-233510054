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
  item.done == !item.done
  console.log(item.done)
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

  <input type="text" v-model="newItem" @keyup.enter="addItem">
  <button @click="addItem">Add</button>
  <select v-model="filter">
    <option value="all">All</option>
    <option value="done">Done</option>
    <option value="not done">Not Done</option>
  </select>

  <ul>
    <li v-for="item in filteredItems" :key="item.text">
      <input type="checkbox" v-model="item.done" @change="toggleDone(item)" :checked="item.done">
      {{ item.text }}
      <button @click="removeItem(item)">Remove</button>
    </li>
  </ul>
</template>

<style scoped></style>
