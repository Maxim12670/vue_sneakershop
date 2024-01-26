<script setup>
import { onMounted, ref, watchEffect } from 'vue';
import CardList from '../components/CardList.vue';
import InfoBlockFavorite from '../components/InfoBlockFavorite.vue';

const favorites = ref([]);

const getFavoritesItems = async () => {
    try {
        favorites.value = await fetch('https://6ffbb2d6fa3c52ee.mokky.dev/favorite')
            .then(res => res.json());
        console.log('dove')
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

onMounted(async () => {
    await getFavoritesItems();
});

watchEffect(async()=>{
    await getFavoritesItems()
})
</script>

<template>
    <div class="favorite">
        <info-block-favorite v-if="favorites.length === 0"/>
        <div v-else>
            <h2 class="favorite__title">
                Мои закладки
            </h2>
            <card-list :items="favorites" />
        </div>
        
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