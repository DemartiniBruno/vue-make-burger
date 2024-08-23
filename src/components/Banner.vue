<template>
    <section id="main-banner">
        <h1>Make Your Burger</h1>
    </section>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'Banner'
})
</script>

<style scoped>
#main-banner{
    background-image: url('/img/burger.jpg');
    background-position: 0 -420px;
    background-size: cover;
    height: 600px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

#main-banner h1{
    color: #fff;
    text-align: center;
    font-size: 60px;
    padding: 20px 40px;
}
</style>