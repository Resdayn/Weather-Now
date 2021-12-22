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
  </section>
</template>

<script>
export default {
  emits: ["sendData"],
  data() {
    return {
      cityInput: "",
      notFound: false,
      token: require("../../token")
    };
  },
  methods: {
    async submitCity() {
      this.notFound = false;
      try {
        const cityWeather = await fetch(
          `https://api.openweathermap.org/data/2.5/weather?q=${this.cityInput}&units=metric&APPID=${this.token.config.token}`
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
          icon: cityWeather.weather[0].icon,
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
  height: 3rem;
  border: 0;
  border-bottom: 2px solid #2C4373;
  text-align: center;
  font-size: 30px;
  background: transparent;
  color: #bbdefb;
}
input:focus {
  outline: none;
}

button {
  padding: 1rem 1rem;
}

p {
  margin-bottom: 2rem;
  color: rgb(235, 77, 77);
}
@media screen and (max-width: 1700px) {
  input {
    width: 50vw;
  }
}
@media screen and (max-width: 700px) {
  input {
    width: 80vw;
  }
}
</style>
