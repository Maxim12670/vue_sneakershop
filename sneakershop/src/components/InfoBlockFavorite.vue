<template>
    <div class="info-block">
        <img class="info-block__img" src="../../public/emoji-1.png" alt="img">
        <h2 class="info-block__title">
            Закладок нет :(
        </h2>
        <div class="info-block__subtitle">
            Вы ничего не добавляли в закладки
        </div>
        <router-link to="/">
            <button class="info-block__button">
                Вернуться назад
            </button>
        </router-link>
    </div>
</template>

<style scoped lang="sass">
.info-block
    display: flex
    flex-direction: column
    align-items: center
    height: 80vh
    &__img
        width: 70px
        height: 70px
        margin-top: 220px
    &__title
        margin-top: 30px
        color: #000
        text-align: center
        font-size: 24px
        font-weight: 600
    &__subtitle
        margin-top: 11px
        color: rgba(0, 0, 0, .4)
        font-weight: 400
        font-size: 16px
    &__button
        margin-top: 70px
        width: 245px
        height: 55px
        border: none
        border-radius: 18px
        background: #9DD458
        color: #fff
        font-size: 16px
        font-weight: 600
</style>