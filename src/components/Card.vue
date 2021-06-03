<template>
    <div class="card">
        <div class="top-wrapper">
            <BaseInput
                :id="panInput.id"
                :label="panInput.label"
                :type="panInput.type"
                :wrapperClasses="panInput.wrapperClasses"
                :inputClasses="panInput.inputClasses"
                :labelClasses="panInput.labelClasses"
                :maskPattern="'#### #### #### ####'"
                :isError="false"
                v-model="panInput.value"
                
            />
        </div>
        <div class="bottom-wrapper">
            <div class="bottom-left-wrapper">
                <p class="expiration-title">Срок действия</p>
                <div class="left-wrapper-container">
                    <BaseInput
                        :id="expireMonthInput.id"
                        :wrapperClasses="expireMonthInput.wrapperClasses"
                        :inputClasses="expireMonthInput.inputClasses"
                        :placeholder="expireMonthInput.placeholder"
                        :maskPattern="'##'"
                        v-model="expireMonthInput.value"
                        :isError="false"
                    />
                    <span class="expire-separator">/</span>
                    <BaseInput
                        :id="expireYearInput.id"
                        :wrapperClasses="expireYearInput.wrapperClasses"
                        :inputClasses="expireYearInput.inputClasses"
                        :placeholder="expireYearInput.placeholder"
                        :maskPattern="'##'"
                        :isError="false"
                        v-model="expireYearInput.value"
                    />
                </div>
            
        </div>
        <div class="bottom-right-wrapper">
            <div class="cvc-title">
                <span>CVV/CVC</span>
                <span class="question-sign">&quest;</span>
            </div>
            <BaseInput
                :id="cvcInput.id"
                :inputClasses="cvcInput.inputClasses"
                :maskPattern="'###'"
                :isError="false"
                v-model="cvcInput.value"
            />
        </div>
        </div>
        
    </div>
</template>

<script>
import BaseInput from './base/BaseInput.vue'

export default {
    components: {
        BaseInput,
    },
    data() {
        return {
            panInput: {
                id: 'pan',
                label: 'Номер карты',
                type: 'text',
                wrapperClasses: ['card-number'],
                inputClasses: ['pan-input', 'hidden-borders'],
                labelClasses: ['pan-label'],
                value: null,
            },
            expireMonthInput: {
                id: 'expire-month',
                wrapperClasses: ['expire-wrapper'],
                inputClasses: ['hidden-borders', 'expire-input'],
                placeholder: 'ММ',
                value: null,
            },
            expireYearInput: {
                id: 'expire-year',
                wrapperClasses: ['expire-wrapper'],
                inputClasses: ['hidden-borders', 'expire-input'],
                placeholder: 'ГГ',
                value: null,
            },
            cvcInput: {
                id: 'cvc-input',
                inputClasses: ['cvc-input', 'hidden-borders'],
                value: null,
            }
        }
    },
    watch: {
        'panInput.value': function(value) {
            this.expireMonthInput.value = value;
            this.expireYearInput.value = value;
            this.cvcInput.value = value;
        }
    }
}
</script>

<style scoped>
    .card {
        width: 500px;
        height: 300px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        border-radius: 0.55rem;
        background-color: #ffffff;
        box-shadow: 0px 1px 12px 1px rgba(46, 46, 46, 0.86);
    }
    .top-wrapper {
        height: 30%;
        width: 90%;
    }

    .bottom-wrapper {
        height: 40%;
        width: 90%;
        display: flex;
    }

    .bottom-left-wrapper,
    .bottom-right-wrapper {
        width: 50%;
    }

    .expiration-title,
    .cvc-title {
        margin-top: 30px;
        font-weight: 500;
        font-size: 1rem;
    }

    .cvc-title {
        margin-bottom: 16px;
        display: flex;
        position: relative;
    }

    .question-sign {
        height: 17px;
        width: 17px;
        position: absolute;
        left: 35%;
        top: -20%;
        border: 0.1px solid #000000;
        border-radius: 50%;
        text-align: center;
        cursor: pointer;
    }

    .left-wrapper-container {
        width: 100%;
        display: flex;
    }

    .expire-separator {
        font-size: 1.1rem;
        font-weight: 900;
        margin: 0 4px 0 4px;
    }
</style>