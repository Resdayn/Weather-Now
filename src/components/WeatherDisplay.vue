<!-- This component receives the object weatherData from App.vue and displays the information and icon -->
<template>
  <section id="weatherDisplay">
    <div id="date">{{ todayDate }}</div>
    <div id="cityName">{{ weatherData.name }}</div>
    <div id="currentWeatherIcon">
      <img :src="getIcon" />
    </div>
    <div id="weatherDescription">{{ weatherDescription }}</div>
    <div id="currentTemp">
      <h3>{{ Math.round(weatherData.temperature) }}°</h3>
    </div>

    <section id="box">
      <div id="windColumn">
        <h3 class="box-title">Wind Speed</h3>
        <img class="icon" src="../assets/icons/wind.png" />
        <div id="wind">{{ weatherData.wind_speed }} m/s</div>
      </div>
      <div id="humidityColumn">
        <h3 class="box-title">Humidity</h3>
        <img class="icon" src="../assets/icons/humidity.png" />
        <div id="humidity">{{ weatherData.humidity }}%</div>
      </div>
      <div id="temperatureColumn">
        <h3 class="box-title">Feels like</h3>
        <img class="icon" src="../assets/icons/temp.png" />
        <div id="feelsLike">{{ Math.round(weatherData.feels_like) }}°C</div>
      </div>
      <div id="cloudColumn">
        <h3 class="box-title">Clouds</h3>
        <img class="icon" src="../assets/icons/clouds.png" />
        <div id="cloud">{{ weatherData.clouds }}%</div>
      </div>
    </section>
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
    getIcon() {
      // the require is needed to let know webpack that this is a url.
      return require(`../assets/icons/${this.weatherData.icon}.png`);
    },
    todayDate() {
      const dateNow = new Date();
      // const month = dateNow.getUTCMonth();
      // const day = dateNow.getUTCDay();
      return `${dateNow.toLocaleString("en-US", {
        month: "short",
      })} ${dateNow.getUTCDate()}, ${dateNow.getUTCFullYear()} (UTC)`;
    },
  },
};
</script>

<style scoped>
* {
  color: #fcfefc;
}
#weatherDisplay {
  display: grid;
  grid-template-areas:
    "date"
    "cityName"
    "icon"
    "weatherDescription"
    "currentTemp"
    "box";
  place-items: center;
  justify-content: center;
  gap: 2rem;
  font-size: 30px;
  margin-bottom: 3rem;
}

#date {
  grid-area: date;
}

#cityName {
  grid-area: cityName;
  font-size: 40px;
}
#currentWeatherIcon {
  grid-area: icon;
}
#currentWeatherIcon img {
  width: 150px;
  height: 150px;
}
#weatherDescription {
  grid-area: weatherDescription;
}
#currentTemp {
  grid-area: currentTemp;
}
@import url('https://fonts.googleapis.com/css2?family=Cairo&display=swap');
#currentTemp h3{
  font-family: 'Cairo', sans-serif;
  color: #c5d9f7;
  font-size: 100px;
}
#box {
  display: flex;
  place-items: center;
  justify-content: center;
  grid-area: box;
  background: linear-gradient(to right, #2c4373 0%, #3a5286 50%, #2c4373 100%);
  padding: 2rem;
  border-radius: 25px;
}

#windColumn {
  grid-area: windColumn;
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  margin: 0px 2rem;
}
#humidityColumn {
  grid-area: humidityColumn;
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  margin: 0px 2rem;
}
#temperatureColumn {
  grid-area: temperatureColumn;
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  margin: 0px 2rem;
}
#cloudColumn {
  grid-area: cloudColumn;
  display: flex;
  flex-direction: column;
  place-items: center;
  justify-content: center;
  margin: 0px 2rem;
}

#windColumn,
#humidityColumn,
#temperatureColumn,
#cloudColumn {
}
.box-title {
  color: #97a9c7;
  margin-bottom: 1rem;
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

.icon {
  width: 30px;
  height: 30px;
  margin-bottom: 1rem;
}
@media screen and (max-width: 900px){
  #box {
    transform: scale(0.9);
  }
}
@media screen and (max-width: 600px){
  #box {
    transform: scale(0.7);
  }
}

@media screen and (max-width: 500px){
  #box {
    flex-direction: column;
    width: 80vw;
  }
}
@media screen and (max-width: 450px){
  #box {
    flex-direction: column;
    width: 90vw;
  }
}
</style>
