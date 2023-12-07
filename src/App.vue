<template>
    <header>
        <h1>{{ name }}</h1>
        <input v-model="name" type="text" />
        <button @click="placeOrder">Place Order</button>
    </header>

    <main>
        <div>
            <label for="currency">Currency</label>
            <select
                name="currency"
                id="currency"
                v-model="selectedCurrency"
            >
                <option
                    v-for="currency in currencies"
                    :key="currency.icon"
                    :value="currency.icon"
                >
                    {{ currency.name }}
                </option>
            </select>
        </div>
        <ul>
            <Order
                v-for="product in products"
                :key="product.name"
                :product="product"
                :addToCart="addToCart"
                @@add-to-cart="(product: Product) => addToCart(product)"
            />
        </ul>
    </main>
</template>

<script setup lang="ts">
import { ref, reactive, provide } from "vue";

import Product from "./types/Product";
import Currency from "./types/Currency";

import Order from "./components/Order.vue";

//Consts
const products = reactive<Array<Product>>([
    { name: "Hamburger 🍔", price: 5 },
    { name: "Cheeseburger 🧀", price: 6 },
    { name: "Impossible Burger 🥕", price: 7 },
    { name: "Fries 🍟", price: 2 },
]);

const currencies = reactive<Array<Currency>>([
    {
        icon: "$",
        name: "Dollars ($)",
        convert: 1,
    },
    {
        icon: "€",
        name: "Euros ($)",
        convert: 0.92,
    },
    {
        icon: "£",
        name: "Pound (£)",
        convert: 0.79,
    },
]);

//Refs
const selectedCurrency = ref<string>("$")
const name = ref<string>("The Snazzy Burger");
const cart = reactive<Array<Product | null>>([]);

function placeOrder(): void {
    window.alert(`Your order ${name.value} has been placed!`);
}

function addToCart(product: Product): void {
    cart.push(product);
    window.alert(cart.map((p) => p.name));
}

provide("selectedCurrency", selectedCurrency)
provide("currencies", currencies)
</script>

<style scoped>
header,
ul {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

main {
  margin-top: 25px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
}
</style>
