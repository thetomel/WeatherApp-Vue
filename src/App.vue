<template>
  <div id='app'>
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Tell me the place..." v-model="query" @keypress="fetchWeather">
      </div>
       <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
          <div class="location-box">
            <div class="location">{{weather.name}}, {{weather.sys.country}}</div>
            <div class="date">Null</div>
          </div>
          <div class="weather-box">
              <div class="temperature">{{ Math.round(weather.main.temp)}}°C</div>
              <div ckass="weather">{{weather.weather[0].main}}</div>
          </div>
       </div>
       <div class="weather-none" v-else>
        <p>Nothing to se here</p>
        Try type something in search bar!
       </div>
    </main>
   </div>
    
</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: 'cc5a1df2395ce9e06bbf15bbe9e7d8fc',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }

  },
  methods: {
    fetchWeather (e) { 
      if (e.key == "Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then( response => {
           return response.json();
        }).then(this.setResults);
      }
    },
    setResults (results) {
       this.weather = results;
    }
  }

}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-boxs;
}
body{
  font-family: 'Barlow', sans-serif;;
}
#app{
  background-image: url('./assets/back.png');
  background-size: cover;
  transition: 0.4s;
  position: bottom; 
  
}
main {
  min-height: 100vh;
  text-align: center;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}
.search-box{
  display: flex;
  align-items: center;
}
.search-box .search-bar{
   display: block;
   width: 100%;
   padding: 15px;

   color: #323232;
   font-size: 20px;

   appearance: none;
   border: none;
   outline: none;
   background: none;

   box-shadow: 0px 0px 16px;
   background-color: rgba(255,255,255,0.5);
   border-radius: 8px 2px 16px 2px;
}
.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0,0,0,0.5);
   border-radius: 10px 6px 20px 6px;
    background-color: rgba(255,255,255,0.75);
}
.location-box {
  color: white;
  text-align: center;
  margin-top: 10px;
  font-size: 32px;
  font-weight: 500;
  text-shadow: 1px 4px rgba(0,0,0,0.25);
}
.location-box .date{
  font-size: 30px;
  font-weight: 300;
}
.weather-box {
  text-align: center;
  color: white;
  padding:  10px 25px;
}
.weather-box .temperature{
  font-size: 102px;
  padding:  10px 15px;
  text-shadow: 3px 7px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 10px;
  margin: 30px 0px;
  box-shadow: 3px 7px rgba(0,0,0,0.25);
}
.weather-box .weather{
  text-shadow: 3px 7px rgba(0,0,0,0.25);
}
.weather-none{
  color: aliceblue;
  padding: 20px;
}
.weather-none > p{
  font-size: 40px;
  font-weight: 400;
  text-shadow: 3px 4px rgba(0,0,0,0.25);
}

</style>
