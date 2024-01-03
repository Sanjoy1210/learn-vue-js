<template>
    <div class="wrapper">
        <div>
            <span>income</span>
            <span class="plus">+${{ income }}</span>
        </div>
        <div>
            <span>expense</span>
            <span class="minus">${{ expense }}</span>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    income: {
        type: Number,
        required: true,
    },
    expense: {
        type: Number,
        required: true,
    },
});
</script>

<style scoped>
.wrapper {
    display: flex;
    justify-content: space-between;
    margin: 20px 0;
    padding: 20px;
    background-color: #fff;
}

.wrapper > div {
    flex: 1;
    text-align: center;
    text-transform: uppercase;
    display: flex;
    flex-direction: column;
}

.wrapper > div:first-of-type {
    border-right: 1px solid gainsboro;
}

.plus {
    color: rgb(6, 202, 6);
}
.minus {
    color: red;
}
</style>