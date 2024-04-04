<template>
    <div class="card">
      <h2 class="card-header">{{ weather.name }}, {{ weather.sys.country }}</h2>
  
      <div class="card-body">
        <div class="row">
          <div class="col-6">
            <p><strong>Current Date:</strong> {{ currentDate }}</p>
            <p><strong>Last Updated:</strong> {{ lastUpdatedTime }}</p>
          </div>
          <div class="col-6 text-right">
            <p><strong>Weather:</strong> {{ weather.weather[0].description }}</p>
            <img :src="'https://openweathermap.org/img/wn/' + weather.weather[0].icon + '.png'" :alt="weather.weather[0].description">
          </div>
        </div>
  
        <div class="row">
          <div class="col-6">
            <p><strong>Temperature:</strong> {{ currentTemp }}°{{ tempUnit }}</p>
            <p><strong>Feels Like:</strong> {{ currentFeelsLike }}°{{ tempUnit }}</p>
          </div>
          <div class="col-6 text-right">
            <p><strong>Humidity:</strong> {{ weather.main.humidity }}%</p>
            <p><strong>Wind:</strong> {{ weather.wind.speed }} m/s, {{ weather.wind.deg }}°</p>
            <p><strong>Cloudiness:</strong> {{ weather.clouds.all }}%</p>
            <p><strong>Sunrise:</strong> {{ new Date(weather.sys.sunrise * 1000).toLocaleTimeString() }}</p>
            <p><strong>Sunset:</strong> {{ new Date(weather.sys.sunset * 1000).toLocaleTimeString() }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      weather: {
        type: Object,
        required: true
      },
      tempUnit: {
        type: String,
        required: true
      },
      currentTemp: {
        type: String,
        required: true
      },
      currentFeelsLike: {
        type: String,
        required: true
      },
      currentDate: {
        type: String,
        required: true
      },
      lastUpdatedTime: {
        type: String,
        required: true
      },
      toggleTempUnit: {
        type: Function,
        required: true
      }
    }
  };
  </script>
  