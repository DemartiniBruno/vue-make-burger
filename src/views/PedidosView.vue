<script lang="ts">
import Dashboard from '@/components/Dashboard.vue';
import { defineComponent } from 'vue';


export default defineComponent({
  name:'PedidosView',
  components:{
    Dashboard
  }
})
</script>

<template>
  <div class="about">
    <main class="main-container">
      <h1>Gerenciar Pedidos</h1>
      <Dashboard class="teste"/>
    </main>
  </div>
</template>

<style scoped>
 .main-container{
  margin-bottom: 214px;
 }
</style>
