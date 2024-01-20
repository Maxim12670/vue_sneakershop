<script setup>
import { inject } from "vue";
import Card from "./Card.vue";

defineProps({
    items: Array
})

const {addToCart} = inject('cart');
</script>

<template>
    <div class="list">
        <Card 
            style="justify-self: center;" 
            v-for="item in items" 
            :key="item.id" 
            :id="item.id" 
            :title="item.title"
            :imageUrl="item.imageUrl" 
            :price="item.price" 
            :isFavorite="item.isFavorite"
            :isAdded="item.isAdded"
            :onClickAdd="() => addToCart(item)"
            :onClickFavorite="() => emit('addToFavorite', item)"/>
    </div>
</template>

<style scoped lang="sass">
.list
    display: grid
    grid-template-columns: repeat(4, minmax(0, 1fr))
    gap: 1.25rem
</style>