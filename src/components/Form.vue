<template>
    <div id="main-form">
        <p>Componente De Mensagem</p>
        <form id="burger-form" @submit="createBurger">
            <div class="input-container">
                <label for="nome">Nome Do Cliente</label>
                <input type="text" name="nome" v-model="nome" placeholder="digite o seu nome" id="nome">
            </div>

            <div class="input-container">
                <label for="pao">Escolha o pão</label>
                <select name="pao" id="pao" v-model="pao">
                    <option value="">Selecione o seu pão</option>
                    <option v-for="pao in paes" :key="pao.id" :value="pao.tipo">{{ pao.tipo }}</option>
                </select> 
            </div>

            <div class="input-container">
                <label for="carne">Escolha a carne</label>
                <select name="carne" id="carne" v-model="carne">
                    <option value="">Selecione a sua carne</option>
                    <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">{{carne.tipo}}</option>
                </select>
            </div>

            <div class="input-container">
                <label for="adicional">Escolha o Adicional</label>
                <select name="adicional" id="adicional" v-model="adicional">
                    <option value="">Selecione o seu Adicional</option>
                    <option v-for="adicional in adicionaldata" :key="adicional.id" :value="adicional.tipo">{{ adicional.tipo }}</option>
                </select>
            </div>

            <div id="option-container" class="input-container">
                <label id="option-title" for="acompanhamento">Escolha o Acompanhamento</label>
                <div class="checkbox-container" v-for="acompanhamento in acompanhamentosdata" :key="acompanhamento.id">
                <input type="checkbox" name="acompanhamento" v-model="acompanhamentos" :value="acompanhamento.tipo">
                <span>{{ acompanhamento.tipo }}</span>
            </div>
        </div>


            <div id="option-container" class="input-container">
                <label id="option-title" for="Bebidas">Escolha sua bebida</label>
                <div class="checkbox-container" v-for="bebida in bebidasdata" :key="bebida.id">
                    <input type="checkbox" name="bebidas" v-model="bebidas" :value="bebida.tipo">
                    <span>{{ bebida.tipo }}</span>
                </div>
            </div>

         
            <div class="input-container">
                <input type="submit" class="submit-btn" value="Enviar Pedido">
            </div>
            
        </form>
    </div>
</template>

<script>
import FormCSS from '../css/Form.css'

    export default {
        name: "Form",
        data () {
            return {
                paes: null,
                carnes: null,
                adicionaldata:null,
                bebidasdata:null, 
                opcionaisdata: null,
                acompanhamentodata: null,
                nome: null,
                pao: null,
                carne: null,
                adicional: [],
                acompanhamentos: [],
                bebidas: [],
                status: 'Solicitado',
                msg: null,
            }
        },
        methods: {
            async getIngredientes(){
                const req = await fetch("http://localhost:8083/Ingredientes");
                const data = await req.json();

                this.paes = data.paes;
                this.carnes = data.carnes;
                this.adicionaldata = data.adicional;
                this.bebidasdata = data.bebidas;
                this.acompanhamentosdata = data.acompanhamentos;

            },
            async createBurger(e) {
                e.preventDefault();
    
                const data = {
                    nome: this.nome,
                    pao: this.pao,
                    carne: this.carne,
                    adicional: this.adicional,
                    acompanhamentos: (this.acompanhamentos),
                    bebidas: Array.from(this.bebidas),
                    status: "Solicitado",

                }
                
               console.log(data)
            }
       },
        mounted(){
            this.getIngredientes()
        },  
        components: {
            FormCSS,
        }
    }
</script>