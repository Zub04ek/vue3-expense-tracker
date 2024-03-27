<template>
	<h3>History</h3>
	<ul id="list" class="p-0 list-none mb-10">
		<li
			v-for="transaction in transactions"
			:key="transaction.id"
			:class="transaction.amount > 0 ? 'plus' : 'minus'"
			class="bg-white text-[#333] flex justify-between relative p-[10px] my-[10px] mx-0"
		>
			{{ transaction.text }}
			<span>{{ transaction.amount }}$</span>
			<button
				@click="deleteTransaction(transaction.id)"
				class="absolute left-0 opacity-0 py-[2px] px-[5px] mx-0 mt-[10px] mb-[30px] border-0 bg-[#e74c3c] text-white text-[20px] leading-5 cursor-pointer focus:outline-0 transition-opacity duration-300 ease-in-out"
			>
				x
			</button>
		</li>
	</ul>
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["transactionDeleted"]);

const { transactions } = defineProps(["transactions"]);
const deleteTransaction = id => {
	emit("transactionDeleted", id);
};
</script>

<style scoped>
button {
	transform: translate(-100%, -50%);
}
li {
	box-shadow: var(--box-shadow);
}
li:hover button {
	opacity: 1;
}
.plus {
	border-right: 5px solid #2ecc71;
}
.minus {
	border-right: 5px solid #c0392b;
}
</style>
