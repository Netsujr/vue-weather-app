<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" placeholder="Search..." id="" class="search-bar" />
      </div>

      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">London</div>
          <div class="date">Monday</div>
        </div>
        <div class="weather-box">
          <div class="temp">23°C</div>
          <div class="weather">Rain</div>
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

#app {
  background-image: url("https://images.unsplash.com/photo-1518791841217-8f162f1e1131?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80");
  background-size: cover;
  background-position: bottom;
  transition: all 0.5s ease;
}

main {
  min-height: 100vh;
  padding: 20px;
  background-image: linear-gradient(
      to bottom,
      rgba(0, 0, 0, 0.5),
      rgba(0, 0, 0, 0.5)
    ),
    url("https://images.unsplash.com/photo-1518791841217-8f162f1e1131?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80");
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
  border-color: #00bcd4;
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
