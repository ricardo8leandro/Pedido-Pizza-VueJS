<template>
    <div id="pizza-table">
        <Message  :msg="msg" v-show="msg" />
        <div>
            <div id="pizza-table-heading">
                <div class="order-id">#</div>
                <div>Cliente:</div>
                <div>Tamanho:</div>
                <div>Recheio:</div>
                <div>Opcionais</div>
                <div>Ações</div>
            </div>
        </div>
        <div id="pizza-table-rows">
            <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
                <div class="order-number">{{pizza.id}}</div>
                <div>{{pizza.nome}}</div>
                <div>{{pizza.tamanho}}</div>
                <div>{{pizza.recheio}}</div>
                <div>
                    <ul>
                        <li v-for="(opcional, index) in pizza.opcionais" :key="index">{{opcional}}</li>
                    </ul>
                </div>
                <div>
                    <select name="status" id="status" @change="updatePizza($event, pizza.id)">
                        <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="pizza.status == s.tipo">{{s.tipo}}</option>
                    </select>
                    <button class="delete-btn" @click="deletePizza(pizza.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Message from './Message.vue';

export default {
    components: { Message },
    name: "Dashboard",
    data() {
        return {
            pizzas: null,
            pizza_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos() {

            const req = await fetch('http://localhost:3000/pizzas');

            const data = await req.json();

            this.pizzas = data;

            //resgatar dados

            console.log(this.pizzas);

            this.getStatus();

        },
        async getStatus() {

            const req = await fetch('http://localhost:3000/status');

            const data = await req.json();

            this.status = data;

        },
        async deletePizza(id) {

            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            this.msg = `Pedido removido com sucesso!`;

            setTimeout(() => this.msg = '', 3000);

            this.getPedidos();

        },
        async updatePizza(event, id) {

            const option = event.target.value;

            console.log(option);

            const dataJson = JSON.stringify({ status : option});

            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "PATCH",
                headers: {"content-Type": "application/json"},
                body:dataJson
            });

            const res = await req.json();

            this.msg = `Pedido Nº ${res.id} foi atualizado para ${res.status}`;

            setTimeout(() => this.msg = '', 3000);

            this.getStatus();

        }
    },
    mounted() {
        this.getPedidos();
    }
}
</script>
<style scoped>
#pizza-table {
    max-width: 1200px;
    margin: 0 auto;
}

#pizza-table-heading,
#pizza-table-rows,
.pizza-table-row {
    display: flex;
    flex-wrap: wrap;
}

#pizza-table-heading {
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}

#pizza-table-heading div,
.pizza-table-row div {
    width: 19%;
}

.pizza-table-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid #ccc;
}

#pizza-table-heading .order-id,
.pizza-table-row .order-number {
    width: 5%;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #222;
    color: #fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin:0 auto;
    cursor: pointer;
    transition: .5s;
}

.delete-btn:hover {
    background-color: transparent;
    color: #222;
}
</style>
