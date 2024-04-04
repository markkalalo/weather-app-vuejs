<template>
    <div class="container mt-5">
      <h1 class="text-center">Weather App</h1>
      <h3 class="text-center">Kuya Mark Ano na!</h3>
  
      <div class="input-group mb-3">
        <input type="text" class="form-control" v-model="city" placeholder="Enter city name">
        <div class="input-group-append">
          <button class="btn btn-primary" type="button" @click="getWeather">Get Weather</button>
        </div>
      </div>
  
      <WeatherDisplay 
        v-if="weather"
        :weather="weather"
        :tempUnit="tempUnit"
        :currentTemp="currentTemp"
        :currentFeelsLike="currentFeelsLike"
        :currentDate="currentDate"
        :lastUpdatedTime="lastUpdatedTime"
        :toggleTempUnit="toggleTempUnit"
      />
  
      <ErrorMessage v-if="error" :error="error" />
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  import WeatherDisplay from './WeatherDisplay.vue';
  import ErrorMessage from './ErrorMessage.vue';
  
  export default {
    components: {
      WeatherDisplay,
      ErrorMessage
    },
    data() {
      return {
        city: 'London', // Default city
        weather: null,
        error: '',
        tempUnit: 'C' // Default temperature unit
      };
    },
    computed: {
      currentTemp() {
        if (this.tempUnit === 'C') {
          return this.weather.main.temp.toFixed(1);
        }
        return ((this.weather.main.temp * 9/5) + 32).toFixed(1);
      },
      currentFeelsLike() {
        if (this.tempUnit === 'C') {
          return this.weather.main.feels_like.toFixed(1);
        }
        return ((this.weather.main.feels_like * 9/5) + 32).toFixed(1);
      },
      currentDate() {
        return new Date().toLocaleDateString();
      },
      lastUpdatedTime() {
        return new Date(this.weather.dt * 1000).toLocaleTimeString();
      }
    },
    methods: {
      async getWeather() {
        try {
          const response = await axios.get(`https://api.openweathermap.org/data/2.5/weather`, {
            params: {
              q: this.city,
              units: 'metric',
              appid: '9db2f327231c51dbcc175921eb36bea7'
            }
          });
  
          if (response.data.cod !== 200) {
            throw new Error(response.data.message || 'Place not found');
          }
  
          console.log('API Response:', response.data);
  
          this.weather = response.data;
          this.error = '';
  
          setTimeout(() => {
            this.error = '';
          }, 5000);
  
        } catch (error) {
          console.error('Error fetching weather:', error.message);
          this.error = error.message;
  
          setTimeout(() => {
            this.error = '';
          }, 5000);
        }
      },
      toggleTempUnit() {
        this.tempUnit = this.tempUnit === 'C' ? 'F' : 'C';
      }
    }
  };
  </script>
  