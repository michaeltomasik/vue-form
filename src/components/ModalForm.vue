<template>
  <div class="detail-form">
    <form action="">
        <b-field
            label="Amount" 
            class="custom-label">
            <div>
                <b-input
                    data-vv-scope="step0"
                    type="number"
                    ref="amount"
                    v-model="amount"
                    placeholder="Type amount of ATOM"
                    @input="updateDate()"
                    v-validate="'required|numeric'"
                    required>
                </b-input>

                <div class="currency">ATOM</div>
            </div>
        </b-field>

        <b-field
            label="Address"
            class="custom-label">
            <b-input
                data-vv-scope="step0"
                type="text"
                ref="address"
                v-model="address"
                placeholder="Type your address"
                @input="updateDate()"
                v-validate="'required'"
                required >
            </b-input>
        </b-field>
    </form>
  </div>
</template>

<script>
import { required, between } from 'vuelidate/lib/validators'

export default {
  name: 'Form',
  props: ['multiStepData'],
    data() {
        return {
            amount: '',
            address: '',
        }
    },
    methods: {
        updateDate(e) {
            this.$emit('input', {
                amount: this.amount,
                address: this.address
            })
        },
    },
}
</script>

<style scope>
.currency {
    position: relative;
    float: right;
    margin-top: -30px;
    margin-right: 10px;
    font-weight: 600;
}

.custom-label {
    margin: 30px 20px;
}

.custom-label label {
    float: left;
    font-size: 12px;
    margin-bottom: 0px !important;
}

.custom-label input {
    border: solid 2px #3e3e3e;
}

.is-danger {
    text-align: start;
}

.detail-form {
    width: 100%;
}

</style>


