<template>
    <h1>
        {{welcome}}
    </h1>
    <div>
        {{data}}
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
          location: 'Dublin',
          aqi: 'yes'
      }
  },
  mounted() {
      axios.post(this.baseUrl+this.apiMethod+'?'+this.key+'&'+'q='+this.location+'&'+'aqi='+this.aqi)
        .then(response => {
            this.data = response.data
            console.log(this.data)
        })
  }
}
</script>
