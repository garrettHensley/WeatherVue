<template>
  <div class="hello container mt-3 ">
    <div class="card-deck">
      <div
        v-for="day in info.slice(0, 5)"
        :key="day.id"
        class="card border-dark mb-3 mx-auto"
        style="max-width: 18rem;"
      >
        <div class="card-header :style={}">
          {{ Day(day.dt) }} {{ getDate(day.dt) }}
        </div>
        <div class="card-body text-dark">
          <!-- Lets eventually add a button that lets you pick which conversion you want. For now we will default F -->
          <h5 class="card-title" style="text-transform:capitalize;">
            {{ day.weather[0].description }}
          </h5>
          <small class="text-muted">Day</small>
          <p class="card-text lead">{{ convertTo(day.temp.day, "F") }}°</p>
          <small class="text-muted">Night</small>
          <p class="card-text lead">{{ convertTo(day.temp.night, "F") }}°</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
var pos = "ass";

console.log(pos);
export default {
  data() {
    return {
      info: null,
    };
  },
  mounted() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/onecall?lat=60.99&lon=30.9&appid=01dca2b05ee4bb1b44311bfc21622618`
      )
      .then((response) => (this.info = response.data.daily));
  },
  methods: {
    Day(time) {
      let date = new Date(time * 1000);
      let day;
      if (date.getDay() === 0) {
        day = "Sunday";
      } else if (date.getDay() === 1) {
        day = "Monday";
      } else if (date.getDay() === 2) {
        day = "Tuesday";
      } else if (date.getDay() === 3) {
        day = "Wednesday";
      } else if (date.getDay() === 4) {
        day = "Thursday";
      } else if (date.getDay() === 5) {
        day = "Friday";
      } else if (date.getDay() === 6) {
        day = "Saturday";
      }
      return day;
    },
    getDate(time) {
      let date = new Date(time * 1000);
      return `${date.getMonth() + 1}/${date.getDate()}`;
    },
    convertTo(K, str) {
      if (str === "F") {
        return Math.floor(K * (9 / 5) - 459.67);
      }
    },
    getWeather(weatherType) {
      //
      return `/assets/${weatherType}.jpg`;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.cloudy {
  background-image: url(../assets/clouds.jpg);
}
.sunny {
}
.rainy {
}
</style>
