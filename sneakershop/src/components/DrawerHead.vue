<template>
    <div class="head_wrapper">
        <svg class="svg" width="16" height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M1 7H14.7143" stroke="black" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" />
            <path d="M8.71436 1L14.7144 7L8.71436 13" stroke="black" stroke-width="2" stroke-linecap="round"
                stroke-linejoin="round" />
        </svg>
        <h2 class="head__title">Корзина</h2>
    </div>
</template>

<style scoped lang="sass">
.head   
    &_wrapper
        display: flex
        align-items: center
        gap: 1.25rem
    &__title
        font-size: 24px
        font-weight: bold
        line-height: normal

.svg
    opacity: 0.3
    cursor: pointer
    transform: rotate(180deg)
    &:hover
        opacity: 1
</style>