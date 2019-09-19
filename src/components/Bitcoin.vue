<template>
    <div class=" bitcoin">
        <h2> Comparaison Bitcoin</h2>
        
          <div>
              Euro: <span v-if="info">{{info.bpi.EUR.rate}}</span>e
          </div>
        <button @click="getInfo">Recupere les infos</button>
      
        
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: "Bitcoin",
    data : function(){
        return{
            info: null
        }
    },
    methods:{
        getInfo:function(){
              axios.get("https://api.coindesk.com/v1/bpi/currentprice.json")
           .then(response => (this.info = response.data))
         
        }
    },
    
    created(){

           axios.get("https://api.coindesk.com/v1/bpi/currentprice.json")
           .then(response => (this.info = response.data))
         
    }
}
</script>