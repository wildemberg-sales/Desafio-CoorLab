<template>
    <div class="center">
        <p>Estas são as melhores alternativas de frete que encontramos para você.</p>

        <div class="block-info-minor">

        <div class="block-info-img">
            <img src="./../assets/iconHand.png"/>
        </div>

        <div class="block-info-data">
            <p><span>Frete com menor valor</span><br/>
            Transportadora: {{ preco.name }}<br/>
            Tempo estimado: {{ preco.lead_time }}
            </p>
        </div>

        <div class="block-info-price">
            <p v-if="parseInt(this.peso) < 101"><span>Preço</span><br/>
                R$ {{ parseFloat(precoFloatMVL * pesoInt).toFixed(2)}}
            </p>
            <p v-else><span>Preço</span><br/>
                R$ {{ parseFloat(precoFloatMVH * pesoInt).toFixed(2)}}
            </p>
        </div>

        </div><!--block-info-minor - bloco para mostrar o menor preço-->

        <div class="block-info-fast">

        <div class="block-info-img">
            <img src="./../assets/iconTime.png"/>
        </div>

        <div class="block-info-data">
            <p><span>Frete mais rápido</span><br/>
            Transportadora: {{tempo.name}} <br/>
            Tempo estimado: {{ tempo.lead_time }} 
            </p>
        </div>

        <div class="block-info-price">
            <p v-if="parseInt(this.peso) < 101"><span>Preço</span><br/>
                R$ {{ parseFloat(precoFloatTL * pesoInt).toFixed(2) }}
            </p>
            <p v-else><span>Preço</span><br/>
                R$ {{ parseFloat(precoFloatTH * pesoInt).toFixed(2) }}
            </p>
        </div>
        
        </div><!--block-info-fast - bloco para mostrar o mais rápido-->

    </div><!--center-->
</template>
<script>

    import {convertFloat} from './BestTransport.vue'


    export default {
        name: "ResponseMsg",
        props:{
            preco:{type: Object},
            tempo:{type:Object},
            peso:String
        },
        data(){
            return{
                pesoInt: parseInt(this.peso),
                precoFloatMVL: convertFloat(this.preco.cost_transport_light),
                precoFloatMVH: convertFloat(this.preco.cost_transport_heavy),
                precoFloatTL: convertFloat(this.tempo.cost_transport_light),
                precoFloatTH: convertFloat(this.tempo.cost_transport_heavy)
            }
        }
    }
    
    
</script>
<style>
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
.block-info-img img{
    width: 60px;
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

</style>