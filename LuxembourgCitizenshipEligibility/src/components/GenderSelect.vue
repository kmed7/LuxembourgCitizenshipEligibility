<template>
  <label>
    Gender:
    <select :value="modelValue" @change="$emit('update:modelValue', $event.target.value)">
      <option value="">Select</option>
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>
  </label>
</template>

<script setup>
defineProps({ modelValue: String })
defineEmits(['update:modelValue'])
</script>

<style scoped>
label { display: block; margin: 10px 0; }
</style>