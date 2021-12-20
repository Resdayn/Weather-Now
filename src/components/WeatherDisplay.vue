<template>
  <section id="weatherDisplay">
    <div id="cityName">{{ weatherData.name }}</div>
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
      const description = this.weatherData.description;
      const words = description.split(" ");
      for (let i = 0; i < words.length; i++) {
        words[i] = words[i][0].toUpperCase() + words[i].substr(1);
      }
      const descriptionCapitalized = words.join(" ");
      return descriptionCapitalized;
    },
  },
};
</script>

<style scoped>
#weatherDisplay {
  display: grid;
  grid-template-areas:
    "cityName cityName cityName cityName"
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
