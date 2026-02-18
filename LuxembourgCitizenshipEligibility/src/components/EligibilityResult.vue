<template>
  <div class="result" :class="{ eligible: isEligible }">
    <h2>{{ isEligible ? '✓ Potentially Eligible!' : '✗ Not Eligible' }}</h2>
    <p v-if="article" class="article">Via: {{ article }}</p>
    <p>{{ result }}</p>
  </div>
</template>

<script setup>
defineProps({
  result: String,
  isEligible: Boolean,
  article: String
})
</script>

<style scoped>
.result { margin-top: 20px; padding: 15px; border-radius: 8px; background: #ffebee; }
.result.eligible { background: #e8f5e9; }
.article { font-weight: bold; color: #1e88e5; }
</style>