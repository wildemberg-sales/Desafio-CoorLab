<template>
  <div class="title">
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand class="ml-2">
        <b>{{ appName }}</b>
      </b-navbar-brand>
    </b-navbar>

    <div class="block">
      <div class="nav-block"><img src="./../assets/logo.png"/>Melhor Frete</div>

      <div class="content">
        
        <div class="content-form">

          <div class="title-form">
            <img src="./../assets/logo.png"/>Insira o destino e o peso
          </div>

          <div class="form-inputs">

            <label>Destino</label>
              <select name="estado" id="input-estado">
                <option value="">Selecione o destino</option>
              </select>
            
            <label for="input-peso">Peso</label>
              <input type="number" placeholder="Peso da carga em Kg" id="input-peso"/>
            
          </div>

          <button>Analisar</button>
          
        </div>

        <div class="response">
          <div class="msg-no-select">Nenhum dado selecionado</div>

          <div class="msg-select">
            <div class="center">
            <p>Estas são as melhores alternativas de frete que encontramos para você.</p>

            <div class="block-info-minor">
              <div class="block-info-img">
                <img src="./../assets/logo.png"/>
              </div>
              <div class="block-info-data">
                <p><span>Frete com menor valor</span><br/>
                  Transportadora: blabla <br/>
                  Tempo estimado: 12h
                </p>
              </div>
              <div class="block-info-price">
                <p><span>Preço</span><br/>
                  R$ 20,00
                </p>
              </div>
            </div>

            <div class="block-info-fast">
              <div class="block-info-img">
                <img src="./../assets/logo.png"/>
              </div>
              <div class="block-info-data">
                <p><span>Frete mais rápido</span><br/>
                  Transportadora: blabla <br/>
                  Tempo estimado: 12h 
                </p>
                
              </div>
              <div class="block-info-price">
                <p><span>Preço</span><br/>
                  R$ 20,00
                </p>
              </div>
            </div>
            
            </div>
          
          </div>
        
        </div>

      
      </div>
    
    </div>
  
  </div>

</template>

<script>
import {
  BNavbar,
  BNavbarBrand,
} from 'bootstrap-vue'

export default {
  components: {
    BNavbar,
    BNavbarBrand,
  },
  data() {
    const appName = ''

    return {
      appName,
    }
  },
  created() {
    // Implemente aqui o GET dos dados da API REST
    // para que isso ocorra na inicialização da pagina
    this.appName = 'Melhor Frete'
  },
  methods: {
    // Implemente aqui os metodos utilizados na pagina
    methodFoo() {
      console.log(this.appName)
    },
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
}

.content-form{
  width: 30%;
  height: 600px;
  margin-right: 30px;
  background-color: #ccc;
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

.content-form button{
  padding: 5px 40px;
  background-color: #00aca6;
  color: #fff;
  border: none;
  border-radius: 5px;
}

.response{
  width: calc(70% - 30px);
  border: 1px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
}
.response span{
  font-weight: bold;
}

.msg-no-select{
  display: none;
  font-size: 30px;
  font-weight: bold;
  color: #817f7f;
}

.msg-select{
  border: 1px solid;
  width: 80%;
  padding: 20px;
}

.center{
  
}
.block-info-minor, .block-info-fast{
  display: flex;
  margin-bottom: 10px;
}

.block-info-img{
  padding: 10px 20px;
  background-color: #00aca6;
  border-bottom-left-radius: 5px;
  border-top-left-radius: 5px;
}

.block-info-data{
  padding: 0 20px;
  width: 40%;
  background-color: #ccc;
  border-bottom-right-radius: 5px;
  border-top-right-radius: 5px;
}

.block-info-price{
  margin-left: 10px;
  background-color: #ccc;
  border-radius: 5px;
  padding: 10px 40px 10px 20px;
}
</style>
