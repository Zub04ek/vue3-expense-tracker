<template>
	<h3>Add new transaction</h3>
	<form id="form" @submit.prevent="onSubmit">
		<div class="form-control">
			<label for="text" class="inline-block my-[10px] mx-0">Text</label>
			<input
				type="text"
				class="block w-full p-[10px] text-[16px] border border-solid border-[#dedede] rounded-sm"
				v-model="text"
				id="text"
				placeholder="Enter text..."
			/>
		</div>
		<div class="form-control">
			<label for="amount" class="inline-block my-[10px] mx-0">
				Amount
				<br />
				(negative - expense, positive - income)
			</label>
			<input
				type="number"
				class="block w-full p-[10px] text-[16px] border border-solid border-[#dedede] rounded-sm"
				v-model="amount"
				id="amount"
				placeholder="Enter amount..."
			/>
		</div>
		<button
			class="block w-full p-[10px] mx-0 mt-[10px] mb-[30px] border-0 bg-[#9c88ff] text-white text-[16px] cursor-pointer focus:outline-0"
		>
			Add transaction
		</button>
	</form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const text = ref("");
const amount = ref("");
const emit = defineEmits(["transactionSubmitted"]);
const toast = useToast();

const onSubmit = () => {
	if (!text.value || !amount.value) {
		toast.error("Both fields must be filled");
		return;
	}

	const transactionData = {
		text: text.value,
		amount: parseFloat(amount.value),
	};

	emit("transactionSubmitted", transactionData);

	text.value = "";
	amount.value = "";
};
</script>

<style scoped>
button {
	box-shadow: var(--box-shadow);
}
</style>