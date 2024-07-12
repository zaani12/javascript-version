<template>
  <v-container>
    <v-card class="pa-4 wizard-card">
      <v-stepper v-model="currentStep">
        <v-stepper-header>
          <v-stepper-item
            v-for="(step, index) in steps"
            :key="index"
            :complete="currentStep > index + 1"
            :value="index + 1"
            editable
          >
            <template v-slot:default="{ step }">
              <div class="step-info">
                <div class="step-circle" :class="{ 'active-step': currentStep === index + 1, 'completed-step': index + 1 <= currentStep }"></div>
                <div class="step-number">{{ ('0' + (index + 1)).slice(-2) }}</div>
                <div class="step-text" :class="{ 'active-step-title': currentStep === index + 1, 'completed-step-title': index + 1 <= currentStep }">
                  {{ step.title }}
                  <small class="d-block">{{ step.subtitle }}</small>
                </div>
              </div>
            </template>
          </v-stepper-item>
          
          <v-divider
            v-if="index < steps.length - 1"
            class="step-divider"
            v-for="(step, index) in steps"
            :key="'divider-' + index"
          />
        </v-stepper-header>

        <v-stepper-items>
          <v-stepper-content
            v-for="(step, index) in steps"
            :key="index"
            :value="index + 1"
            v-show="currentStep === index + 1"
          >
            <component :is="step.component"></component>
            <v-btn
              v-if="index > 0"
              @click="prevStep"
              class="mr-4"
            >
              Previous
            </v-btn>
            <v-btn
              v-if="index < steps.length - 1"
              @click="nextStep"
            >
              Next
            </v-btn>
            <v-btn
              v-if="index === steps.length - 1"
              @click="submitForm"
            >
              Submit
            </v-btn>
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>
    </v-card>
  </v-container>
</template>

<script>
import Step1 from '@/views/Wizard/Step1.vue';
import Step2 from '@/views/Wizard/Step2.vue';
import Step3 from '@/views/Wizard/Step3.vue';

export default {
  data() {
    return {
      currentStep: 1,
      steps: [
        {
          title: 'Account Details',
          subtitle: 'Setup Account Details',
          component: Step1
        },
        {
          title: 'Personal Info',
          subtitle: 'Add personal info',
          component: Step2
        },
        {
          title: 'Social Links',
          subtitle: 'Add social links',
          component: Step3
        }
      ]
    };
  },
  methods: {
    goToStep(step) {
      this.currentStep = step;
    },
    nextStep() {
      if (this.currentStep < this.steps.length) this.currentStep++;
    },
    prevStep() {
      if (this.currentStep > 1) this.currentStep--;
    },
    submitForm() {
      alert('Form submitted!');
      console.log(this.$refs);
    }
  }
};
</script>

<style scoped>
/* .wizard-card {
  border: 1px solid #ddd;
  border-radius: 0.5rem;
}
.step-info {
  display: flex;
  align-items: center;
}
.step-circle {
  display: inline-block;
  width: 1.5rem;
  height: 1.5rem;
  border: 2px solid #ddd;
  border-radius: 50%;
  background-color: #fff;
  transition: all 0.3s ease;
}
.active-step {
  border-color: #6f42c1;
  background-color: #e9ecef;
}
.completed-step {
  background-color: #6f42c1;
  border-color: #6f42c1;
}
.step-number {
  font-size: 1.25rem;
  color: #563d7c;
  margin-right: 0.5rem;
}
.step-text {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}
.step-divider {
  height: 2px;
  background-color: #ddd;
  margin: 0 1rem;
} */
</style>
