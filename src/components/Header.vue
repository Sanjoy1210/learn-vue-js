<template>
    <header class="header">
        <h1>{{ title }}</h1>
    </header>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    title: {
        type: String,
        require: true,
    }
})
</script>

<style scoped>
.header {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

h1 {
    font-size: 18px;
    font-weight: 600;
}
</style>