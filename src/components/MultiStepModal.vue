<template>
  <div class="hello">
    <header class="custom-header">
        <p class="modal-card-title">Send</p>
        <div class="progress-line"><div class="line" /></div>
        <ul class="steps-nav">
          <li v-for="(step, index) in steps" :key="`step-${index}`"
            :class="['circle', currentStepIndex === index ? 'active' : '']">
            <div class="steps-index">{{index+1}}</div>
            <div class="steps-title">{{step.title}}</div>
          </li>
        </ul>
    </header>
    <div class="modal-card">
      <form class="modal-card-body" ref="form">
        <component :is="steps[currentStepIndex].component" :multiStepData="multiStepData" @input="handleChange"></component>
      </form>
    </div>

    <div class="custom-footer is-right">
      <button class="button is-info" :disabled="isDisabled" v-on:click="nextStep()">Next</button>
    </div>
  </div>
</template>

<script>
import ModalForm from './ModalForm.vue'
import Submit from './Submit.vue'
export default {
  name: 'MultiStep',
  components: {
    ModalForm,
    Submit
  },
  props: ['steps'],
    data() {
      return {
        currentStepIndex: 0,
        multiStepData: {
          amount: '',
          address: '',
        },
        isDisabled: true,
      }
    },
  methods: {
    nextStep() {
      this.$root.$validator.validate('step'+(this.currentStepIndex)+'.*').then(valid => {
        if (valid){
          this.currentStepIndex += 1;
        }
      }); 
    },
    handleChange(data) {
      this.$root.$validator.validate('step'+(this.currentStepIndex)+'.*').then(valid => {
          if (valid){
            this.isDisabled = false;
          }
      }); 
      this.multiStepData = data
    }
  },
}
</script>

<style scope>
.modal-card-title {
  padding: 20px 30px 50px;
  font-weight: 600;
}

.steps-nav {
  display: flex;
  justify-content: center;
}

.steps-index {
  vertical-align: middle;
  height: 100%;
  margin-top: 2px;
  margin-left: 1px;
}

.steps-title {
  margin-top: 10px;
  margin-left: -10px
}

.custom-header {
  display: flex;
  flex-direction: column;
  background-color: white;
  flex-shrink: 0;
  justify-content: flex-start;
  padding: 20px;
  position: relative;
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
}

.custom-footer {
  display: flex;
  flex-direction: column;
  background-color: white;
  flex-shrink: 0;
  justify-content: flex-start;
  padding: 20px;
  position: relative;
  border-bottom-left-radius: 6px;
  border-bottom-right-radius: 6px;
}

.circle {
  margin: 0 5em;
  font-size: 12px;
  width: 20px;
  height: 20px;
  text-align: center;
  line-height: 1em;
  border-radius: 1em;
  background: white;
  border: 2px solid #d1d1d1;  
  display: inline-block;
  position: relative;
  z-index: 10;
}

.progress-line {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: -10px;
}

.line {
  position: relative;
  width: 10em;
  height: .1em;
  background: #d1d1d1;
  z-index: 1;
}


.circle:first-child::before {
  display: none;
}

.active {
  background: #f4e1ed;
  border: 2px solid #f82ca6;
  color: #f82ca6;
}

.button {
  width: 100px;
  margin: 0 20px;
  background-color: #3148f1;
}

.modal-card-body {
  height: 400px;
  padding: 0 20px;
  display: flex;
  align-items: center;
}

</style>


