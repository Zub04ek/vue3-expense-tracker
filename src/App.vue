<template>
	<Header />
	<div class="my-[30px] mx-auto w-[400px]">
		<Balance :total="+total" />
		<IncomeExpenses :income="+income" :expenses="+expenses" />
		<TransactionList @transactionDeleted="handleTransactionDeleted" :transactions="transactions" />
		<AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
	</div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { ref, computed, onMounted } from "vue";
import { useToast } from "vue-toastification";

const transactions = ref([]);
const toast = useToast();

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
})

// Get total
const total = computed(() =>
	transactions.value.reduce((acc, trans) => acc + trans.amount, 0),
);

// Get income
const income = computed(() =>
	transactions.value
		.filter(trans => trans.amount > 0)
		.reduce((acc, trans) => acc + trans.amount, 0)
		.toFixed(2),
);

// Get expenses
const expenses = computed(() =>
	transactions.value
		.filter(trans => trans.amount < 0)
		.reduce((acc, trans) => acc + trans.amount, 0)
		.toFixed(2),
);

// Add transaction
const handleTransactionSubmitted = transactionData => {
	transactions.value.push({
		id: generateUniqueId(),
		text: transactionData.text,
		amount: transactionData.amount,
	});
  savedTransactionsToLocalStorage()
	toast.success("Transaction added");
};

const generateUniqueId = () => Math.floor(Math.random() * 1000000);

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((trans) => trans.id !== id);
  savedTransactionsToLocalStorage()
  toast.success('Transaction deleted')
}

// Save to local storage
const savedTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<style lang="scss" scoped></style>
