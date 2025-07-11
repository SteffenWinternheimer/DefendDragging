<script setup>
const props = defineProps({
  name: String,
})
</script>

<template>
  <div
    class="mechanism"
    draggable="true"
    @dragstart="$event.dataTransfer.setData('mechanism', name)"
  >
    {{ name }}
  </div>
</template>

<style scoped>
.mechanism {
  padding: 0.5rem 1rem;
  background: linear-gradient(to right, #1d5a89, #2a88cf);
  box-shadow: 0 0 12px rgba(0, 68, 255, 0.6);
  border: 1px solid #aaa;
  border-radius: 5px;
  font-weight: bold;
  cursor: grab;
  color: #d6d6d6;
}
</style>
