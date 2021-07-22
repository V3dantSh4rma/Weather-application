<template>
  <div id="app">
    <div class="title">
      <title> Weather Searcher </title>
      <h1> Weather Searcher </h1>
    </div>
    
    <div class="search-bar">
      <input 
      type = "text" 
      placeholder="Enter the City here..." 
      class = "search"
      v-model="query"
      @keypress="getWeather"/>
    </div>

    <div class="footer">
      <h1> Website made using VueJS. </h1>
    </div>

    <div class="nav-bar">
      <ul>
        <li><a href = "#"> Home </a></li>
        <li><a href="https://discord.gg/MzD9z6gDYV"> Join our Discord! </a></li>
      </ul>
    </div>

    <div class="main-box">
      <div class="dtl" v-if="typeof weather.main != 'undefined'" > 
        <p class = "location"> {{ weather.name}} , {{ weather.sys.country }} </p>
        <p class = "date"> {{dateBuild()}} </p>
        <p class = "temp"> {{ Math.round(weather.main.temp)}}℃</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data (){
    return{
      api_url: "https://api.openweathermap.org/data/2.5/",
      api_key: "8e7a8ee9cfa3e74bebf51e39857bedec",
      query: '',
      weather: {}
    }
  },

  methods: {

    getWeather(e){
      if(e.key === "Enter"){
        fetch(`${this.api_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(
          res => {
            return res.json();
          }
        ).then(this.setResults);
      } 
    },

    setResults (results){
      this.weather = results;
    },

    dateBuild(){
      let dt = new Date();
      let months = ['January' , 'February' , 'March' , 'April' , 'May' , 'June' , 'July' , 'August' , 'September' , 'October' , 'Novemver' , 'December'];
      let weeks = ['Monday' , ' Tuesday' , 'Wednesday' , 'Thursday' , 'Friday', 'Saturday' , 'Sunday'];
      
      let current_date = dt.getDate();
      let current_week = weeks[dt.getDay()];
      let current_year = dt.getFullYear();
      const current_month = months[dt.getMonth()];

      return `${current_date} ${current_month}, ${current_week} ${current_year}`
    }
  }
}
</script>

<style>
*{
  margin: 0%;
  padding: 0;
  backface-visibility: visible;
  background-color: rgb(24,24,24);
}

.title{
  position: absolute;
  font-display: initial;
  font-family: monospace;
  font-size: medium;
  color: white;
  top:05%;
  left: 40%;
  margin: 2px;
  padding: 12px solid #fff;
  margin: auto;
  border-radius: 12px;
}

.dtl{
  display: initial;
  position: absolute;
  font-size: 150%;
  position: absolute;
  left: 40%;
  top: 30%;
  font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
  font-stretch: ultra-condensed;
  font-size: xx-large;
  color: white;
  border: 2px solid white;
  border-radius: 12px;
  padding: 20px;
}

.main-box{
  background-color: #fff;
  align-items: center;
  position: absolute;
  justify-content: center;
  top: 24%;
  left: 40%;
  border-radius: 10px;
  margin: 20px auto;
  border-radius: 25px;
  margin: 2px solid;
}
.dtl .temp{
  font-size: 30px;
}

.dtl .location{
  font-size: 40px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.dtl .time{
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.dtl .date{
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.dtl .temp{
  display: inline-block;
  padding: 10px 25px;
  font-display: initial;
  font-size: 102px;
  font-weight: 300;
}

.search-bar{
  width: 30%;
  position: relative;
  position: absolute;
  top: 15%;
  left: 40%;
}


.search-bar:focus{
  color: #000;
  box-shadow: 0 0 5px #fd5e53;
}

.search-bar .btn{
  width: 45px;
  height: 36px;
  border: 1px soid #000000;
  background-color: black;
}

.footer{
  color: white;
  font-display: inherit;
  font-family: sans-serif;
  position: absolute;
  display: flex;
  flex-direction: column;
  top: 80%;
  left: 35%;
  font-size: 15px;
}

.nav-bar ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  align-items: center;
  justify-items: center;

}

.nav-bar li {
  float: left;
}

.nav-bar li a {
  display: block;
  color: white;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
}

.search-bar .search{
  width: 50%;
  border: none;
  padding: 2px solid;
  border-radius: 12px;
  position: absolute;
  background-color: white;
  width: 80%;
  height: 2rem;
  position: absolute;
  margin: auto;
}

#app, *{
  margin: auto;
}
</style>
