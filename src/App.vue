<script setup>
import AddTransaction from "./components/AddTransaction.vue";
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import Transactions from "./components/Transactions.vue";

import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// get total balance
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// get income
const income = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount > 0).reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// get expense
const expense = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount < 0).reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// handle add transaction
const handleAddTransaction = (transaction) => {
  transactions.value.push({
    id: generateUniqueId(),
    ...transaction
  });

  saveToLocalStorage();

  toast.success('Transaction added successfully.');
}

// generate unique id
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
}

// delete transaction
const handleDeleteTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);

  saveToLocalStorage();

  toast.success('Transaction deleted successfully.');
}

// save transactions to the local storage
const saveToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
}
</script>

<template>
  <div class="container">
    <Header title="Expense Tracker" />
    <Balance :total="+total" />
    <IncomeExpense :income="income" :expense="expense" />
    <Transactions :transactions="transactions" @delete-transaction="handleDeleteTransaction"  />
    <AddTransaction @add-transaction="handleAddTransaction" />
  </div>
</template>

<style>
.container {
  max-width: 400px;
  width: 100%;
  margin: 20px auto;
}
</style>
