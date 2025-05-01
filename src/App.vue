<script setup>
import { ref } from 'vue'

const items = ref([])

const newItem = ref('')

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


</script>

<template>

  <input type="text" v-model="newItem" @keyup.enter="addItem">
  <button @click="addItem">Add</button>

  <ul>
    <li v-for="item in items" :key="item.text">
      {{ item.text }}
      <button @click="removeItem(item)">Remove</button>
    </li>
  </ul>
</template>

<style scoped></style>
