<script setup>
defineProps({
    title: String,
    imageUrl: String,
    price: Number,
    isFavorite: Boolean,
    isAdded: Boolean,
    onClickAdd: Function,
    onClickFavorite: Function
})
</script>

<template>
    <div class="card__wrapper">
        <img @click="onClickFavorite" :src="!isFavorite ? '../../public/like-1.svg' : '../../public/like-2.svg'"
            alt="favorite" class="btn_favorite">
        <img :src="imageUrl" alt="sneaker">
        <p>{{ title }}</p>

        <div class="card__desrc">
            <div class="card__info">
                <span class="card__info_price">Цена:</span>
                <b>{{ price }}</b>
            </div>
            <img @click="onClickAdd" :src="!isAdded ? '../../public/plus.svg' : '../../public/checked.svg'" alt="plus">
        </div>

    </div>
</template>

<style scoped lang="sass">
.card
    &__wrapper
            position: relative
            margin-top: 30px
            padding: 2rem
            border: 1px solid #F3F3F3
            border-radius: 1.5rem
            background-color: #fff
            cursor: pointer
            &:hover
                transform: translateY(-8px)
                box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1), 0 8px 10px -6px rgb(0 0 0 / 0.1)
    &__desrc
        display: flex
        justify-content: space-between
        margin-top: 14px
    &__info
        display: flex
        flex-direction: column
        &_price
            color: rgb(148 163 184)

.btn_favorite
    position: absolute
    top: 30px
    left: 30px
</style>