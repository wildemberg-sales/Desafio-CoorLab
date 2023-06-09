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
              <select name="estado" id="input-estado">
                <option value="">Selecione o destino</option>
              </select>
            
            <label for="input-peso">Peso</label>
              <input type="number" placeholder="Peso da carga em Kg" id="input-peso"/>
            
          </div><!--form-inputs - bloco onde ficam os inputs-->

          <button>Analisar</button>
          
        </div><!--content-form - bloco onde fica o formulário-->

        <div class="response">
          <div class="msg-no-select">Nenhum dado selecionado</div><!--msg-no-select-->

          <div class="msg-select">
            <div class="center">
              <p>Estas são as melhores alternativas de frete que encontramos para você.</p>

              <div class="block-info-minor">

                <div class="block-info-img">
                  <img src="./../assets/iconHand.png"/>
                </div>

                <div class="block-info-data">
                  <p><span>Frete com menor valor</span><br/>
                    Transportadora: blabla <br/>
                    Tempo estimado: 12h
                  </p>
                </div>

                <div class="block-info-price">
                  <p><span>Preço</span><br/>
                    R$ 200000,00
                  </p>
                </div>

              </div><!--block-info-minor - bloco para mostrar o menor preço-->

              <div class="block-info-fast">

                <div class="block-info-img">
                  <img src="./../assets/iconTime.png"/>
                </div>

                <div class="block-info-data">
                  <p><span>Frete mais rápido</span><br/>
                    Transportadora: blabla <br/>
                    Tempo estimado: 12h 
                  </p>
                </div>

                <div class="block-info-price">
                  <p><span>Preço</span><br/>
                    R$ 20000,00
                  </p>
                </div>
                
              </div><!--block-info-fast - bloco para mostrar o mais rápido-->
              
              <button>Limpar</button>

            </div><!--center-->
          
          </div><!--msg-select - mensagem de retorno quando os dados forem analisados-->
        
        </div><!--response - bloco de resposta-->

      
      </div><!--content - bloco onde fica todos os conteúdos-->
      
    </div><!--block - bloco onde irá ficar os conteúdos e formulários-->
     
    <div class="overlay-modal">
      <div class="modal-box">
        <div class="modal-img">
          <img src="./../assets/iconErro.png"/>
        </div>
        <p>Insira os valores para realizar a análise.</p>
        <button>Fechar</button>
      </div><!--modal-box - modal de erro-->
    </div><!--overlay-modal - overlay para inserção do modal de erro-->

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

.content-form button, .msg-select button, .modal-box button{
  padding: 5px 40px;
  background-color: #00aca6;
  border: none;
  border-radius: 5px;
  font-weight: 700;
  transition: 0.7s;
}
.content-form button:hover, .msg-select button:hover, .modal-box button:hover{
  background-color: #06d4ce;
}

.response{
  width: calc(70% - 30px);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 20px;
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
  width: 100%;
  height: 100%;
  padding: 20px;
}

.center{
  text-align: center;
}

.block-info-minor, .block-info-fast{
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
  text-align: left;
}

.block-info-img{
  padding: 20px 20px;
  background-color: #00aca6;
  border-bottom-left-radius: 5px;
  border-top-left-radius: 5px;
}

.block-info-data{
  padding: 0 20px;
  width: 40%;
  background-color: #dfdede;
  border-bottom-right-radius: 5px;
  border-top-right-radius: 5px;
}

.block-info-price{
  width: 200px;
  margin-left: 10px;
  background-color: #dfdede;
  border-radius: 5px;
  padding: 10px 20px;
}

.msg-select button{
  position: fixed;
  bottom: 150px;
  right: 100px;
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
</style>
