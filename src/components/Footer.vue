<template>
    <footer>
        <p>make your burger &copy; 2021</p> 
    </footer>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { RouterLink } from 'vue-router';
    
export default defineComponent({
    name:'Footer'
})

</script>

<style scoped>
  footer {
    height: 200px;
    background-color: #222;
    border-top: 4px solid #111;
    color: #fcba03;
    display: flex;
    align-items: center;
    justify-content: center;
    bottom: 0;
    width: 100%;
  }
</style>