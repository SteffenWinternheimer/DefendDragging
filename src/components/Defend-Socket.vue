<script setup>
import { ref, watch, computed } from 'vue'

const props = defineProps({
  name: String,
  currentAttack: String,
})

const emits = defineEmits(['increment'])
const droppedMechanism = ref(null)

const matchMap = {
  'Brute Force Attack': 'Authentication',
  'Reverse Engineering': 'Encryption',
  'Phishing Attack': 'Authorization',
  'SQL Injection': 'Web Application Firewall',
  'Cross-Site Scripting (XSS)': 'Web Application Firewall',
  'Denial of Service': 'Network Segmentation',
}

function handleDrop(event) {
  const data = event.dataTransfer.getData('mechanism')
  if (data) {
    droppedMechanism.value = data
  }
  const expected = matchMap[props.currentAttack]
  if (droppedMechanism.value === expected) {
    emits('increment', 1)
    playSound('Success')
  } else {
    playSound('Error')
  }
}

function playSound(soundType) {
  if (soundType === 'Error') {
    const audio = new Audio('/sounds/error.wav')
    audio.play()
  } else {
    const audio = new Audio('/sounds/success.mp3')
    audio.play()
  }
}

function allowDrop(event) {
  event.preventDefault()
}

watch(
  () => props.currentAttack,
  () => {
    droppedMechanism.value = null
  },
)

const socketColor = computed(() => {
  if (!droppedMechanism.value) return 'gray'

  const expected = matchMap[props.currentAttack]
  if (!expected) return 'gray'

  return droppedMechanism.value === expected ? 'green' : 'red'
})
</script>

<template>
  <div
    class="socket"
    :style="{ backgroundColor: socketColor }"
    @dragover="allowDrop"
    @drop="handleDrop"
  >
    <span>{{ droppedMechanism || name }}</span>
  </div>
</template>

<style scoped>
.socket {
  padding: 1rem;
  min-width: 250px;
  min-height: 60px;
  border: 2px dashed #999;
  border-radius: 10px;
  text-align: center;
  transition: background-color 0.3s;
  color: #d6d6d6;
}
</style>
