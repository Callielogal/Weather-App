<template>
    <div class="weather">

        <div class="meteo" v-if="info">
            <h2>Prévisions météo des prochains jours</h2>
            <h3>Aujourd'hui</h3>
            <div class="hvr-grow">
                <img :src="weathericon">
            </div>
            <div>
                <p>Il fait :</p> <span class="temp"> {{info.list[0].main.temp}}° </span>
            </div>
            <p>Le vent souffle (sur les plaines de la bretagne armoriquaine) à :</p>
            <p class="wind"> {{info.list[0].wind.speed}}km</p>

            <h2>Les prochains jours...</h2>

            <div class="cards">

                <div class="card hvr-grow">
                    <p class="date">{{info.list[7].dt_txt}}</p>
                    <p class="temperature">{{info.list[7].main.temp}}°</p>
                    <p class="icon"><img :src="weathericon1"></p>
                </div>

                    <div class="card hvr-grow">
                    <p class="date">{{info.list[15].dt_txt}}</p>
                    <p class="temperature">{{info.list[15].main.temp}}°</p>
                    <p class="icon"><img :src="weathericon2"></p>
                </div>

                <div class="card hvr-grow">
                    <p class="date">{{info.list[23].dt_txt}}</p>
                    <p class="temperature">{{info.list[23].main.temp}}°</p>
                    <p class="icon"><img :src="weathericon3"></p>
                </div>

                <div class="card hvr-grow">
                    <p class="date">{{info.list[31].dt_txt}}</p>
                    <p class="temperature">{{info.list[31].main.temp}}°</p>
                    <p class="icon"><img :src="weathericon4"></p>
                </div>

                <div class="card hvr-grow">
                    <p class="date">{{info.list[39].dt_txt}}</p>
                    <p class="temperature">{{info.list[39].main.temp}}°</p>
                    <p class="icon"><img :src="weathericon5"></p>
                </div>

            </div>
        
        </div>

    </div>


</template>

<script>
import axios from 'axios'

export default {
    name: "Weather",
    data : function(){
        return{
            info: null,              
        }
    },
    computed:{
        weathericon: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[0].weather[0].icon + "@2x.png" : " " ; },    
        weathericon1: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[7].weather[0].icon + "@2x.png" : " " ; },
        weathericon2: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[15].weather[0].icon + "@2x.png" : " " ; },
        weathericon3: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[23].weather[0].icon + "@2x.png" : " " ; },
        weathericon4: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[31].weather[0].icon + "@2x.png" : " " ; },
        weathericon5: function(){ return this.info ? "https://openweathermap.org/img/wn/"+ this.info.list[39].weather[0].icon + "@2x.png" : " " ; },
    
    
    },

    methods:{
        getInfo:function(){
              axios.get("http://api.openweathermap.org/data/2.5/forecast?q=Lens,FR&units=metric&APPID=415d86c31731f7ef7ca607d709fa4e05")
           .then(response => (this.info = response.data))
   
        }
    },
    
    created(){

            axios.get("http://api.openweathermap.org/data/2.5/forecast?q=Lens,FR&units=metric&APPID=415d86c31731f7ef7ca607d709fa4e05")
           .then(response => (this.info = response.data))
        }
}
</script>
<style scoped>
p{
    font-style: oblique;
    font-size: 20px;
    font-weight: bold;
}
img{
    height: 15vh;
}

h2{
color: black;
background-color: rgb(239, 239, 239);
font-size: 30px;
width: 70%;
margin: auto;
border-radius: 10px;
box-shadow: 2px 2px 2px black;
margin-bottom: 1em;
}

h3{
    font-size: 30px;
    text-decoration: underline;
}

.meteo{
  
    margin: auto;
    text-align: center;
 
}

.cards{
    margin: auto;
    display: flex;
    flex-wrap: wrap;
    }

.card{
    width:10rem;
    border: solid black 2px;
    border-radius: 10px;
    box-shadow: 2px 2px 2px;
    margin: auto;
    margin-bottom: 2vh;
 
}

.date{
    border-bottom: solid black 1px;
    line-height: 2em;
    font-weight: bold;
    text-shadow: 1px 1px 1px white;
    padding-bottom: 1em;
}

.temperature{
    color: crimson;
    background-color: navajowhite;
    font-weight: bold;
    width: 60%;
    margin: auto;
    line-height: 2em;
    border-radius: 10px;
}
.icon{
    margin-bottom: 0;
}

.hvr-grow {
  -webkit-transform: perspective(1px) translateZ(0);
  transform: perspective(1px) translateZ(0);
  box-shadow: 0 0 1px rgba(0, 0, 0, 0);
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  -webkit-transition-property: transform;
  transition-property: transform;
}
.hvr-grow:hover, .hvr-grow:focus, .hvr-grow:active {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.temp{
    font-weight: bold;
    font-style: italic;
    font-size: 30px;
}

.wind{
     font-weight: bold;
    font-style: italic;
    font-size: 30px;

}

.weather{
    box-sizing: border-box;
    background-size: cover;
    background-image: url('../assets/cloud.jpg');
    margin: 0;
}




</style>