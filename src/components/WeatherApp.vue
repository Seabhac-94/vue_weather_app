<template>
    <h1>
        {{welcome}}
    </h1>
    <div>
        <p>To get started, type in the region, town or city you'd like to see the weather: <input name="inputLocation" v-model="location" type="text" /></p>
        <button @click="getWeather()">Get Weather</button>
        <p>
            {{ tempC }} / {{ selectedLocation }} / {{ conditionDescription }}
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
          tempC: '',
          icon: '',
          conditionDescription: '',
          selectedLocation: ''

      }
  },
  mounted() {
      axios.get('http://ipwhois.app/json/')
        .then(response => {
            this.ipData = response.data
            console.log(this.ipData) // needed for now, will use it for other data
            this.location = this.ipData.city
            this.getWeather()
        })
},
  methods: {
      getWeather(){
      this.selectedLocation = this.location
      axios.post(this.baseUrl+this.apiMethod+'?'+this.key+'&'+'q='+this.location+'&'+'aqi='+this.aqi)
        .then(response => {
            this.data = response.data
            console.log(this.data)
            this.current = this.data.current
            this.condition = this.current.condition
            this.tempC = this.current.temp_c
            this.conditionDescription = this.condition.text
            this.icon = this.condition.icon
            // for (let index = 0; index < this.data.length; index++) {
            //     this.element = this.data[index];
            //     console.log(this.element[1])

            // }
        })
      },
  }
}
</script>
