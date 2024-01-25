<script setup>
import { inject } from "vue";
import Card from "./Card.vue";

defineProps({
    items: Array
});

const {addToCart} = inject('cart');

const addToFavorite = async (item) => {
    try {
        const url = "https://6ffbb2d6fa3c52ee.mokky.dev/favorite";

        if (!item.isFavorite) {
            const obj = {
                parentId: item.id
            };

            const response = await fetch(url, {
                method: 'POST',
                body: JSON.stringify(obj),
                headers: {
                    "Content-type": "application/json; charset=UTF-8"	
                }
            });

            const data = await response.json();

            item.isFavorite = true;
            item.favoriteId = data.id;
        }
        else {
            const data = await fetch(`${url}/${item.favoriteId}`, {
                method: 'DELETE'
            });

            item.isFavorite = false;
            item.favoriteId = null;
        }
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}
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
            :onClickFavorite="() => addToFavorite(item)"/>
    </div>
</template>

<style scoped lang="sass">
.list
    display: grid
    grid-template-columns: repeat(4, minmax(0, 1fr))
    gap: 1.25rem
</style>