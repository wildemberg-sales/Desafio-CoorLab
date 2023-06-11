<template>
  <div>
    <div class="title">
      <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand class="ml-2">
          <b>{{ appName }}</b>
        </b-navbar-brand>
      </b-navbar>
    </div>

    <div class="block">
      <div class="nav-block"><img src="./../assets/logo.png"/>Melhor Frete</div>

      <div class="content">
        
        <div class="content-form">

          <div class="title-form">
            <img src="./../assets/iconMap.png"/>Insira o destino e o peso
          </div><!--title-form-->

          <div class="form-inputs">

            <label>Destino</label>
              <select name="estado" id="input-estado" v-model="citySelected">
                <option value="" default>Selecione o destino</option>
                <option v-for="(obj) in cities" v-bind:key="obj.id" :value="obj">{{ obj }}</option>
              </select>
            
            <label for="input-peso">Peso</label>
              <input type="number" placeholder="Peso da carga em Kg" id="input-peso" v-model="peso" min="0"/>
            
          </div><!--form-inputs - bloco onde ficam os inputs-->

          <button @click="analisar">Analisar</button>
          
        </div><!--content-form - bloco onde fica o formulário-->

        <div class="box-response">
          <div class="response">

          <div class="msg-select" v-if="showResponse" >
            <ResponseMsg :preco="menorPreco" :tempo="menorTempo" :peso="peso"/>
          </div><!--msg-select - mensagem de retorno quando os dados forem analisados-->
        
          <div class="msg-no-select" v-else>Nenhum dado selecionado</div><!--msg-no-select-->

          </div><!--response - bloco de resposta-->

          <div class="box-button-clear" id="box-button-clear">
            <button class="button-clear" @click="clearValues">Limpar</button>
          </div><!--box-button-clear - Utilizado para limpar os valores-->

        </div>
        

        
      </div><!--content - bloco onde fica todos os conteúdos-->
      
    </div><!--block - bloco onde irá ficar os conteúdos e formulários-->
     
    <div class="overlay-modal" id="overlay">
      <div class="modal-box">
        <div class="modal-img">
          <img src="./../assets/iconErro.png"/>
        </div>
        <p>Insira os valores para realizar a análise.</p>
        <button @click="closeOverlay">Fechar</button>
      </div><!--modal-box - modal de erro-->
    </div><!--overlay-modal - overlay para inserção do modal de erro-->

  </div>

</template>

<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

<script>
import {
  BNavbar,
  BNavbarBrand,
} from 'bootstrap-vue'
import ResponseMsg from './ResponseMsg.vue'

const axios = require('axios').default;

export function convertFloat(val) {
  // Remove o símbolo de R$ e quaisquer espaços em branco
  const valorSemSimbolo = val.replace(/R\$\s*/g, '');
  const valorFloat = parseFloat(valorSemSimbolo);

  return valorFloat;
}

function retiraH(val) {
  const valorSemH = val.slice(0, -1);
  const valorInteiro = parseInt(valorSemH);

  return valorInteiro;
}

export default {
  components: {
    BNavbar,
    BNavbarBrand,
    ResponseMsg
  },
  data() {
    const appName = ''
    const data = []
    const cities = []
    const citySelected = ""
    const peso =""
    const menorPreco = {}
    const menorTempo = {}
    const showResponse = false
    return {
      appName,
      data,
      cities,
      citySelected,
      peso,
      menorPreco,
      menorTempo,
      showResponse
    }
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = 'Melhor Frete'

    axios.get('http://localhost:3000/transport')
    .then((res)=>{
      this.data = res.data;
      console.log(this.data);
      this.filterCities(res.data);
    })
    .catch(error => {console.log(error)})

  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina

    filterCities(val){
      let array = []
      val.map((value)=>{
        if(array.indexOf(value.city) == -1){
          array.push(value.city)
        }
      })
      this.cities = [...array];
      console.log(this.cities);
    },
    
    analisar(){
      if(this.citySelected == "" || this.peso == 0){

        const ov = document.getElementById("overlay");
        ov.style.display = "block";
      
      }else{
                      let menorValor = {name: "a",
                        cost_transport_light: "R$ 999.00",
                        cost_transport_heavy: "R$ 999.00",
                        city: "a",
                        lead_time: "999h"};
                      let menorTempo = {name: "a",
                        cost_transport_light: "R$ 999.00",
                        cost_transport_heavy: "R$ 999.00",
                        city: "a",
                        lead_time: "999h"};

        this.data.map(val=>{

          if(this.citySelected == val.city){

            //verifica o menor preço baseado no peso
            if(this.peso <= 100){
              let value_light = convertFloat(val.cost_transport_light);
              let menorVal_light = convertFloat(menorValor.cost_transport_light)

              if(value_light < menorVal_light){
                menorValor = val;
              }

            }else if(this.peso > 100){
              let value_heavy = convertFloat(val.cost_transport_heavy);
              let menorVal_heavy = convertFloat(menorValor.cost_transport_heavy)

              if(value_heavy < menorVal_heavy){
                menorValor = val;
              }

            }
            
            //Verifica o menor tempo
            let valH = retiraH(val.lead_time);
            let menorValH = retiraH(menorTempo.lead_time);
            if(valH <= menorValH){
              menorTempo = val;
            }

          }
          
        })

        this.menorPreco = menorValor;
        this.menorTempo = menorTempo;
        this.showResponse = true;
        document.getElementById("box-button-clear").style.display = "block";
        document.getElementById("input-peso").disabled = true
        document.getElementById("input-estado").disabled = true
      }
        
    },
    closeOverlay(){
      const ov = document.getElementById("overlay");
      ov.style.display = "none";
    },
    clearValues(){
      this.menorPreco = {}
      this.menorTempo = {}
      this.peso = ""
      this.citySelected = ""
      this.showResponse = false
      document.getElementById("box-button-clear").style.display = "none";
      document.getElementById("input-peso").disabled = false
      document.getElementById("input-estado").disabled = false
    }
  },
  
}
</script>

<style scoped>
.title .navbar {
  background-color: #00aca6 !important;
}

.title .navbar-brand {
  margin-left: 20px;
}

.block{
  margin: 20px 30px;
  border: 1px solid #000;
  border-radius: 10px;
}

.nav-block{
  background-color: #00aca6;
  padding: 10px 30px;
  border-top-right-radius: 10px;
  border-top-left-radius: 10px;
  display: flex;
  align-items: center;
  font-weight: bold;
  font-size: 20px;
}

.nav-block img, .title-form img, .block-info-img img{
  width: 50px;
  margin-right: 10px;
}

.content{
  padding: 30px 15px;
  display: flex;
  flex-wrap: wrap;
}

.content-form{
  width: 30%;
  height: 600px;
  margin-right: 30px;
  background-color: #dfdede;
  border-radius: 5px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.title-form{
  font-weight: bold;
  font-size: 20px;
}
.title-form img{
  width: 70px;
}

.form-inputs{
  width: 80%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

label{
  font-weight: bold;
  display: block;
  margin-top: 30px;
}
input{
  display: block;
  width: 100%;
  margin-bottom: 30px;
  padding: 8px;
  border-radius: 5px;
  border: none;
}
select{
  display: block;
  width: 100%;
  padding: 8px;
  border-radius: 5px;
  border: none;
}

.content-form button, .msg-select button, .modal-box button, .button-clear{
  padding: 5px 60px;
  background-color: #00aca6;
  border: none;
  border-radius: 5px;
  font-weight: 700;
  transition: 0.7s;
}
.content-form button:hover, .msg-select button:hover, .modal-box button:hover, .button-clear:hover{
  background-color: #06d4ce;
}

.response{
  width: 100%;
  height: calc(100% - 40px);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
}
.response span{
  font-weight: bold;
}

.msg-no-select{
  display: block;
  font-size: 30px;
  font-weight: bold;
  color: #817f7f;
  transition: 1s;
}

.msg-select{
  width: 100%;
  height: 100%;
  padding: 20px;
  transition: 1s;
}

.overlay-modal{
  display: none;
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgb(0, 0, 0, 0.8);
}

.modal-box{
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  background-color: white;
  padding: 30px;
  width: 60%;
  max-width: 600px;
  text-align: center;
  font-size: 25px;
  border-radius: 5px;
}
.modal-box button{
  font-size: 15px;
}

.modal-box p{
  margin: 30px;
}

.box-button-clear{
  display: none;
  width: 100%;
  height: 40px;
}
.button-clear{
  float: right;
  margin-right: 50px;
}

.box-response{
  width: calc(70% - 30px);
  display: flex;
  flex-wrap: wrap;
}
</style>
