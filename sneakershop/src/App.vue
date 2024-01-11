<script setup>
import Header from "./components/Header.vue";
import Cardist from "./components/CardList.vue";
import Drawer from "./components/Drawer.vue";
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
                        <select class="select_list">
                            <option>По названию</option>
                            <option>По возрастанию цены</option>
                            <option>По убыванию цены</option>
                        </select>
                        <div style="position: relative;">
                            <img style="position: absolute; top: 15px; left: 8px;" src="../public/search.svg" alt="search_icon">
                            <input class="input_search" type="text" placeholder="Поиск...">
                        </div>
                    </div>
                </div>
            </div>
            <Cardist />
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
