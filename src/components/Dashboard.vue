<script lang="ts">
import { defineComponent } from 'vue';
import Message from './Message.vue';

type Burger = {
    id: number,
    nome: string,
    pao: string,
    carne: string,
    opcionais: Array<string>,
    status: string
}

type Stats = {
    id: number,
    tipo: string
}

export default defineComponent({
    name: 'Dashboard',
    components:{
        Message
    },
    data() {
        return {
            burgers: [] as Burger[],
            status: [] as Stats[],
            msg: ''
        }
    },
    methods: {
        async getBurguers() {
            const reqBurgers = await fetch('http://localhost:3000/burgers')
            this.burgers = await reqBurgers.json()

        },

        async getStatus() {
            const reqStatus = await fetch('http://localhost:3000/status')
            this.status = await reqStatus.json()
        },

        async deletePedido(id:any){
            this.msg = `Pedido ${id} cancelado`
            setTimeout(() => this.msg = '', 3 * 1000)

            await fetch(`http://localhost:3000/burgers/${id}`,{
                method: 'DELETE'
            })
            this.getBurguers()
        },

        async updatePedido(event:any, id:any){
            await fetch(`http://localhost:3000/burgers/${id}`,{
                method: 'PATCH',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({status: event.target.value})
            })

            this.msg = `Pedido ${id} alterado para: ${event.target.value}`
            setTimeout(() => this.msg = '', 3 * 1000)

        }
    },
    mounted() {
        this.getBurguers();
        this.getStatus();
    }
})

</script>

<template>
    <div id="burger-table">
        <div id="msg">
            <Message class="teste" :msg/>
        </div>
        <div>
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
            <div id="burger-table-rows">
                <div v-for="burger in burgers" :key="burger.id" class="burger-table-row">
                    <div id="id">{{ burger.id }}</div>
                    <div>{{ burger.nome }}</div>
                    <div>{{ burger.pao }}</div>
                    <div>{{ burger.carne }}</div>
                    <div>
                        <ul>
                            <li v-for="(opcional, index) in burger.opcionais" :key="index">
                                {{ opcional }}
                            </li>
                        </ul>
                    </div>
                    <div>
                        <select @change="updatePedido($event ,burger.id)" name="status" class="status">
                            <!-- <option :value="burger.status">{{ burger.status }}</option> -->
                            <option v-for="stats in status" :key="stats.id" :value="stats.tipo" :selected="stats.tipo == burger.status">{{ stats.tipo }}</option>
                        </select>
                        <button @click="deletePedido(burger.id)" class="delete-btn">Cancelar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
#msg{
    position: absolute;
    top: 15%;
}

#id {
    width: 55px;
}

#burger-table {
    max-width: 1200px;
    margin: 0 auto;
}

#burger-table-heading,
#burger-table-rows,
.burger-table-row {
    display: flex;
    flex-wrap: wrap;
}

#burger-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

.burger-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #CCC;
}

#burger-table-heading div,
.burger-table-row div {
    width: 19%;
}

#burger-table-heading .order-id,
.burger-table-row .order-number {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
    width: 100px;
}

.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>