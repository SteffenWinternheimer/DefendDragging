<template>
  <div>
    <h4>{{ name }}</h4>
  </div>
</template>

<script setup>
defineProps({
  name: String,
})
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
</style>
