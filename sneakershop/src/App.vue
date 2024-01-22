<script setup>
import { onMounted, reactive, ref, provide, watch, computed } from "vue";

import Header from "./components/Header.vue";
import Cardist from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";

const drawerFlag = ref(false);
const buttonDisabled = ref(false);
const items = ref([]);
const cart = ref([]);
const filters = reactive({
    sortBy: 'title',
    searchQuery: ''
});

const createOrder = () => {
    try{
        const obj = {
            items: cart.value,
            totalPrice: price.value
        }

        if(cart.value) {
            const data = fetch('https://6ffbb2d6fa3c52ee.mokky.dev/carts', {
                method: 'POST',
                body: JSON.stringify(obj),
                headers: {
                    "Content-type": "application/json; charset=UTF-8"
                }
            });

            cart.value = [];
            items.value = items.value.map(item => {
                return {
                    ...item,
                    isAdded: false
                }
            })
            console.log('отправил');
        }
        else{
            console.log('массив пустой');
        }
    }
    catch(error){
        console.log(`Произошла ошибка: ${error}!`);
    }
}

const price = computed(
    () => cart.value.reduce((acc, item) => acc + item.price, 0)
);

const addToCart = (item) => {
    if(!item.isAdded) {
        cart.value.push(item);
        item.isAdded = true;
    }
    else {
        cart.value.splice(cart.value.indexOf(item), 1);
        item.isAdded = false;
    }
}

const openDrawer = () => {
    drawerFlag.value = !drawerFlag.value;
}

const getFavoriteItems = async () => {
    try {
        const favorites = await fetch('https://6ffbb2d6fa3c52ee.mokky.dev/favorite')
            .then(res => res.json());

        items.value = items.value.map(item => {
            const favorite = favorites.find(favorite => favorite.parentId === item.id);

            if (!favorite) {
                return item;
            }

            return {
                ...item,
                isFavorite: true,
                favoriteId: favorite.id
            }
        });
    }
    catch (error) {
        console.log(`Произошла ошибка: ${error}`);
    }
}

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
            .then(res => res.json());

        items.value = data.map((obj) => ({
            ...obj,
            favoriteId: null,
            isFavorite: false,
            isAdded: false
        }));
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

onMounted(async () => {
    await getItems();
    await getFavoriteItems();
});

watch(filters, getItems);
provide('optionsDrawer', openDrawer);
provide('cart', {
    cart,
    price,
    addToCart,
    addToFavorite
});
provide('order', {
    buttonDisabled,
    createOrder
})

</script>

<template>
    <Drawer v-if="drawerFlag"/>
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
            <Cardist :items="items"/>
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
