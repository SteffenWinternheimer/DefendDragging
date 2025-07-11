<template>
  <div class="variant" :class="{ greyed: isGreyedOut, flash: isFlashing }">
    {{ name }}
  </div>
</template>

<script setup>
import { watch, ref } from 'vue'

const props = defineProps({
  name: String,
  targetHit: Boolean,
})

const isGreyedOut = ref(false)
const isFlashing = ref(false)

watch(
  () => props.targetHit,
  (newVal) => {
    if (newVal) {
      isGreyedOut.value = true

      isFlashing.value = true
      setTimeout(() => {
        isFlashing.value = false
      }, 300)
    }
  },
)
</script>

<style scoped>
div {
  width: 150px;
  height: 100px;
  border: 2px dashed #888;
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  background: linear-gradient(to right, #00963e, #64dd17);
  box-shadow: 0 0 12px rgba(0, 255, 100, 0.6);
  color: white;
  font-weight: bold;

  display: flex;
  justify-content: center;
  align-items: center;

  transition:
    background-color 0.3s,
    color 0.3s;
}

.greyed {
  background: #888;
  color: #eee;
  box-shadow: none;
}

.flash {
  animation: flashHighlight 0.3s ease forwards;
}

@keyframes flashHighlight {
  0% {
    box-shadow: 0 0 15px 8px #ffd700;
    background-color: #ffd700;
    color: #888;
  }
  100% {
    box-shadow: none;
    background-color: inherit;
    color: inherit;
  }
}
</style>
