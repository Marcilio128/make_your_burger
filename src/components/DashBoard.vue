<template>
    <div id="burger-table">
        <Message :msg="msg" v-show="msg"/>
        <div>
            <div id="burgerhead">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Adicional:</div>
                <div>bebida:</div>
                <div>Acomp:</div>
                <div>Ações:</div>
            </div>
            <div id="burger-table-row">
                <div class="burger-table-row" v-for="Burger in Burgers" :key="Burger.id">
                    <div class="order-number">{{ Burger.id }}</div>
                    <div>{{ Burger.nome }}</div>
                    <div>{{ Burger.pao }}</div>
                    <div>{{ Burger.carne }}</div>
                    <div>{{ Burger.adicional }}</div>
                    <ul>
                        <li v-for="(bebidas, index) in Burger.bebidas" :key="index">{{ bebidas }}</li>
                    </ul>
                    <ul>
                        <li v-for="(acompanhamentos, index) in Burger.acompanhamentos" :key="index">{{ acompanhamentos }}</li>
                    </ul>
                    
                    <select name="status" class="status" @change="update($event, Burger.id)">
                        <option value="">Status do hamburger</option>
                        <option v-for="s in Status" :key="s.id" :value="s.tipo" :selected="Burger.status == s.tipo">{{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="Delete(Burger.id)">Cancelar</button>
                </div>

            </div>
        
        </div>

    </div>
</template>

<script>
import DashBoardCSS from '../css/DashBoard.css'
import Message from "../components/Message.vue"
    export default{
        name: "DashBoard",
        data () {
            return{
                Burgers: null,
                Burgers_id: null,
                Status: [],
                msg: null 
            }
        },
        methods: {
            async getPedidos() {
                const req = await fetch("http://localhost:8083/Burgers");
                const data = await req.json();
                this.Burgers = data;
                console.log(this.Burgers)

                this.getStatus();
            },
            async getStatus(){
                const req = await fetch("http://localhost:8083/Status");
        
                const data = await req.json()
        
                this.Status = data;

        },
        async Delete(id) {
            const req = await fetch(`http://localhost:8083/Burgers/${id}`, {
            method: "DELETE",
        });
        const res = await req.json();
        
        this.getPedidos();

        this.msg = `Pedido removido com sucesso`

        setTimeout(() => this.msg = "", 5000)

    },
        async update(event, id){
            const option = event.target.value;

            const datajson = JSON.stringify({ Status: option })

            const req = await fetch(`http://localhost:8083/Burgers/${id}`, {
                method: 'PATCH',
                headers: {"Content-type": "application/json"},
                body: datajson
            })

            const res = await req.json();

            console.log(res)

            this.msg = `Pedido n° ${res.id} atualizado para ${res.Status}`

            setTimeout(() => this.msg = "", 5000)

        }



    },
        mounted(){
            this.getPedidos();

        },
        components: {
            DashBoardCSS,
            Message
        }        
    }

</script>

<style scoped>

select{
    padding: 12px, 6px;
    border: 1px solid #222;

}

</style>