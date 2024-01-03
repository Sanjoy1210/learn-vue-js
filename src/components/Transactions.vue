<template>
    <p>History</p>
    <ul class="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount > 0 ? 'plus' : 'minus'">
            <span>
                {{ transaction.text }}
            </span>
            <span>
                ${{ transaction.amount }}
            </span>
            <button @click="onClick(transaction.id)">X</button>
        </li>
    </ul>
</template>

<script setup>
import { defineProps } from 'vue';

const emit = defineEmits(['delete-transaction']);

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    }
});

const onClick = (id) => {
    emit('delete-transaction', id);
}
</script>

<style scoped>
p {
    border-bottom: 1px solid gainsboro;
    padding-bottom: 4px;
}

.list {
    list-style-type: none;
    padding-top: 8px;
}

.list li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #fff;
    padding: 8px 6px;
    position: relative;
    margin-bottom: 8px;
}

.list li.minus {
    border-right: 3px solid red;
}

.list li.plus {
    border-right: 3px solid rgb(6, 202, 6);
}

.list li button {
    position: absolute;
    left: 0;
    background: red;
    padding: 4px 6px;
    color: #fff;
    border: none;
    font-size: 12px;
    opacity: 0;
    transform: translate(-100%, 0);
    transition: opacity 0.3s linear;
    cursor: pointer;
}

.list li:hover button {
    opacity: 1;
}
</style>