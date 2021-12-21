<!-- This component receives the object weatherData from App.vue and displays the information and icon -->
<template>
  <section id="weatherDisplay">
    <div id="cityName">{{ weatherData.name }}</div>
    <div id="icon">
      <img :src="getIcon">
    </div>
    <div id="weatherDescription">{{ weatherDescription }}</div>
    <div id="temperatureColumn">Temperature</div>
    <div id="humidityColumn">Humidity</div>
    <div id="windColumn">Wind Speed</div>
    <div id="cloudColumn">Clouds</div>
    <div id="currentTemp">Current: {{ Math.round(weatherData.temperature) }}°C</div>
    <div id="feelsLike">Feels like {{ Math.round(weatherData.feels_like) }}°C</div>
    <div id="humidity">{{ weatherData.humidity }}%</div>
    <div id="wind">{{ weatherData.wind_speed }} m/s</div>
    <div id="cloud">{{ weatherData.clouds }}%</div>
  </section>
</template>

<script>
export default {
  props: ["weatherData"],
  computed: {
    weatherDescription() {
      // To capitalize the first letter of each word in the weather description
      const description = this.weatherData.description;
      const words = description.split(" ");
      for (let i = 0; i < words.length; i++) {
        words[i] = words[i][0].toUpperCase() + words[i].substr(1);
      }
      const descriptionCapitalized = words.join(" ");
      return descriptionCapitalized;
    },
    getIcon(){
      // the require is needed to let know webpack that this is a url.
      return require(`../assets/icons/${this.weatherData.icon}.png` );
    }
  },
};
</script>

<style scoped>
#weatherDisplay {
  display: grid;
  grid-template-areas:
    "cityName cityName cityName cityName"
    "icon icon icon icon"
    "weatherDescription weatherDescription weatherDescription weatherDescription"
    "temperatureColumn humidityColumn windColumn cloudColumn"
    "currentTemp humidity wind cloud"
    "feelsLike humidity wind cloud";
  place-items: center;
  justify-content: center;
  gap: 2rem;
  font-size: 30px;
}

#cityName {
  grid-area: cityName;
  font-size: 40px;
}
#icon {
  grid-area: icon;
}
#icon img {
  width: 200px;
  height: 200px;
}
#weatherDescription {
  grid-area: weatherDescription;
}
#temperatureColumn {
  grid-area: temperatureColumn;
}
#humidityColumn {
  grid-area: humidityColumn;
}
#windColumn {
  grid-area: windColumn;
}
#cloudColumn {
  grid-area: cloudColumn;
}
#currentTemp {
  grid-area: currentTemp;
}
#feelsLike {
  grid-area: feelsLike;
}
#humidity {
  grid-area: humidity;
}
#wind {
  grid-area: wind;
}
#cloud {
  grid-area: cloud;
}
</style>
