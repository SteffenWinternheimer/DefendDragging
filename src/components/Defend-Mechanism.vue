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
  background-color: #1d5a89;
  border: 1px solid #aaa;
  border-radius: 5px;
  cursor: grab;
  color: #d6d6d6;
}
</style>
