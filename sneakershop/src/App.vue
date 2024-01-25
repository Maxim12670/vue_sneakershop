<script setup>
import { ref, provide, computed } from "vue";
import Header from "./components/Header.vue";
import Drawer from "./components/Drawer.vue";

const drawerFlag = ref(false);
const cart = ref([]);

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

provide('optionsDrawer', openDrawer);
provide('cart', {
    cart,
    price,
    addToCart
});
provide('order', {
    createOrder
})
</script>

<template>
    <Drawer v-if="drawerFlag"/>
    <div class="wrapper">
        <Header/>
        <router-view></router-view>
    </div>
</template>

<style scoped lang="sass">
.wrapper
    width: 80%
    margin: 0 auto
    margin-top: 20px
    border-radius: 35px
    background-color: #fff
</style>
