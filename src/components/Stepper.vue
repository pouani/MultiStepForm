<template>
    <div>
      <div class="step-header">
        <h2>{{ steps[currentStepIndex].title }}</h2>
      </div>
      <div class="step-container">
        <div class="steppers">
            <div v-for="(step, index) in steps" :key="step.title" :class="{ active: currentStepIndex === index, completed: index < currentStepIndex }">
                <div class="step-content">
                    <small class="step-title">{{ step.title }}</small>
                    <div class="step-number">{{ index + 1 }}</div>
                </div>
            </div>
        </div>
        <div class="step-content">
            <slot :name="steps[currentStepIndex].slotName"></slot>
        </div>
      </div>
      
      <div class="step-buttons">
        <button @click="prevStep" :disabled="currentStepIndex === 0">Previous</button>
        <button @click="nextStep" :disabled="currentStepIndex === steps.length - 1">Next</button>
      </div>
    </div>
  </template>
  
  <script>
  import { ref } from 'vue'
  
  export default {
    props: {
      steps: {
        type: Array,
        required: true,
      },
      validations: {
        type: Boolean,
        default: false,
        required: false,
      },
    },
    setup(props) {
      const currentStepIndex = ref(0)
  
      const prevStep = () => {
        if (currentStepIndex.value > 0) {
            currentStepIndex.value--
        }
      }
  
      const nextStep = () => {
        if(props.validations){
            if (currentStepIndex.value < props.steps.length - 1) {
            currentStepIndex.value++
            }
        }
      }
  
      return {
        currentStepIndex,
        prevStep,
        nextStep,
      }
    },
  }
  </script>

  <style scoped>
    .steppers {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 1rem;
}

.steppers .step-number {
  display: inline-block;
  width: 2rem;
  height: 2rem;
  line-height: 2rem;
  text-align: center;
  border-radius: 50%;
  background-color: #ddd;
  color: #fff;
}

.steppers .step-content {
  display: flex;
  align-items: center;
  gap: .6rem;
}

.steppers .active .step-number {
  background-color: blue;
}

.step-container {
  display: flex;
}

.steppers .step-title {
  margin-bottom: 0.5rem;
  font-weight: bold;
}

.steppers .active .step-number {
  background-color: blue;
}

.steppers .step-title {
    margin-bottom: 0 !important;
  font-weight: 500;
}

.steppers .completed .step-number {
  background-color: blue;
}
</style>