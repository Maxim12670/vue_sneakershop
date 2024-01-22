<script setup>

</script>

<template>
    <div class="cart">
        <img class="cart__img" src="../../public/package-icon.png" alt="packageIcon">
        <h2 class="cart__title">
            Корзина пустая
        </h2>
        <div class="cart__descr">
            Добавьте хотя бы одну пару<br>
            кроссовок, чтобы сделать заказ.
        </div>
    </div>
</template>

<style scoped lang="sass">
.cart
    display: flex
    flex-direction: column
    margin-top: 310px
    &__img
        display: block
        margin: 0 auto
        width: 120px
        height: 120px
    &__title
        margin: 0 auto
        margin-top: 21px
        color: #000
        font-size: 22px
        font-weight: 600
    &__descr
        margin-top: 10px
        color: #000
        text-align: center
        font-size: 16px
        font-weight: 400
        line-height: 24px
</style>