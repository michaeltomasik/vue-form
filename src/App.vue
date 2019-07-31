<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <ModalHolder :steps="steps" />
  </div>
</template>

<script>
import ModalHolder from './components/ModalHolder.vue'

export default {
  name: 'app',
  components: {
    ModalHolder,
  },
  data() {
    return {
      steps: [{
        title: 'Details',
        component: 'ModalForm'
      },
      {
        title: 'Submit',
        component: 'Submit',
      }],
      currentStep: 0,
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
