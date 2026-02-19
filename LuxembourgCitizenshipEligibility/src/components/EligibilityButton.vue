<template>
  <button @click="$emit('check')">Check Eligibility</button>
</template>

<script setup>
defineEmits(['check'])
</script>

<style scoped>
button { 
  background: #51ADDA; 
  color: white; 
  padding: 10px 20px; 
  border: none; 
  border-radius: 4px; 
  cursor: pointer; 
  margin-top: 15px;
  margin-left: 10px;
}
</style>