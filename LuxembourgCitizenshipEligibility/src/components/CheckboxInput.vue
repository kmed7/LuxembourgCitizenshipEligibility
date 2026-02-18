<template>
  <label>
    <input 
      type="checkbox" 
      :checked="modelValue" 
      @change="$emit('update:modelValue', $event.target.checked)" 
    />
    {{ label }}
  </label>
</template>

<script setup>
defineProps({
  modelValue: Boolean,
  label: String
})
defineEmits(['update:modelValue'])
</script>

<style scoped>
label { display: block; margin: 10px 0; }
</style>