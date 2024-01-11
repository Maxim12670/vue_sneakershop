<script setup>
import Card from "./Card.vue";
</script>

<template>
    <div class="list">
        <Card 
            title="Мужские кроссовки Nike Air" 
            imageUrl="./public/sneakers/sneakers-1.jpg"
            :isFavorite="false"
            :isAdded="false" 
            :price="1250"
        />
    </div>
</template>

<style scoped lang="sass">
.list
    display: grid
    grid-template-columns: repeat(4, minmax(0, 1fr))
    gap: 1.25rem
</style>