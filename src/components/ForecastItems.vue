<template>
  <div>
    <h4  
      v-if="cityName">
      The weather of <span class="green-text text-darken-2">{{ cityName }}</span>
    </h4>
    <ul class="forecast-list">
      <li 
        v-for="(day, index) in forecast" 
        :id="day" 
        :Key="index" 
        class="z-depth-1 hoverable forecast-list-item">
        <span class="list-header">
          <img v-bind:src="imgSrc + day.weather[0].icon + '.png'" class="left-align">
          <span class="temperature">{{ Math.floor(day.main.temp) }} C°</span>
        </span>
        <p>{{ day.weather[0].description }}</p>
        <p>{{ day.dt_txt }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ['forecast', 'imgSrc', 'cityName'],

  data() {
    return {

    }
  },
}
</script>

<style lang="scss" scoped>

.forecast-list {
  padding: 0;
  margin: 0 auto;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  color: #2c3e50;
  font-weight: bold;
  text-transform: capitalize;
  width: 85%;
}


.forecast-list-item {
  margin: 4px;
  padding-bottom: 6px;
}

.forecast-list-item p {
  margin: 0;
  text-align: center;
}

.forecast-list-item img {
  width: 25%;
  height: 25%;
}

.list-header {
  display: flex;
  justify-content: space-around;
  margin: 10px 0;
}

.temperature {
  margin-top: 5px;
  font-size: 1.7em;
  font-weight: 400;
  border-spacing: 100px;
  color: #616161;
}

@media screen and (max-width: 1340px) {
  .forecast-list {
    width: 95%;
  }
}

@media screen and (max-width: 1020px) {
  .forecast-list {
    width: 98%;
  }
}

@media screen and (max-width: 964px) {
  .forecast-list {
    grid-template-columns: repeat(5, 1fr);
    width: 100%;
  }
  
  .forecast-list-item {
    margin: 8px;
  }
}

@media screen and (max-width: 774px) {
  .forecast-list {
    grid-template-columns: repeat(4, 1fr);
  }

  .forecast-list-item {
    margin: 6px;
  }
}

@media screen and (max-width: 480px) {
  .forecast-list {
    grid-template-columns: repeat(2, 1fr);
  }

  .forecast-list-item {
    margin: 4px;
  }
}
</style>
