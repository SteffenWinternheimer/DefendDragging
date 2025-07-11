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
  <div class="attack-box">
    <p class="label">🚨 Cyberattack Incoming</p>
    <p class="attack-name">{{ currentAttack }}</p>
  </div>
</template>

<style scoped>
.attack-box {
  padding: 1.5rem;
  border-radius: 12px;
  background: linear-gradient(145deg, #ff1e56, #ff6a00);
  box-shadow: 0 0 15px rgba(255, 0, 0, 0.5);
  text-align: center;
  animation: pulse 2s infinite;
  min-width: 300px;
  max-width: 400px;
  color: white;
  transition: all 0.3s ease;
}

.label {
  font-size: 1rem;
  font-weight: 600;
  opacity: 0.8;
  margin-bottom: 0.5rem;
}

.attack-name {
  font-size: 1.3rem;
  font-weight: bold;
  text-shadow: 0 0 6px #000;
  transition: all 0.5s ease-in-out;
}

@keyframes pulse {
  0% {
    box-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
  }
  50% {
    box-shadow: 0 0 20px rgba(255, 0, 0, 0.8);
  }
  100% {
    box-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
  }
}
</style>
