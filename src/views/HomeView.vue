<script lang="ts">
import Banner from '@/components/Banner.vue';
import BurgerForm from '../components/BurgerForm.vue';
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomeView',
  components:{
    Banner,
    BurgerForm
  }
})

</script>

<template>

  <Banner />
  <main class="main-container">
    <h1>Monte o seu burger:</h1>
    <BurgerForm />
  </main>
</template>

<style scoped>

</style>
