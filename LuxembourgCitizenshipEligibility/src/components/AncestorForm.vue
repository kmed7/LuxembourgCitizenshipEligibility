<template>
  <div class="ancestor">
    <div class="header">
      <h3>{{ ancestor.label }}</h3>
      <button v-if="canRemove" class="remove-btn" @click="$emit('remove')">✕</button>
    </div>
    
    <GenderSelect v-model="ancestor.gender" />
<div class="checkbox-group">
  <!-- Only Gen 0 has this checkbox -->
  <CheckboxInput 
    v-if="generation === 0"
    v-model="ancestor.bornBetween1815And1943" 
    label="Born between 1815-1943" 
  />

  <!-- Placeholder for other generations -->
  <span v-else class="checkbox-placeholder"></span>

  <!-- This one stays for all generations -->
  <CheckboxInput 
    v-model="ancestor.bornAfter1969" 
    label="Born after January 1, 1969" 
  />
</div>
  </div>
</template>

<script setup>
import GenderSelect from './GenderSelect.vue'
import CheckboxInput from './CheckboxInput.vue'

defineProps({
  ancestor: { type: Object, required: true },
  generation: { type: Number, required: true },
  canRemove: { type: Boolean, default: false }
})

defineEmits(['remove'])
</script>

<style scoped>
.ancestor {
  border: 1px solid #ccc; 
  padding: 15px;
  margin: 10px 0;
  border-radius: 8px;
  
  }

.header { display: flex; justify-content: space-between; align-items: center; }
.header h3 { margin: 0; }
.remove-btn {
  background: #e53935;
  color: white;
  border: none;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  cursor: pointer;
  font-size: 14px;
  line-height: 1;
}
.checkbox-placeholder {
  display: block;
  height: 24px; /* match actual checkbox height */
}
</style>