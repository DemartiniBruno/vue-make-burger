<script lang="ts">
import { defineComponent } from 'vue';
import Message from './Message.vue';


type Pao = {
    id: number,
    tipo: string
}

type Carne = {
    id: number,
    tipo: string
}

type Opcional = {
    id: number,
    tipo: string
}

export default defineComponent({
    name: "BurgerForm",
    components: {
        Message
    },
    data() {
        return {
            paes: {} as Pao[],
            carnes: {} as Carne[],
            opcionaisData: {} as Opcional[],
            nome: null,
            pao: 0,
            carne: 0,
            opcionais: [],
            msg: ''
        }
    },
    methods: {
        async getIngredientes() {
            const req = await fetch('http://localhost:3000/ingredientes')
            const data = await req.json()

            this.paes = data.paes
            // this.pao = 'Selecione o seu pão'
            this.carnes = data.carnes
            this.opcionaisData = data.opcionais

        },

        async createBurguer(e: any) {
            e.preventDefault();

            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            if(this.nome===null){
                this.msg = `Preencha seu nome`
                setTimeout(() => this.msg = '', 3 * 1000)
            }
            else if (data.pao === 0) {
                this.msg = `Selecione o pão`
                setTimeout(() => this.msg = '', 3 * 1000)

            } else if (data.carne === 0) {
                this.msg = `Selecione a carne`
                setTimeout(() => this.msg = '', 3 * 1000)
            } else {
                const req = await fetch('http://localhost:3000/burgers', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(data)
                })

                const res = await req.json()


                /* 
                    definindo msg
                */
                if (req.status === 201) {
                    this.msg = `Pedido Nº${res.id} Realizado`
                }


                /* 
                    limpando msg
                */
                setTimeout(() => this.msg = '', 3 * 1000)


                /* 
                    deixando campos vazios
                */
                this.nome = null;
                this.pao = 0;
                this.carne = 0;
                this.opcionais = [];
            }


        }
    },
    mounted() {
        this.getIngredientes()
    }


})
</script>


<template>
    <div>
        <Message :msg/>
        <div>
            <form id="burger-form" @submit="createBurguer($event)">
                <div class="input-container">
                    <label for="nome">Nome do cliente:</label>
                    <input type="text" id="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>

                <div class="input-container">
                    <label for="pao">Escolha o pão:</label>
                    <select name="pao" id="pao" v-model="pao">
                        <option disabled value="0">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                            {{ pao.tipo }}
                        </option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha a carne:</label>
                    <select name="carne" id="carne" v-model="carne">
                        <option disabled value="0">Selecione o tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
                            {{ carne.tipo }}
                        </option>
                    </select>
                </div>
                <div id="opcionais-title" class="input-container">
                    <label for="opcionais">Selecione os opcionais:</label>
                    <div v-for="opcional in opcionaisData" :key="opcional.id" class="checkbox-container">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar Burguer">
                </div>
            </form>
        </div>
    </div>
</template>


<style scoped>
#burger-form {
    max-width: 400px;
    margin: 0 auto;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    ;
    padding: 5px 10px;
    border-left: 4px solid #fcba03;
}

input,
select {
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container {
    flex-direction: row;
    flex-wrap: wrap;
}

#opcionais-title {
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn {
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

.submit-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>