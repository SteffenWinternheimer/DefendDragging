<script setup>
import { ref, watch, computed } from 'vue'

const props = defineProps({
  name: String,
  currentAttack: String,
})

const emits = defineEmits(['increment', 'incorrect'])
const droppedMechanism = ref(null)

const matchMap = {
  'Brute Force Attack': 'Authentication',
  'Reverse Engineering': 'Encryption',
  'Phishing Attack': 'Authorization',
  'SQL Injection': 'Web Application Firewall',
  'Cross-Site Scripting (XSS)': 'Web Application Firewall',
  'Denial of Service': 'Network Segmentation',
}

const targetMap = {
  'Brute Force Attack': 'User Accounts',
  'Reverse Engineering': 'Licensing Systems',
  'Phishing Attack': 'Identities',
  'SQL Injection': 'Data',
  'Cross-Site Scripting (XSS)': 'Web Session',
  'Denial of Service': 'Network Integrity',
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
    emits('incorrect', {
      dropped: droppedMechanism.value,
      expected,
      attack: props.currentAttack,
      target: targetMap[props.currentAttack],
    })
    playSound('Error')
  }
}

function playSound(soundType) {
  const file = soundType === 'Error' ? '/sounds/error.wav' : '/sounds/success.mp3'
  const audio = new Audio(file)
  audio.play()
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
  const expected = matchMap[props.currentAttack]
  if (!droppedMechanism.value || !expected) return 'neutral'
  return droppedMechanism.value === expected ? 'success' : 'error'
})
</script>

<template>
  <div class="socket" :class="socketColor" @dragover="allowDrop" @drop="handleDrop">
    <span>{{ droppedMechanism || name }}</span>
  </div>
</template>

<style scoped>
.socket {
  padding: 1.2rem;
  min-width: 250px;
  min-height: 60px;
  border-radius: 12px;
  text-align: center;
  font-weight: bold;
  font-size: 1.1rem;
  color: white;
  border: 2px dashed rgba(255, 255, 255, 0.2);
  background: linear-gradient(to right, #2c3e50, #4ca1af); /* neutral state */
  transition:
    background 0.4s ease,
    box-shadow 0.3s ease;
  box-shadow: 0 0 8px rgba(255, 255, 255, 0.1);
}

.socket.success {
  background: linear-gradient(to right, #00c853, #64dd17);
  box-shadow: 0 0 12px rgba(0, 255, 100, 0.6);
}

.socket.error {
  background: linear-gradient(to right, #d32f2f, #ff5252);
  box-shadow: 0 0 12px rgba(255, 50, 50, 0.6);
}
</style>
