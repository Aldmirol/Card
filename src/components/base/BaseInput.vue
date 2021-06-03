<template>
    <div :class="wrapperClasses">
        <label :for="id" :class="labelClasses">{{ label }}</label>
        <input :type="type"
            :id="id"
            :name="id"
            :placeholder="placeholder"
            :class="inputClasses"
            v-maska="maskPattern"
            v-model="currentValue"
            @input="action(currentValue)"
        >
    </div>
</template>

<script>
import { maska } from 'maska';

export default {
    props: {
        wrapperClasses: Array,
        id: String,
        type: String,
        placeholder: String,
        inputClasses: Array,
        label: String,
        labelClasses: Array,
        maskPattern: String,
        value: String
    },
    directives: {
        maska
    },
    data() {
        return {
            currentValue: null
        }
    },
    methods: {
        action(value) {
            this.$emit('input', value);
        }
    },
    watch: {
        value() {
            this.currentValue = this.value;
        }
    }
}
</script>

<style scoped>
    .card-number {
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: flex-end;
    }

    .pan-label {
        font-weight: 500;
    }

    .pan-input {
        height: 40%;
        font-size: 1.3rem;
    }

    .expire-wrapper {
        width: 25%;
    }

    .expire-input {
        width: 90%;
        font-size: 1.3rem;
        text-align: center;
    }

    .expire-input::placeholder {
        text-align: center;
        color: #000000;
    }

    .cvc-input {
        width: 45%;
        text-align: center;
        font-size: 1.3rem;
    }

    .hidden-borders {
        border: none;
        outline: none;
        border-bottom: 2px solid #2C363D;
    }

    .is-error {
        border-top: 1px solid red;
    }
</style>