<script setup>
import { inject } from 'vue';
import CartItem from './CartItem.vue';

const { cart, addToCart } = inject('cart');
</script>

<template>
    <CartItem v-for="item in cart"
    :key="item.id"
    :title="item.title"
    :imageUrl="item.imageUrl"
    :price="item.price"
    :onClickAdd = "() => addToCart(item)"
    />
</template>