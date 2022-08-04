<template>
  <div id="app" :style="hourBg >= 6 && hourBg <= 18 ? `background-image : url(${dayBg});` : `background-image : url(${nightBg}); height: ${viewportHeight}px` ">
    <Animation :weatherName="weather" :dayOrNight="isItDayOrNight" :viewportWidth="viewportWidth" :viewportHeight="viewportHeight"/>
    <main :style="`height: ${viewportHeight}px`">
      <div class="search-box">
        <input
          id="search"
          class="search-bar"
          type="text"
          placeholder="Search for a city..."
          autocomplete="off"
          v-model="city"
          @keyup="cityHandler"
        >
        <select class="country-select" v-model="country" @change="countryHandler">
          <option value="" disabled selected hidden>Select a country</option>
          <option value=""></option>
          <option :value="country.alpha2" v-for="(country, countryIndex) in countries" :key='countryIndex'>{{country.name}}</option>
        </select>

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
                <h6 class="value">{{weather.wind.speed}} m/s</h6>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="message no-result" v-else-if="weather.cod == '400' || weather.cod == '404'">
        <h2>Please enter a valid city</h2>
      </div>
      <div class="welcome" v-else>
        <div class="message enter" >
          <h2>WEATHER APP</h2>
        </div>
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
      url_weather_base: 'https://api.openweathermap.org/data/2.5/',
      url_location_base: 'https://api.openweathermap.org/geo/1.0/reverse?',
      city: '',
      country: '',
      query: '',
      countries: [],
      weather : {},
      isItDayOrNight : '',
      hourBg : 0,
      nightBg : require('../src/assets/nightBG.png'),
      dayBg : require('../src/assets/dayBG.png'),
      viewportWidth : null,
      viewportHeight : null

    }
  },
  methods: {
    // Displays Day or Night according to API weather icon
    dayNight() {
      let letterPosition = this.weather.weather[0].icon.length - 1;
      if (this.weather.weather[0].icon[letterPosition] == 'd') {
        this.isItDayOrNight = "Day";
      } else {
        this.isItDayOrNight = 'Night';
      }
    },
    // get country codes for select field
    getCountryCodes() {
      fetch('https://raw.githubusercontent.com/lukes/ISO-3166-Countries-with-Regional-Codes/master/slim-2/slim-2.json')
      .then(res => {
        return res.json();
      })
      // clean up alpha-2 key
      .then(res => {
        res.map(country => {
          country['alpha2']  = country['alpha-2'];
          delete country['alpha-2'];
          delete country['country-code'];
        });
        return res;
      })
      .then(res => this.countries = res);
    },
    cityHandler(e){
      if (e.key === 'Enter') {
        this.fetchWeather();
      }
    },
    countryHandler(){
      if (this.city !== '') {
        setTimeout(() => {
          this.fetchWeather();
        }, 50);
      }
    },
    // Concatenates city and country for the query
    getQuery() {
        this.query = `${this.city},${this.country}`; 
        // this.fetchWeather();
    },
    // API call
    fetchWeather () {
      console.log(`${this.url_weather_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      fetch(`${this.url_weather_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(res => {
        return res.json();
      }).then(this.setResults);
      // this.query = '';
      document.getElementById("search").blur();
    },
    
    // Get location from Geolocation API
    getPosition() {
      const successCallback = (position)=> {
        fetch(`${this.url_location_base}lat=${position.coords.latitude}&lon=${position.coords.longitude}&limit=2&APPID=${this.api_key}`)
        .then(res => {
          return res.json();
        })
        .then(res => {
            this.query = res[0].name;
            this.fetchWeather();
          });
      }
      const errorCallback = (error)=> {
        this.currentPosition = error.message;
      }
      navigator.geolocation.getCurrentPosition(successCallback, errorCallback);
    },


    // Puts results of API call into "weather" object
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
      return `${day} ${date} ${month}, ${year}`;
    }
  },
  created() {
    // defines current time to set day or night Homepage background image
    let d = new Date();
    let hour = d.getHours();
    this.hourBg = hour;
    // Defines device's viewport sizes to be passed onto body, #app, main and .container elements
    let viewportWidth = window.innerWidth;
    let viewportHeight = window.innerHeight;
    this.viewportWidth = viewportWidth;
    this.viewportHeight = viewportHeight;
    setTimeout(() => {
      this.getPosition();
    }, 1000);
    this.getCountryCodes();
  },
  watch : {
    city(newcity) {
      this.city = newcity;
      this.getQuery();
    },
    country(newcountry) {
      this.country = newcountry;
      this.getQuery();
    },
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  margin:0;
  font-family: 'Roboto', sans-serif;
}

#app {
  background-position: top;
  transition: .4s;
  position: relative;
  z-index: 0;
}

main {
  height: 100%;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.1), rgba(0, 0, 0, 0.5));
  z-index: 2;
}
.search-box {
  width: 100%;
  margin-bottom: 20px;
  text-align: center;
}
.search-box {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  .search-bar,
  .country-select,
  .country-select option {
    text-align: center;
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
  .country-select {
    padding: 5px;
    option {
      max-width: 100%;
      font-size: 10px;
    }
  }
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
  text-shadow: 9px 4px 1px rgba(0, 0, 0, 0.25);
  font-size: 39px;
  font-family: 'Montserrat', sans-serif;
}

</style>
