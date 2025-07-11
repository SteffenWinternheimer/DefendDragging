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

      // Flash-Effekt starten
      isFlashing.value = true
      setTimeout(() => {
        isFlashing.value = false
      }, 300) // Dauer des Flashs in ms
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
  background: #09871b;

  display: flex;
  justify-content: center; /* horizontal zentrieren */
  align-items: center; /* vertikal zentrieren */
}

.greyed {
  background: #888;
}
.flash {
  animation: flashHighlight 0.3s;
}

@keyframes flashHighlight {
  0% {
    box-shadow: 0 0 10px 5px #ffd700;
    background-color: #ffd700;
    color: black;
  }
  100% {
    box-shadow: none;
  }
}
</style>
