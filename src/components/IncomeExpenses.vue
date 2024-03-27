<template>
	<div class="inc-exp-container p-5 flex justify-between my-5 mx-0">
		<div
			class="flex-1 text-center border-r border-y-0 border-l-0 border-solid border-r-[#dedede]"
		>
			<h4>Income</h4>
			<p
				id="money-plus"
				class="text-[20px] my-[5px] mx-0 tracking-[1px] text-[#2ecc71] plus"
			>
				+{{ income }}$
			</p>
		</div>
		<div class="flex-1 text-center">
			<h4>Expense</h4>
			<p
				id="money-minus"
				class="text-[20px] my-[5px] mx-0 tracking-[1px] text-[#c0392b] minus"
			>
				{{ expenses }}$
			</p>
		</div>
	</div>
</template>

<script setup>
import { defineProps } from "vue";

const { income, expenses } = defineProps(["income", "expenses"]);
</script>

<style scoped>
.inc-exp-container {
	box-shadow: var(--box-shadow);
}
</style>
