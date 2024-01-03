<template>
    <p>your balance</p>
    <h1>${{ total }}</h1>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    total: {
        type: Number,
        required: true,
    }
})
</script>

<style scoped>
p {
    font-size: 14px;
    text-transform: uppercase;
    padding-top: 16px;
}

h1 {
    font-size: 28px;
    font-weight: 600;
}
</style>