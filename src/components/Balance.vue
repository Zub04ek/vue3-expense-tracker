<template>
	<h4>Your Balance</h4>
	<h1 id="balance">${{ total }}</h1>
</template>

<script setup>
import { defineProps } from 'vue';

const {total} = defineProps(['total'])
</script>

<style lang="scss" scoped></style>
