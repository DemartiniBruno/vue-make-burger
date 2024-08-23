<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    name:'Message',
    props: {
        msg: String
    }
})
</script>

<template>
    <div v-show="msg" class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>

<style scoped>

    .message-container{
        color: darkblue;
        background-color: rgb(198, 237, 250);
        border: 2px solid rgb(171, 221, 238);
        border-radius: 5px;
        padding: 10px;
        max-width: 400px;
        margin: 30px auto;
    }

</style>