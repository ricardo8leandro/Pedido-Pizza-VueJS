<template>
    <div>
        <Message  :msg="msg" v-show="msg" />
        <div>
            <form id="pizza-form" @submit="createPizza">
                <div class="input-container">
                    <label for="nome">Nome do Cliente:</label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome">
                </div>
                <div class="input-container">
                    <label for="tamanho">Ecolha o Tamanha da sua Pizza:</label>
                    <select name="tamanho" id="tamanho" v-model="tamanho">
                        <option value="" selected="selected">Selecione o tamanho da sua Pizza</option>
                        <option v-for="tamanho in tamanhos" :key="tamanho.id" :value="tamanho.tipo">
                            {{ tamanho.tipo }}
                        </option>
                    </select>
                </div>
                <div class="input-container">
                    <label for="recheio">Ecolha o recheio da sua pizza:</label>
                    <select name="recheio" id="recheio" v-model="recheio">
                        <option value="">Selecione o recheio</option>
                        <option v-for="recheio in recheios" :key="recheio.id" :value="recheio.tipo">
                            {{ recheio.tipo }}
                        </option>                    
                    </select>
                </div>
                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Selecione os opcionais:</label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>
                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu pizza">
                </div>
            </form>
        </div>
    </div>
</template>
<script>
import { createBlock } from 'vue';
import Message from './Message.vue';

export default {
  components: { Message },
    name: "pizzaForm",
    data() {
        return {
            tamanhos: null,
            recheios: null,
            opcionaisdata: null,
            nome: null,
            tamanho: null,
            opcionais: [],
            status: "solicitado",
            msg: null
        }
    },
    methods: {
        async getIngredientes() {

            const req = await fetch('http://localhost:3000/ingredientes');
            const data = await req.json();

            this.tamanhos = data.tamanhos;
            this.recheios = data.recheios;
            this.opcionaisdata = data.opcionais;
        },
        async createPizza(e) {

            e.preventDefault();

            const data = {
                nome: this.nome,
                recheio: this.recheio,
                tamanho: this.tamanho,
                opcionais: Array.from(this.opcionais),
                status: "solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch('http://localhost:3000/pizzas', {
                method: "POST",
                headers: {"content-Type": "application/json"},
                body:dataJson
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} realizado com sucesso!`;


            setTimeout(() => this.msg = '', 3000);

                this.nome = "";
                this.recheio = "";
                this.tamanho = "";
                this.opcionais = "";


        }
    }, mounted() {
        this.getIngredientes();
    }
}
</script>
<style scoped>
#pizza-form {
    max-width: 400px;
    margin: 0 auto 200px;
}

.input-container {
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color:#222;
    padding: 5px 10px;
    border-left:4px solid #FCBA03;
}

input, select {
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container {
    flex-direction:row;
    flex-wrap: wrap;
}

#opcionais-title {
    width:100%;
}

.checkbox-container {
    display: flex;
    align-items: flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span, 
.checkbox-container input {
    margin-left: 5px;
} 

.checkbox-container input {
    width: auto;
} 

.checkbox-container span {
    font-weight:bold;
} 

.submit-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding:10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

.submit-btn:hover {
    background-color: transparent;
    color:#222;
}
</style>
