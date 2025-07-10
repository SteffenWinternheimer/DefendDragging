<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const emits = defineEmits(['attackChanged'])

const attacks = [
  'Brute Force Attack',
  'Reverse Engineering',
  'Phishing Attack',
  'SQL Injection',
  'Cross-Site Scripting (XSS)',
  'Denial of Service',
]

const currentAttack = ref('')

function getRandomItem() {
  const randomIndex = Math.floor(Math.random() * attacks.length)
  currentAttack.value = attacks[randomIndex]
  emits('attackChanged', currentAttack.value)
}

let intervalId

onMounted(() => {
  getRandomItem()
  intervalId = setInterval(getRandomItem, 5000)
})

onBeforeUnmount(() => {
  clearInterval(intervalId)
})
</script>

<template>
  <div class="attack">
    <p><strong>Current Attack:</strong> {{ currentAttack }}</p>
  </div>
</template>

<style scoped>
.attack {
  background-color: #ff0000;
  padding: 1rem;
  border: 2px dashed #aaa;
  border-radius: 8px;
  text-align: center;
  min-width: 250px;
}
p {
  margin: 0;
  color: #d6d6d6;
  font-weight: bold;
}
</style>
