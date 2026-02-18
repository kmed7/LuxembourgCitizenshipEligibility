<template>
  <div class="container">
    <h1>Luxembourg Citizenship Eligibility Checker</h1>
    <p>Check if you qualify for Luxembourg dual citizenship through ancestry.</p>

    <AncestorForm 
      v-for="(ancestor, index) in ancestors" 
      :key="index" 
      :ancestor="ancestor"
      :generation="index"
      :can-remove="index > 0"
      @remove="removeGeneration(index)"
    />

    <AddGenerationButton @add="addGeneration" />

    <EligibilityButton @check="checkEligibility" />

    <EligibilityResult 
      v-if="result" 
      :result="result" 
      :is-eligible="isEligible" 
      :article="article"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AncestorForm from './components/AncestorForm.vue'
import AddGenerationButton from './components/AddGenerationButton.vue'
import EligibilityButton from './components/EligibilityButton.vue'
import EligibilityResult from './components/EligibilityResult.vue'

const ancestors = ref([
  { label: 'Gen 0 - Luxembourg Ancestor', gender: '', bornAfter1969: false },
])

const result = ref('')
const isEligible = ref(false)
const article = ref('')

function addGeneration() {
  const gen = ancestors.value.length
  ancestors.value.push({ 
    label: `Gen ${gen}`, 
    gender: '', 
    bornAfter1969: false 
  })
}

function removeGeneration(index) {
  ancestors.value.splice(index, 1)
  // Relabel remaining generations
  ancestors.value.forEach((ancestor, i) => {
    ancestor.label = i === 0 ? 'Gen 0 - Luxembourg Ancestor' : `Gen ${i}`
  })
}

function checkEligibility() {
  if (ancestors.value.length < 2) {
    result.value = 'Please add at least one descendant generation.'
    isEligible.value = false
    article.value = ''
    return
  }

  const lastIndex = ancestors.value.length - 1
  let article7BreaksAt = -1

  for (let i = 0; i < ancestors.value.length - 1; i++) {
    const parent = ancestors.value[i]
    const child = ancestors.value[i + 1]
    
    if (parent.gender === 'female' && !child.bornAfter1969) {
      article7BreaksAt = i + 1
      break
    }
  }

  if (article7BreaksAt === -1) {
    result.value = 'Your lineage shows an unbroken chain of citizenship eligibility!'
    isEligible.value = true
    article.value = 'Article 7'
    return
  }

  const generationsFromBreak = lastIndex - article7BreaksAt
  const eligibleAncestor = ancestors.value[article7BreaksAt - 1]

  if (generationsFromBreak <= 1) {
    result.value = `Article 7 passes citizenship to ${eligibleAncestor.label}. You can then use Article 23 to claim citizenship through them as your ${generationsFromBreak === 0 ? 'parent' : 'grandparent'}.`
    isEligible.value = true
    article.value = 'Article 7 + Article 23'
    return
  }

  result.value = `Citizenship chain broken at ${ancestors.value[article7BreaksAt].label}. Article 7 only reaches ${eligibleAncestor.label}, which is more than 2 generations from you. Article 23 cannot bridge this gap.`
  isEligible.value = false
  article.value = ''
}
</script>

<style>
.container { max-width: 600px; margin: 0 auto; padding: 20px; }
</style>