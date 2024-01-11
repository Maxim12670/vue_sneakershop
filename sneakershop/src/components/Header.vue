
<template>
    <header class="header">
        <div class="header__logo">
            <img src="/logo.png" alt="logo">
            <div>
                <h2 class="header__title">vue sneakers</h2>
                <p class="header__subtitle">Магазин лучших кроссовок</p>
            </div>
        </div>
        <ul class="navigation">
            <li class="navigation__item">
                <img src="/cart.svg" alt="cart">
                <b>1205 руб.</b>
            </li>
            <li class="navigation__item">
                <img src="/heart.svg" alt="heart">
                <span>Закладки</span>
            </li>
            <li class="navigation__item">
                <img src="/profile.svg" alt="profile">
                <span>Профиль</span>
            </li>
        </ul>
    </header>
</template>

<style scoped lang="sass">
.header
    display: flex
    justify-content: space-between
    padding: 20px 35px
    border-bottom: 1px solid #EAEAEA
    &__logo
        display: flex
        align-items: center
        gap: 1rem
        img
            width: 40px
    &__title
        color: #000
        font-size: 20px        
        font-weight: 700
        line-height: normal
        text-transform: uppercase
    &__subtitle
        color: #9D9D9D
        font-size: 14px
        font-weight: 400
        line-height: normal

.navigation
    display: flex
    gap: 2.5rem
    align-items: center
    &__item
        display: flex
        align-items: center
        gap: 0.75rem
        cursor: pointer
        color: rgb(107, 114, 128)
        &:hover
            color: rgb(0, 0, 0)
            font-weight: bold
</style>