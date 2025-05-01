<script setup>
import { ref } from 'vue'

const items = ref([
  {
    text: 'Makan',
    done: false
  },
  {
    text: 'Minum',
    done: false
  },
  {
    text: 'Main',
    done: false
  }
])

const newItem = ref('')

const addItem = () => {
  items.value.push({
    id : items.value.length + 1,
    text: newItem.value,
    done: false
  })
  newItem.value = ''
}
</script>

<template>

<input type="text" v-model="newItem" @keyup.enter="addItem">
<button @click="addItem">Add</button>

<ul>
  <li v-for="item in items" :key="item.text">
    {{ item.text }} : {{ item.done }}
  </li>
</ul>
</template>

<style scoped></style>
