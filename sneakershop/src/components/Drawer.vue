<script setup>
import DrawerHead from "./DrawerHead.vue";
import CartItemList from "./CartItemList.vue";
import { inject } from "vue";

const { price } = inject('cart');
const { buttonDisabled, createOrder } = inject('order');
</script>

<template>
    <div class="wrapp">
        <div class="stub"></div>
        <div class="drawer">
            <DrawerHead />

            <CartItemList />

            <div class="result">
                <div class="result__wrapper">
                    <span class="result__caption">Итого:</span>
                    <div></div>
                    <b class="result__anmount">{{ price }} руб</b>
                </div>
                <div class="result__wrapper">
                    <span class="result__caption">Налог 5%:</span>
                    <div></div>
                    <b class="result__anmount">1074 руб</b>
                </div>
                <button @click="createOrder" :disabled="price === 0" class="result__btn">Оформить заказ</button>
            </div>
        </div>
    </div>
</template>

<style scoped lang="sass">
.wrapp
    display: flex
.stub
    position: fixed
    top: 0
    left: 0
    width: 100%
    height: 100%
    background-color: black
    z-index: 10
    opacity: 0.7
    box-shadow: -10px 4px 24px 0px rgba(0, 0, 0, 0.10)

.drawer
    position: fixed
    right: 0
    top: 0
    padding: 2rem
    width: 24rem
    height: 100%
    background-color: #fff
    z-index: 20

.result
    display: flex
    flex-direction: column
    margin-top: 30px
    &__wrapper
        display: flex
        margin-bottom: 20px
        div
            display: flex
            flex: 1
            margin: 0px 8px
            border-bottom: 1px dotted #DFDFDF
    &__caption
        font-size: 16px
    &__anmount
        font-size: 16px
        font-weight: bold
    &__btn
        height: 55px
        width: 100%
        border: none
        border-radius: 18px
        background-color: #9DD458
        color: #fff
        cursor: pointer
        &:disabled
            cursor: wait
            background-color: rgb(203 213 225)


        

        
</style>