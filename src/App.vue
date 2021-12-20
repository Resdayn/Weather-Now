<template>
  <section id="app-body">
    <the-title></the-title>
    <search-component @sendData="displayData"></search-component>
    <weather-display :weatherData="this.weatherData"></weather-display>
  </section>
</template>

<script>
import SearchComponent from "./components/SearchComponent.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue"

export default {
  data() {
    return {
      weatherData: {}
    }
  },
  name: "App",
  components: {
    SearchComponent,
    WeatherDisplay
  },
  methods: {
    displayData(data) {
      console.log("Displaying Data from App.vue");
      console.log(data);
      this.weatherData = data;
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app-body {
  width: 100vw,
}
</style>
