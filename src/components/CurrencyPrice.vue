<script setup lang="ts">
import { computed, inject, type Ref } from "vue";
import type Currency from "../types/Currency";

const props = defineProps<{
    price: number;
}>();
const selectedCurrency: Ref<String> | undefined = inject("selectedCurrency");
const currencies: Array<Currency> | undefined = inject("currencies");

//0.86, 1.09
const price = computed(() => {
    const currency = currencies.find((c) => c.icon == selectedCurrency.value)

    switch (selectedCurrency.value) {
        case "$":
            return (props.price * currency.convert).toFixed(2);
        case "€":
            return (props.price * currency.convert).toFixed(2);
        case "£":
            return (props.price * currency.convert).toFixed(2);
    }
});
</script>

<template>
    <span>{{ `${price}${selectedCurrency}` }}</span>
</template>
