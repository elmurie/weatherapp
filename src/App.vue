<template>
  <div id="app" :style="hourBg >= 6 && hourBg <= 18 ? `background-image : url(${dayBg})` : `background-image : url(${nightBg})`">
    <Animation :weatherName="weather" :dayOrNight="isItDayOrNight"/>
    <main>
      <div class="search-box">
        <input 
          class="search-bar"
          type="text"
          placeholder="Search for a city..."
          v-model="query"
          @keyup="fetchWeather"
        >
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
        <div class="location-box">
          <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
          <div class="date">{{dateBuilder()}}</div>
          <div class="icon">
            <img :src="`http://openweathermap.org/img/wn/${weather.weather[0].icon}.png`" alt="Weather Icon">
            <div class="day-night">{{isItDayOrNight}}</div>
          </div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
          <div class="weather">{{weather.weather[0].main}}</div>
          <div class="weather-extra">
            <div class="top">
              <div class="min">
                <h6 class="title">MIN</h6>
                <h6 class="value">{{Math.round(weather.main.temp_min)}}°C</h6>
              </div>
              <div class="max">
                <h6 class="title">MAX</h6>
                <h6 class="value">{{Math.round(weather.main.temp_max)}}°C</h6>
              </div>
            </div>
            <div class="bottom">
              <div class="humidity">
                <h6 class="title">HUMIDITY</h6>
                <h6 class="value">{{weather.main.humidity}}%</h6>
              </div>
              <div class="wind">
                <h6 class="title">WIND</h6>
                <h6 class="value">{{weather.wind.speed}}m/s</h6>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="message no-result" v-else-if="weather.cod == '400' || weather.cod == '404'">
        <h2>Please enter a valid city</h2>
      </div>
      <div class="message enter" v-else>
        <h2>WEATHER APP</h2>
      </div>
    </main>
  </div>
</template>

<script>
import Animation from './components/Animation.vue';
export default {
  name: 'App',
  components : {
    Animation
  },
  data() {
    return {
      api_key : '5c91c46023d7f1646dce8d2f732f5e3b',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather : {},
      isItDayOrNight : '',
      hourBg : 0,
      nightBg : 'https://i.imgur.com/G8HPRuc.jpg',
      dayBg : 'https://i.imgur.com/fbTfPz5.jpg' 
    }
  },
  methods: {
    dayNight() {
      let letterPosition = this.weather.weather[0].icon.length - 1;
      if (this.weather.weather[0].icon[letterPosition] == 'd') {
        this.isItDayOrNight = "Day";
      } else {
        this.isItDayOrNight = 'Night';
      }
    },
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults);
        this.query = '';
      }
    },
    setResults(results) {
      this.weather = results;
      this.dayNight();
    },
    dateBuilder() {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      let hour = d.getHours;
      this.hourBg = hour;

      return `${day} ${date} ${month}, ${year}`;
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rammetto+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin:k0;
  font-family: 'Roboto', sans-serif;
}

#app {
  background-size: cover;
  background-repeat: no-repeat;
  transition: .4s;
  position: relative;
  z-index: 0;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.5));
  z-index: 2;
}
.search-box {
  width: 100%;
  margin-bottom: 20px;
  text-align: center;
}
.search-box .search-bar {
  display: inline-block;
  width: 100%;
  max-width: 500px;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  font-weight: 400;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 15px;
  transition: .4s;
}

::placeholder {
  color: rgb(31, 31, 31);
  font-weight: 700;
  font-family: 'Roboto', sans-serif;

}

.search-box .search-bar:focus {
  box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 25px;
}

.location-box .location {
  color: #fff;
  font-size: 40px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  text-align: center;
  font-style: italic;
}
.weather-box {
  text-align: center;
  color : #fff;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(65, 65, 65, 0.25);
  border-radius: 16px;
  margin: 15px auto;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  display: block;
  font-size: 45px;
  font-weight: 700;
  color: #fff;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.location-box .icon {
  display: flex;
  justify-content: center;
  align-items: center;
  color: #fff;
}

.location-box .icon img {
  -webkit-filter: drop-shadow(5px 5px 2px #222);
  filter: drop-shadow(0px 0px 5px #fff);
}
.location-box .icon .day-night {
  font-size: 30px;
  font-weight: 500;
}

.weather-extra,
.weather-extra .top,
.weather-extra .bottom {
  display: flex;
}

.weather-extra {
  max-width: 500px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 20px auto;
}

.weather-extra h6 {
  font-size: 28px;
  text-shadow: 3px 3px rgba(0, 0, 0, 0.25);
}

.weather-extra .top,
.weather-extra .bottom {
  justify-content: space-around;
  width: 95%;
  margin: 10px 0;
}

.message {
  text-align: center;
}
.message h2 {
  color : #ffffff;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
  font-size: 54px;
}

.enter {
  font-family: 'Rammetto One', cursive;
}

</style>
