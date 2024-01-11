<script setup>
import Card from "./Card.vue";

defineProps({
    items: Array
})
</script>

<template>
    <div class="list">
        <Card 
            style="justify-self: center;"
            v-for="item in items"
            :key="item.id"
            :title="item.title" 
            :imageUrl="item.imageUrl"
            :isFavorite="false"
            :isAdded="false" 
            :price="item.price"
        />
    </div>
</template>

<style scoped lang="sass">
.list
    display: grid
    grid-template-columns: repeat(4, minmax(0, 1fr))
    gap: 1.25rem
</style>