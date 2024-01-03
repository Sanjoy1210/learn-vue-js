<template>
    <div>
        <p>Add new transaction</p>
        <form @submit.prevent="onSubmit">
            <div class="form-control">
                <label for="text">Text</label>
                <input 
                    type="text" 
                    name="text" 
                    id="text" 
                    placeholder="Enter text..."
                    v-model="text"
                />
            </div>
            <div class="form-control">
                <label for="amount">Amount <br />
                    (negative - expense, positive - income)
                </label>
                <input 
                    type="text" 
                    name="amount" 
                    id="amount" 
                    placeholder="Enter amount..."
                    v-model="amount"
                />
            </div>
            <button class="btn">Add transaction</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from "vue-toastification";

const toast = useToast();

const text = ref('');
const amount = ref('');

const emit = defineEmits(['add-transaction']);

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error("Both fields must be filled.");
        return;
    }
    const newTransaction = {
        text: text.value,
        amount: parseFloat(amount.value),
    };

    emit('add-transaction', newTransaction);

    // clear inputs
    text.value = '';
    amount.value = '';
}
</script>

<style scoped>

p {
    padding-top: 20px;
    border-bottom: 1px solid gainsboro;
    padding-bottom: 4px;
}

label {
    display: inline-block;
    margin: 10px 0;
}

input[type='text'], 
input[type='number']  {
    border: 1px solid #dedede;
    border-radius: 2px;
    font-size: 14px;
    padding: 10px;
    width: 100%;
}

.btn {
    cursor: pointer;
    background-color: #9c88ff;
    box-shadow: var(--box-shadow);
    color: #fff;
    border: 0;
    display: block;
    font-size: 16px;
    margin: 10px 0 30px;
    padding: 10px;
    width: 100%;
}

.btn:focus {
    outline: none;
}

</style>