<template>
    <h1>
        {{welcome}}
    </h1>
    <div>
        <p>To get started, type in the region, town or city you'd like to see the weather: <input type="text" v-bind:value="location"></p>
        <button @click="getWeather()">Get Weather</button>
        <p>
        {{data}}
        </p>
        <img v-bind:src="icon" alt="Weather Icon" srcset="">
    </div>
</template>


<script>
import axios from 'axios'

export default {
  name: 'WeatherApp',
  props: {

  },
  data (){
      return {
          welcome: 'Weather App',
          baseUrl: 'http://api.weatherapi.com/v1',
          apiMethod: '/current.json',
          key: 'key='+process.env.VUE_APP_API_KEY,
          data: null,
          location: '',
          aqi: 'yes',
          icon: ''
      }
  },
  mounted() {
      axios.get('http://ipwhois.app/json/')
        .then(response => {
            this.ipData = response.data
            console.log(this.ipData) // needed for now, will use it for other data
            this.location = this.ipData.country
            this.getWeather()
        })
},
  methods: {
      getWeather(){
      axios.post(this.baseUrl+this.apiMethod+'?'+this.key+'&'+'q='+this.location+'&'+'aqi='+this.aqi)
        .then(response => {
            this.data = response.data
            console.log(this.data)
            this.icon = this.data.current.condition.icon
        })
      },
  }
}
</script>
