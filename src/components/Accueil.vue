<template>


  <div>
    <div>
      <input type="text" id="position" v-model="requete" v-on:keypress="goMeteo">
    </div>

<div v-if="temps">
    <h3>Position: {{temps.name}}</h3>
    <h4>Température : {{temps.main.temp}}</h4>
    <h4>Temps : {{temps.weather[0].description}}</h4>
</div>


  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'Accueil',
  data(){
    return{
      requete: '',
      temps: undefined,
      api_code: '77e17860965e3743c05d064b8e9dcc98',
      url_recherche: 'https://api.openweathermap.org/data/2.5/weather?'
    }
  },
  methods: {
    goMeteo(e){
        if (e.key == "Enter") {
        axios
        .get(`${this.url_recherche}q=${this.requete}&units=metric&APPID=${this.api_code}&lang=fr`)
        .then(reponse =>{
          this.temps = reponse.data
        })
        this.requete = ''
        }
    }
  }
  
}
</script>

<style scoped>

</style>
