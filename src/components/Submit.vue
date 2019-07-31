<template>
  <section class="submit">
    <div class="green-notification">
      <p>Send <b>{{multiStepData.amount}}</b> Atoms</p>
      <p class="send-to">To {{multiStepData.address}} </p>
    </div>
    <div class="slider">
      <VueSlider
        dotSize="20"
        v-model="value"
        :adsorb="true"
        :interval="0.01"
        :min=0
        :max=0.5
        :marks="marks" />
    </div>
    <div class="total-details">
      <div class="row">
        <div>Subtotal</div>
        <div>{{parseFloat(multiStepData.amount).toFixed(3)}} Atoms</div>
      </div>
      <div class="row">
        <div>Network Fee</div>
        <div>{{parseFloat(value).toFixed(3)}} Atoms</div>
      </div>
      <hr/>
      <div class="row">
        <div>Total</div>
        <div>{{total}} Atoms</div>
      </div>
    </div>
  </section>
</template>

<script>
import VueSlider from 'vue-slider-component'
import 'vue-slider-component/theme/antd.css'

export default {
    components: {
      VueSlider
    },
    props: ['multiStepData'],
    data() {
      return {
        value: 0.000,
        marks: [0, 0.1, 0.25, 0.4, 0.5]
      }
    },
    computed: {
      total() {
        return parseFloat(this.value + parseFloat(this.multiStepData.amount)).toFixed(3);
      }
    }
}
</script>

<style scope>
.submit {
  margin: 0 20px;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.send-to {
  font-size: 12px;
}

.total-details {
  font-weight: 600;
  font-size: 12px;
}

.green-notification {
  border: 2px solid #39a430;
  background-color: #e5efe5;
  text-align: left;
  padding: 10px;
  margin-top: 30px;
}

.slider {
  margin: 40px 0;
}

.row {
  display: flex;
  justify-content: space-between;
}

.vue-slider-process {
  display: none;
}

.vue-slider-mark {
  width: 0px !important;
}

.vue-slider-mark-step {
  border-radius: 0%;
  top: -3px !important;
  height: 10px;
  border: 1px solid #e8e8e8;
  box-shadow: none;
}

.vue-slider:hover .vue-slider-mark-step-active {
  box-shadow: none;
}

</style>