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
  <style>
  body {
    color: #fff;
    overflow-x: hidden;
    height: 100%;
    background-image: linear-gradient(#81D4FA, #2196F3);
    background-repeat: no-repeat;
}
.card{
  background: bottom;
}

.card0 {
    width: 94%;
}

.card1 {
    background-image: linear-gradient(#2196F3, #81D4FA);
    padding: 30px 20px 30px 50px;
}

.image {
    width: 300px;
    height: 300px;
}

.large-font {
    font-size: 70px;
    font-family: Arial;
}

.fa-sun-o {
    font-size: 22px;
}

.card2 {
    background-color: #607D8B;
    padding: 0px 0px 40px 40px;
}

input {
    background-color: #607D8B;
    padding: 24px 0px 12px 0px !important;
    width: 80%;
    box-sizing: border-box;
    border: none !important;
    border-bottom: 1px solid #CFD8DC !important;
    font-size: 16px !important;
    color: #fff !important;
}

input:focus {
    -moz-box-shadow: none !important;
    -webkit-box-shadow: none !important;
    box-shadow: none !important;
    border-bottom: 1px solid #fff !important;
    outline-width: 0;
    font-weight: 400;
}

::placeholder {
    color: #B0BEC5 !important;
    opacity: 1;
}

:-ms-input-placeholder {
    color: #B0BEC5 !important;
}

::-ms-input-placeholder {
    color: #B0BEC5 !important;
}

.fa-search {
    color: #607D8B;
    background-color: #E1F5FE;
    font-size: 20px;
    padding: 20px;
    width: 20%;
    cursor: pointer;
}

.light-text {
    color: #B0BEC5;
}

.suggestion:hover {
    color: #fff;
    cursor: pointer;
}

.line {
    height: 1px;
    background-color: #B0BEC5;
}

@media screen and (max-width: 500px) {
    .card1 {
        padding-left: 26px;
    }
}
  </style>
  