<template>
  <div id="app">
   <main>
    <div class="search-box">
      <input type="text" class="search-bar" placeholder="Search country..."
      v-model="$data.city" @keyup.enter="getWeather()">
      
      <div class="weather-wrap">
        <div class="location-box">
          <div class="location"> {{ $data.city }}</div>
          <div class="date">{{ new Date().toLocaleString() }}</div>

        </div>
      </div>
      <div class="weather-box">
        <div class="temp">{{this.data.weather.main.temp}}&deg;</div>
        <div class="weather">Rain</div>
      </div>
    </div>
   </main>
  </div>
</template>

<script>

import axios from 'axios'
export default {
  name: 'App',
  components: {
  
  },
  data(){
    return{
      api_key:'581be601477c8281e3c52f55c3d63a7d',
      city:'',
      weather:'',
      current_day:''
    }
  },
  methods:{
    async  getWeather(){

      const result= await axios.get(
         `https://api.openweathermap.org/data/2.5/weather?q=${this.data.city}&appid=${this.data.api_key}`
      )

      this.data.weather=result.data;

      console.log(this.data.weather);


      
    }

   
    },
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;

}

#app{
  background-image: url('./assets/1.png');
  background-position: bottom;
  background-size: cover;
  transition: 0.5s;
  
}

main{
  min-height: 100vh;
  padding:25px;
  /* background-image: linear-gradient(to bottom,rgba(0,0,0.25),rgba(0,0,0.75)); */
}

.search-box{
  width: 100%;
  margin-bottom: 30px;

}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: #31313131;
  font-size: 18px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
  box-shadow: 0px 0px 8px rgba(0,0,0.25);
}
.search-box .search-bar:focus{ 
  background-color: rgba(255,255,255,0.75);
  box-shadow: 0px 0px 16px rgba(0,0,0.25);
  border-radius: 16px 0px 16px 0px;
}
.location-box .location{
  margin-top: 20px;
  font-size: 30px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0.75);
}

.location-box .date{
   margin-top: 15px;
  font-size: 20px;
  font-weight: 700;
  text-align: center;
  /* text-shadow: 1px 3px rgba(0,0,0.15); */
  font-style: italic;
}

.weather-box{
  text-align: center;
}
.weather-box .temp{
  margin-top: 30px;
  display: inline-block;
  padding: 10px 25px;
  font-size: 80px;
  font-weight: 500;
  border-radius: 15px;
  background-color: rgba(255,255,255,0.5);
  /* box-shadow: 3px 6px rgba(0,0,0.25); */
}
.weather-box .weather{
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  margin-top: 20px;
}
</style>
