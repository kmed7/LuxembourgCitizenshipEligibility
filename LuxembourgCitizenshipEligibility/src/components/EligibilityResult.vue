<template>
  <div class="result" :class="{ eligible: isEligible }">
    <h2>{{ isEligible ? '✓ Eligible!' : '✗ Not Eligible' }}</h2>
  
  </div>
    <p v-if="article" class="article">Via: {{ article }}</p>
    <p>{{ result }}</p>
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
.result.eligible { 
  background-image: url("/27107.jpg");
      background-repeat: no-repeat;
    background-position: center;
    background-size: cover;
    }
.article { font-weight: bold; color: #1e88e5; }
</style>