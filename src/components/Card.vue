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
                v-model="panInput.value"
            />
            <WarningLight
                :classList="panLight.classList"
                :isCorrect="panLight.isCorrect"
                :isError="panLight.isError"
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
                    />
                    <span class="expire-separator">/</span>
                    <BaseInput
                        :id="expireYearInput.id"
                        :wrapperClasses="expireYearInput.wrapperClasses"
                        :inputClasses="expireYearInput.inputClasses"
                        :placeholder="expireYearInput.placeholder"
                        :maskPattern="'##'"
                        v-model="expireYearInput.value"
                    />
                </div>
                <WarningLight
                :classList="dateLight.classList"
                :isCorrect="isCorrectDate"
                :isError="dateLight.isError"
            />
            </div>
        <div class="bottom-right-wrapper">
            <div class="cvc-title">
                <span>CVV/CVC</span>
                <span class="question-sign" title="Help must be there">&quest;</span>
                <font-awesome-icon icon="eraser" class="eraser" @click="removeValue"/>
            </div>
            <BaseInput
                :id="cvcInput.id"
                :inputClasses="cvcInput.inputClasses"
                :maskPattern="'###'"
                v-model="cvcInput.value"
            />
            <WarningLight
                :classList="cvcLight.classList"
                :isCorrect="cvcLight.isCorrect"
                :isError="cvcLight.isError"
            />
        </div>
        </div>
        
    </div>
</template>

<script>
import BaseInput from './base/BaseInput.vue';
import WarningLight from './base/WarningLight.vue';

export default {
    components: {
        BaseInput,
        WarningLight,
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
            panLight: {
                classList: ['pan-position'],
                isError: false,
                isCorrect: false
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
            dateLight: {
                classList: ['date-position'],
                isCorrect: false,
                isError: true,
            },
            cvcInput: {
                id: 'cvc-input',
                inputClasses: ['cvc-input', 'hidden-borders'],
            },
            cvcLight: {
                classList: ['cvc-position'],
                isCorrect: false,
                isError: false,
            },
        }
    },
    methods: {
        removeValue() {
            this.panInput.value = '';
            this.expireMonthInput.value = '';
            this.expireYearInput.value = '';
            this.cvcInput.value = '';
        }
    },
    computed: {
        isCorrectDate() {
            const monthValue = +this.expireMonthInput.value;
            const today = new Date;
            const currentYear = today.getFullYear();
            const yearValue = +this.expireYearInput.value;
            if ((monthValue > 0 && monthValue <= 12 && (yearValue === currentYear - 2000))) {
                return true;
            } else {
                return false;
            }
        }
    },
    watch: {
        isCorrectDate: function(value) {
            if (value) {
                this.dateLight.isCorrect = true;
            }
        },
        'cvcInput.value': function(value) {
            if (value === '000') {
                this.cvcLight.isError = true;
            } else if (value.length === 3) {
                this.cvcLight.isError = false;
                this.cvcLight.isCorrect = true;
            } else {
                this.cvcLight.isError = false;
                this.cvcLight.isCorrect = false;
            }
        },
        'panInput.value': function(value) {
            let str = value.replace(/\s/g, '')

            if (str.length > 0 && str.length < 16) {
                this.panLight.isCorrect = false;
                this.panLight.isError = true;
            } else if (str.length === 16) {
                this.panLight.isError = false;
                this.panLight.isCorrect = true;
            } else if (str.length === 0) {
                this.panLight.isError = false;
                this.panLight.isCorrect = false;
            }
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
        position: relative;
    }

    .bottom-wrapper {
        height: 40%;
        width: 90%;
        display: flex;
    }

    .bottom-left-wrapper,
    .bottom-right-wrapper {
        width: 50%;
        position: relative;
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

    .eraser {
        position: absolute;
        top: -150px;
        left: 215px;
        cursor: pointer;
        color: #575353;
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