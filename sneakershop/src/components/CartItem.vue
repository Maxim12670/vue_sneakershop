<script setup>
import { inject } from 'vue';

defineProps({
    title: String,
    imageUrl: String,
    price: Number,
    onClickAdd: Function,
});

const {addToCart} = inject('cart');

</script>

<template>
    <div class="cart">
        <img class="cart__photo" :src=imageUrl :alt=title>
        <div class="wrapper">
            <span class="cart__name">{{ title }}</span>
            <div class="container">
                <b class="cart__price">{{ price }} руб.</b>
                <img @click="onClickAdd" class="btn__delete" src="../../public/close.svg" alt="delete">
            </div>
        </div>
    </div>
</template>

<style scoped lang="sass">
.cart
    display: flex
    align-items: center
    justify-content: space-around
    height: 120px
    margin-top: 20px
    background-color: #fff
    border: 1px solid #F3F3F3
    border-radius: 20px
    &__photo
        width: 70px
        height: 70px
    &__name
        width: 150px
    &__price
        margin-top: 10px
        font-weight: bold
    &:hover 
        transform: translateY(-4px)

.wrapper
    display: flex
    flex-direction: column

.container
    display: flex
    justify-content: space-between

.btn__delete
    cursor: pointer


</style>