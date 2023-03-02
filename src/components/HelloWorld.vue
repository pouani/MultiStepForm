<template>
  <Stepper :steps="steps" :validations="validation">
    <template #step1>
      <!-- Contenu de l'étape 1 -->
      <form action="">
        <input type="text" placeholder="name">
        <input type="text" placeholder="email">
      </form>
    </template>
    <template #step2>
      <!-- Contenu de l'étape 2 -->
    </template>
    <template #step3>
      <!-- Contenu de l'étape 3 -->
    </template>
  </Stepper>
</template>

<script>
import Stepper from './Stepper.vue'

export default {
  components: {
    Stepper,
  },
  data() {
    return {
      steps: [
        { title: 'Step 1', slotName: 'step1' },
        { title: 'Step 2', slotName: 'step2' },
        { title: 'Step 3', slotName: 'step3' },
        { title: 'Step 4', slotName: 'step4' },
      ],
      validation : true
    }
  },
}
</script>