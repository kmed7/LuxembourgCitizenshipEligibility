<template>
  <button class="add-btn" @click="$emit('add')">+ Add Generation</button>
</template>

<script setup>
defineEmits(['add'])
</script>

<style scoped>
.add-btn { 
  background: #EA141D; 
  color: white; 
  padding: 10px 20px; 
  border: none; 
  border-radius: 4px; 
  cursor: pointer; 
  margin-top: 15px;
}
</style>