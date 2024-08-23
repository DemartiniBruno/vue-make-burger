<template>
  <header>
    <Navbar :src="logo_src" :alt="app_name" />
  </header>

  <RouterView />

  <Footer />
</template>

<script lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'App',
  data() {
    return {
      logo_src: '/public/img/logo.png',
      app_name: 'Make Your Burguer'
    }
  },
  components: {
    Navbar,
    Footer
  }
})
</script>


<style>
  * {
    font-family: Helvetica;
    padding: 0;
    margin: 0;
    box-sizing: border-box;
  }

  .main-container {
    margin: 50px;
    min-height: 300px;
  }

  h1 {
    text-align: center;
    font-size: 42px;
    margin-bottom: 30px;
    color: #222;
  }
</style>
