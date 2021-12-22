<!-- App.vue will pass the data received from SearchComponent to WeatherDisplay as a prop.
The WeatherDisplay component won't be shown until the sendData listener has been triggered at least one time  -->
<template>
  <section id="app-body">
    <the-title></the-title>
    <search-component @sendData="displayData"></search-component>
    <weather-display v-if="showDisplay" :weatherData="this.weatherData"></weather-display>
  </section>
</template>

<script>
import SearchComponent from "./components/SearchComponent.vue";
import WeatherDisplay from "./components/WeatherDisplay.vue"

export default {
  data() {
    return {
      weatherData: {},
      showDisplay: false
    }
  },
  name: "App",
  components: {
    SearchComponent,
    WeatherDisplay
  },
  methods: {
    displayData(data) {
      this.showDisplay = true;
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
body {
  min-height: 100vh;
  background: linear-gradient(to bottom, #63A1F2 0%, #67B0F3 50%, #577EF2 100%);
}
#app-body {
  width: 100vw;
  height: 100%;
}
</style>
