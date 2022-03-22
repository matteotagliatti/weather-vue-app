<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search"
          v-model="search"
          @keydown.enter="fetchWeather"
        />
      </div>
      <div v-if="Object.entries(weather).length > 0">
        <div class="location-box">
          <p class="location">{{ weather.name }}, {{ weather.sys.country }}</p>
          <p class="date">Date</p>
        </div>
        <div class="weather-box">
          <p class="temperature">{{ Math.round(weather.main.temp) }}°c</p>
          <p class="weather">{{ weather.weather[0].main }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      apikey: "44a0bb060c36bd8495c54fbb5a1101c6",
      url_base: "https://api.openweathermap.org/data/2.5/",
      search: "",
      weather: {},
    };
  },

  methods: {
    fetchWeather() {
      fetch(
        `${this.url_base}weather?q=${this.search}&units=metric&APPID=${this.apikey}`
      )
        .then((data) => {
          return data.json();
        })
        .then(this.setResult);
    },
    setResult(result) {
      this.weather = result;
      console.log(this.weather);
    },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: "Montserrat", sans-serif;
}

#app {
  background-image: url("./assets/bg-cold.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 2rem;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

.search-box {
  width: 100%;
  margin-bottom: 2rem;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1rem;
  font-size: 1.5rem;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  color: #313131;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #fff;
  font-size: 2.5rem;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  color: #fff;
  font-size: 1.5rem;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temperature {
  margin: 2rem 0 1rem 0;
  padding: 1rem 2rem;
  display: inline-block;
  font-size: 7rem;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  border-radius: 1rem;
  color: #fff;
  background-color: rgba(255, 255, 255, 0.25);
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 2.5rem;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
