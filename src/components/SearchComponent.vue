<!-- This component represents the search bar where the user types the city name. Upon submission, the data is fetched
from the API and a new object is created with only the required data. This object is then emitted to App.vue to be sent as props for WeatherDisplay.vue -->
<template>
  <section>
    <input
      @keydown="cleanNotFound"
      @keydown.enter="submitCity"
      v-model="cityInput"
      type="text"
      placeholder="Type a city"
    />
    <p v-if="notFound">Sorry, the city "{{ this.cityInput }}" can't be found</p>
    <button @click="submitCity">Submit</button>
  </section>
</template>

<script>
export default {
  emits: ["sendData"],
  data() {
    return {
      cityInput: "",
      notFound: false,
    };
  },
  methods: {
    async submitCity() {
      this.notFound = false;
      try {
        const cityWeather = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.cityInput}&units=metric&APPID=ec8cf6e7dcf475ec14f176624d9fd3ed`
        ).then((value) => value.json());
        if (Object.keys(cityWeather).length === 2) {
          this.notFound = true;
          throw Error(`${cityWeather.message}`);
        }

        const requiredWeatherData = {
          name: cityWeather.name,
          description: cityWeather.weather[0].description,
          temperature: cityWeather.main.temp,
          feels_like: cityWeather.main.feels_like,
          humidity: cityWeather.main.humidity,
          wind_speed: cityWeather.wind.speed,
          clouds: cityWeather.clouds.all,
          icon: cityWeather.weather[0].icon
        };
        this.$emit("sendData", requiredWeatherData);
      } catch (error) {
        console.log(error);
      }
    },
    cleanNotFound() {
      // removes the "can't find city" error message for each keystroke"
      this.notFound = false;
    },
  },
};
</script>

<style scoped>
section {
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  padding: 3rem 0;
}

input {
  width: 20vw;
  height: 2rem;
  margin-bottom: 2rem;
}

button {
  padding: 1rem 1rem;
}

p {
  margin-bottom: 1rem;
  color: red;
}
</style>
