<template>
    <div>
        <input
            v-model="inputValue"
            @input="validateRFC"
            placeholder="Enter RFC"
        />
        <p class="invalid" v-if="!isValid">RFC no válido</p>
    </div>
</template>

<script setup>
    import { ref, watch, defineProps } from 'vue';
    const props = defineProps({
        RFC: String
    });

    const inputValue = ref(props.RFC || '');
    const isValid = ref(true);

    function validateRFC() {
        const rfcPatternFisica = /^[A-ZÑ&]{3,4}\d{6}[A-Z\d]{3}$/i;
        const rfcPatternMoral = /^[A-ZÑ&]{3}\d{6}[A-Z\d]{3}$/i;
        const rfc = inputValue.value.trim().toUpperCase();

        if (rfcPatternFisica.test(rfc) || rfcPatternMoral.test(rfc)) {
            isValid.value = true;
        } 
        else {
            isValid.value = false;
        }
    }

    watch(() => props.RFC, (newValue) => {
        inputValue.value = newValue;
        validateRFC();
    });

    watch(inputValue, validateRFC);

</script>

<style scoped>
    .invalid {
        color: red;
    }
</style>