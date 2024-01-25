<script setup>

import { onMounted, ref, watch } from 'vue';
import CardList from '../components/CardList.vue';

const items = ref([]);
const favorites = ref([]);
const array = ref([]);

const getItems = async () => {
    try {
        items.value = await fetch('https://6ffbb2d6fa3c52ee.mokky.dev/items')
            .then(res => res.json());
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

const getFavoritesItems = async () => {
    try {
        favorites.value = await fetch('https://6ffbb2d6fa3c52ee.mokky.dev/favorite')
            .then(res => res.json());
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

const selectionFavoriteInItems = () => {
    try {
        for (let i in items.value) {
            for (let f in favorites.value) {
                if (items.value[i].id === favorites.value[f].parentId) {
                    array.value.push(items.value[i]);
                }
            }
        }
        console.log(items.value)
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

onMounted(async () => {
    await getItems();
    await getFavoritesItems();
});
watch(selectionFavoriteInItems, getItems);
</script>

<template>
    <div class="favorite">
        <h2 class="favorite__title">
            Мои закладки
        </h2>
        <card-list :items="array" />
    </div>
</template>

<style scoped lang="sass">
.favorite
    &__title
        margin-top: 42px
        margin-left: 116px
        color: #000
        font-size: 32px
        font-weight: 700
</style>