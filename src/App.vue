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
</script>

<template>
<ul>
  <li v-for="item in items" :key="item.text">
    {{ item.text }} : {{ item.done }}
  </li>
</ul>
</template>

<style scoped></style>
