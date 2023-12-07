<template>
    <li>
        <p>
            {{product.name}}
        </p>
        <CurrencyPrice :price="product.price" />
        <button @click="$emit('@addToCart', product)">Add to cart</button>
    </li>
</template>

<script setup lang="ts">
import type Product from '../types/Product';
import type Currency from '../types/Currency';
import CurrencyPrice from '../components/CurrencyPrice.vue'

defineProps<{product: Product;}>()
defineEmits<{"@addToCart": [product: Product]}>()
</script>

<style scoped>
li {
  display: flex;
  align-items: center;
  gap: 8px;
}
</style>