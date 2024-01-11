<script setup>
import { onMounted, reactive, ref, watch } from "vue";

import Header from "./components/Header.vue";
import Cardist from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";

const items = ref([]);

const filters = reactive({
    sortBy: 'title',
    searchQuery: ''
});

const getItems = async () => {
    try {
        const parametr = {
            sortBy: filters.sortBy
        }

        let url = `https://6ffbb2d6fa3c52ee.mokky.dev/items?sortBy=${parametr.sortBy}`

        if (filters.searchQuery) {
            parametr.title = `*${filters.searchQuery}*`;
            url = `https://6ffbb2d6fa3c52ee.mokky.dev/items?title=${parametr.title}&sortBy=${parametr.sortBy}`;
        }

        const data = await fetch(url)
            .then(res => res.json())
            .catch(error => console.log('Error:', error));

        items.value = data;
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

const onChangedSelect = (event) => {
    filters.sortBy = event.target.value;
}

const onChangedSearchInput = (event) => {
    filters.searchQuery = event.target.value;
}

onMounted(getItems);

watch(filters, getItems)
</script>

<template>
    <!-- <Drawer/> -->
    <div class="wrapper">
        <Header />
        <div class="content">
            <div style="display: flex; justify-content: space-between; align-items: center;">
                <h2 class="title">Все кроссовки</h2>
                <div>
                    <div style="display: flex;">
                        <select @change="onChangedSelect" class="select_list">
                            <option value="title">По названию</option>
                            <option value="price">По возрастанию цены</option>
                            <option value="-price">По убыванию цены</option>
                        </select>
                        <div style="position: relative;">
                            <img style="position: absolute; top: 15px; left: 8px;" src="/search.svg" alt="search_icon">
                            <input @input="onChangedSearchInput" class="input_search" type="text" placeholder="Поиск...">
                        </div>
                    </div>
                </div>
            </div>
            <Cardist :items="items" />
        </div>
    </div>
</template>

<style scoped lang="sass">
.wrapper
    width: 80%
    margin: 0 auto
    margin-top: 20px
    border-radius: 35px
    background-color: #fff

.content
    margin-top: 10px

.title
    font-size: 32px
    font-weight: bold
    padding-left: 60px 
    margin-top: 20px

.select_list
    height: 45px
    margin-right: 60px
    border-radius: 10px
    border: 1px solid #F3F3F3

.input_search
    height: 45px
    margin-right: 60px
    border-radius: 10px
    border: 1px solid #F3F3F3
    color: #C4C4C4
    font-size: 14px
    padding-left: 30px
    &:focus
        color: #000
</style>
