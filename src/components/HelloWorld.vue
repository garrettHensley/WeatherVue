<template>
  <div class="hello container mt-3 ">
    <div class="location">
      <div class="d-inline-flex pt-2 px-2 temp text-light">
        <input type="radio" id="one" value="F" v-model="temp" />
        <label for="one">Fahrenheit</label>

        <input type="radio" id="two" value="C" v-model="temp" />
        <label for="two">Celsius</label>
      </div>
      <p class="d-inline-flex lead px-5 text-light">
        5-day Forcast for Sarasota, Florida
      </p>
    </div>
    <div class="container deck-holder p-3">
      <div class="card-deck">
        <div
          v-for="day in info.slice(0, 5)"
          :key="day.id"
          :class="day.weather[0].main"
          class="card border-dark mb-3 mx-auto text-light"
          style="max-width: 18rem;"
        >
          <div class="card-header">
            <span>{{ Day(day.dt) }} {{ getDate(day.dt) }}</span>
          </div>
          <div class="card-body">
            <!-- Lets eventually add a button that lets you pick which conversion you want. For now we will default F -->
            <h5
              class="card-title text-light"
              style="text-transform:capitalize;"
            >
              {{ day.weather[0].description }}
            </h5>
            <small class="text-white-50">Day</small>
            <p class="card-text lead text-light">
              {{ convertTo(day.temp.day, temp) }}°
            </p>
            <small class="text-white-50">Night</small>
            <p class="card-text lead text-light">
              {{ convertTo(day.temp.night, temp) }}°
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      info: null,
      temp: "F",
    };
  },
  mounted() {
    axios
      .get(
        `https://api.openweathermap.org/data/2.5/onecall?lat=27.33&lon=27.33&appid=01dca2b05ee4bb1b44311bfc21622618`
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
      } else if (str === "C") {
        return Math.floor(K - 273.15);
      } else {
        return K;
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
.Clouds {
  background-image: linear-gradient(rgba(1, 0, 0, 0.8), rgba(28, 100, 0, 0.2)),
    url(../assets/clouds.jpg);
  background-size: cover;
}
.Clear {
  background-image: linear-gradient(
      rgba(155, 133, 133, 0.5),
      rgba(0, 0, 0, 0.5)
    ),
    url(../assets/clear.jpg);
  background-size: cover;
}
.Rain {
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),
    url(../assets/rain.jpg);
  background-size: cover;
}

.temp {
  background-color: #413537;
  border-radius: 0.5rem 0.5rem 0 0;
}
.location {
  background-color: #373541;
}
.deck-holder {
  background-color: #353d41;
  border-radius: 0 0.5rem 0.5rem 0.5rem;
}
</style>
