<template>
  <div>
    <h1>{{ message }}</h1>
    <button @click="reverseMessage">ReverseMessage</button>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const message = ref('Hello, Vue!')

function reverseMessage() {
  message.value = message.value.split('').reverse().join('')
}
</script>
