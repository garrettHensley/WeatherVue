<template>
  <div class="home">
    <WeatherTrack />
  </div>
</template>

<script>
// @ is an alias to /src
import WeatherTrack from "@/components/WeatherTrack.vue";

export default {
  name: "Home",
  components: {
    WeatherTrack
  },
};
</script>

<style>
body {
  background-color: #374e5a;
}
</style>
