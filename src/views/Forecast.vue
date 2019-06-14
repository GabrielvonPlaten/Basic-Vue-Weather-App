<template>
  <div class="weather-form-container">
    <div class="row">
      <form clas="input-field col weather-form" v-on:submit="call_weather">
        <input class="validate" name="city" placeholder="City name" v-model="cityInput">
        <button 
          class="waves-effect waves-light btn green darken-2 z-depth-2 hoverable form-button">
          Submit
        </button>
        <button 
          class="waves-effect waves-teal btn grey z-depth-2 hoverable form-button"
          v-on:click="clearForecast">
          Clear
        </button>
      </form>

      <!-- Conditional Render If city is not found or state is cleared -->
      <div v-if="forecast.length > 0">
        <ForecastItems :forecast="forecast" :imgSrc="weatherIcon" :cityName="cityName"/>
      </div>
      <div v-else-if="fetchError === true">
        <h4 class="red-text text-darken-1 center-align">City Not Found!</h4> 
      </div>
      <div v-else>
        <h2 class="grey-text center-align empty-field-title">Search for a city in the text field!</h2> 
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import ForecastItems from '../components/ForecastItems.vue';

export default {

  data() {
    return {
      cityInput: '',
      cityName: '',
      forecast: [],
      fetchError: false,
      weatherIcon: 'https://openweathermap.org/img/w/',
      err: null,
    }
  },

  methods: {
    call_weather(e) {
      e.preventDefault();
      
      axios.get(`https://api.openweathermap.org/data/2.5/forecast?q=${this.cityInput}&APPID=15f9383f7cb16f45317f5c373dcf6dfe&units=metric`)
        .then(res => {
          this.forecast = res.data.list;
          this.cityName = res.data.city.name;
          this.cityInput = '';
          this.fetchError = false;
          this.err = null;
        })
        .catch(err => {
          this.fetchError = true;
          this.forecast = [];
          this.err = err;
        });
    },

    clearForecast(e) {
      e.preventDefault();
      this.fetchError = false;
      this.forecast = [];
    }
  },

  components: {
    ForecastItems: ForecastItems,
  }
}
</script>

<style lang="scss">
  .weather-form {
    margin: 0 auto;
  }

  .weather-form-container {
    margin: 0 auto;
  }

  .weather-form-container button:nth-last-child(1) {
    margin-left: 10px;
  }

  @media screen and (max-width: 1340px) {
    .empty-field-title {
      font-size: 2em; 
    }
  }

  @media screen and (max-width: 399px) {
    .empty-field-title {
      font-size: 1.7em; 
    }
  }

  @media screen and (max-width: 338px) {
    .empty-field-title {
      font-size: 1.4em; 
    }
  }
</style>


