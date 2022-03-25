<template>
  <div id="app">
    <main>
      <div class="title">Weather App</div>
      <div class="search-box">
        <input
          type="text"
          placeholder="Search city/country..."
          class="search-bar"
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="(typeof weather.main) != 'undefined' " >
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      api_key: process.env.VUE_APP_WEATHER_API_KEY,
      url_base: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        const url = `${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`;
        fetch(url)
          .then((response) => response.json())
          .then((data) => {
            this.weather = data;
            console.log(data);
          });
      }
    },
    dateBuilder() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date}, ${month} ${year}`;
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
  font-family: "Roboto", sans-serif;
  font-size: 16px;
  color: #333;
  background: #fafafa;
}

.title {
  color: white;
  font-size: 20px;
}

#app {
  background-image: url("assets/kitty.jpeg");
  background-size: cover;
  background-position: bottom;
  transition: all 0.5s ease;
}

main {
  min-height: 100vh;
  padding: 20px;
  background-size: cover;
  background-image: linear-gradient(
      to bottom,
      rgba(0, 0, 0, 0.5),
      rgba(0, 0, 0, 0.5)
    ),
    url("assets/kitty.jpeg");
  display: flex;
  flex-direction: column;
  align-items: center;
}

.search-box {
  width: 50%;
  margin-bottom: 20px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  color: #333;
  background: #fff;
  transition: all 0.5s ease;
}

.search-box .search-bar:focus {
  outline: none;
  border: 1px solid #00bcd4;
}

.location-box .location {
  color: #fff;
  font-size: 90px;
  font-weight: bold;
  text-transform: uppercase;
  text-align: center;
  text-shadow: 0 0 5px #000;
}

.location-box .date {
  color: #fff;
  font-size: 44px;
  text-align: center;
  text-shadow: 0 0 5px #000;
}

.weather-box {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.weather-box .temp {
  display: inline-block;
  width: fit-content;
  padding: 10px 25px;
  border-radius: 5px;
  background-color: rgba(255, 255, 255, 0.2);
  color: #fff;
  font-size: 90px;
  font-weight: bold;
  text-shadow: 3px 5px #000;
  box-shadow: 3px 5px #000;
  margin: 10px;
}

.weather-box .weather {
  color: #ccc;
  font-size: 44px;
  font-weight: bold;
  font-style: italic;
  text-shadow: 0 0 5px #000;
}
</style>
