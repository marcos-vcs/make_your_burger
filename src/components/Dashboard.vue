<template>
    <div class="main-container">
        <message ref="messageRef"></message>
        <div class="table-wrapper">
            <table>
                <thead>
                    <tr>
                        <th>#:</th>
                        <th>Clientes:</th>
                        <th>Pão:</th>
                        <th>Carne:</th>
                        <th>Opcionais:</th>
                        <th>Ações:</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="burger in burgers" :key="burger.id">
                        <td>{{ burger.id }}</td>
                        <td>{{ burger.nome }}</td>
                        <td>{{ burger.pao }}</td>
                        <td>{{ burger.carne }}</td>
                        <td>
                            <ul>
                                <li v-for="(opcional, index) in burger.opcionais" :key="index">
                                    {{opcional}}
                                </li>
                            </ul>
                        </td>
                        <td>
                            <select name="status" class="status" @change="updateBurger($event, burger.id)">
                                <option value="">Selecione</option>
                                <option 
                                    v-for="s in status" 
                                    :key="s.id" 
                                    :value="s.tipo" 
                                    :selected="burger.status == s.tipo">
                                        {{s.tipo}}
                                </option>
                            </select>
                            <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                        </td>

                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import Message from './Message.vue';

export default {
    name: 'Dashboard',
    components: {
        Message,
    },
    data(){
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null,
        }
    },
    methods: {
        async getPedidos(){
            const req = await fetch('http://localhost:3000/burgers');
            const data = await req.json();
            this.burgers = data;

            // resgatando os status
            this.getStatus();
        },
        async getStatus(){
            const req = await fetch('http://localhost:3000/status');
            const data = await req.json();
            this.status = data;
        },
        async deleteBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            this.$refs.messageRef.get(`Pedido removido com sucesso`);
            this.getPedidos();
        },
        async updateBurger(event, id){
            const option = event.target.value;
            const dataJson = JSON.stringify({status: option});
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: 'PATCH',
                headers: {'Content-Type': 'application/json'},
                body: dataJson
            });

            const res = await req.json();
            this.$refs.messageRef.get(`O pedido Nº ${res.id} foi atualizado para ${res.status}`);
        }
    },
    mounted(){
        this.getPedidos();
    }
}
</script>

<style scoped>
.table-wrapper {
    max-height: 500px;
    overflow-y: auto;
}
table {
  width: 100%;
  border-collapse: collapse;
  border: none;
}
table thead{
    font-weight: bold;
    padding: 12px;
    border-bottom: 3px solid #333;
}
table tbody tr{
    border-bottom: 1px solid #dddddd;
}
table tbody tr:last-child{
    border-bottom: none;
}

thead tr th{
    padding-top: 10px;
    padding-bottom: 10px;
    text-align: left;
}

tbody tr td{
    padding-top: 8px;
    padding-bottom: 8px;
}

td:first-child{
    text-align: left;
    min-width: 60px;    
}

thead tr th:first-child + th{
    text-align: left;
}
td:first-child + td{
    text-align: left;
    min-width: 350px;
}

thead tr th:first-child + th + th{
    text-align: left;
}
td:first-child + td + td{
    text-align: left;
    min-width: 200px;
}

thead tr th:first-child + th + th + th{
    text-align: left;
}
td:first-child + td + td + td{
    text-align: left;
    min-width: 170px;
}

thead tr th:first-child + th + th + th + th{
    text-align: left;
}
td:first-child + td + td + td + td{
    text-align: left;
    min-width: 120px;
}

thead tr th:last-child{
    text-align: left;
}
td:last-child{
    text-align: left;
    min-width: 220px;
}

select {
    padding: 12px 6px;
    margin-right: 12px;
}

.delete-btn {
    background-color: #222;
    color: #FCBA03;
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