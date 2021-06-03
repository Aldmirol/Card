<template>
    <div :class="classes" class="warning-light"></div>
</template>

<script>
export default {
    props: {
        classList: Array,
        isError: Boolean,
        isCorrect: Boolean,
    },
    data() {
        return {
            error: 'is-error',
            correct: 'is-correct'
        }
    },
    watch: {
        
    },
    computed: {
        classes() {
            let classes = [...this.classList, this.isError ? this.error : '', this.isCorrect ? this.correct : ''];

            return classes;
        }
    },
    
}
</script>

<style scoped>
    .warning-light {
        height: 8px;
        width: 8px;
        position: absolute;
        border-radius: 50%;
        background-color: #1c0f92;
    }
    .pan-position {
        top: 40%;
        left: 90%;
    }

    .cvc-position {
        top: 28%;
        left: 50%;
    }

    .date-position {
        top: 28%;
        left: 57%;
    }

    .is-error {
        background-color: #c21717;
    }

    .is-correct {
        background-color: #58be29;
    }
</style>