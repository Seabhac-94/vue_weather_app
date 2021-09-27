<template>
    <h1>
        {{welcome}}
    </h1>
    <div>
        <form action="" method="get"></form>
        <p>To get started, type in the region, town or city you'd like to see the weather: <input type="text" v-model="location"></p>
        <button @click="getWeather()">Get Weather</button>
        <p>
        {{data}}
        </p>
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
          aqi: 'yes'
      }
  },
  mounted() {

  },
  methods: {
      getWeather(){
      axios.post(this.baseUrl+this.apiMethod+'?'+this.key+'&'+'q='+this.location+'&'+'aqi='+this.aqi)
        .then(response => {
            this.data = response.data
            console.log(this.data)
        })
      }
  }
}
</script>
